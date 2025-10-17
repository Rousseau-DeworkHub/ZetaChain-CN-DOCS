| 标题 | 描述 |
| :- | :- |
| Solana | 介绍如何通过 Solana Gateway 与通用应用交互、存入资产并处理回退。 |

# Solana

在 Solana 上与通用应用（Universal Apps）交互时，需要使用 **Solana Gateway**。  
Solana Gateway 支持以下操作：

- 将 SOL 存入 ZetaChain 上的通用应用或账户  
- 存入已支持的 SPL token  
- 存入 SOL 并调用通用应用  
- 存入已支持的 SPL token 并调用通用应用  

---

## 存入 SOL（Deposit SOL）

要将 SOL 存入外部拥有账户（EOA）或通用合约，请调用 Solana Gateway 程序的 `deposit` 指令：

```rust
pub fn deposit(ctx: Context<Deposit>, amount: u64, receiver: [u8; 20], revert_options: Option<RevertOptions>) -> Result<()>
```

`deposit` 指令接收以 lamports 为单位的 SOL，并将其发送至 ZetaChain 上的 `receiver`。  
请注意，1 SOL = 1,000,000,000 lamports，在指定 `amount` 参数时需进行换算。

`receiver` 可以是外部拥有账户（EOA）或 ZetaChain 上的通用应用地址。  
即使接收方是具有标准 `receive` 函数的通用应用合约，`deposit` 指令也不会触发合约调用。  
如果希望在存入的同时调用通用应用，请使用 `deposit_and_call` 指令。

存入处理完成后，接收方将收到存入代币的 [ZRC-20 版本](/developers/evm/zrc20)，例如 ZRC-20 SOL。

---

## 存入 SPL Token（Deposit SPL Tokens）

要将 SPL token 存入外部账户或通用合约，请调用 `deposit_spl_token` 指令：

```rust
pub fn deposit_spl_token(ctx: Context<DepositSplToken>, amount: u64, receiver: [u8; 20], revert_options: Option<RevertOptions>) -> Result<()>
```

仅支持 [已支持的 SPL token](/developers/evm/zrc20) 存入。  
接收方将收到存入代币的 ZRC-20 版本（例如 ZRC-20 USDC.SOL）。  
SPL token 必须先经过白名单验证，方可通过 Gateway 存入。

`amount` 参数用于指定要存入的 SPL token 数量。

---

## 存入 SOL 并调用通用应用（Deposit SOL and Call a Universal App）

要在存入 SOL 的同时调用通用应用，请使用 `deposit_and_call` 指令：

```rust
pub fn deposit_and_call(ctx: Context<Deposit>, amount: u64, receiver: [u8; 20], message: Vec<u8>, revert_options: Option<RevertOptions>) -> Result<()>
```

跨链交易处理完成后，通用应用合约中的 `onCall` 函数会被执行。

`receiver` 必须是通用应用合约的地址。  
调用通用应用时，`message` 会传递给 `onCall`。

---

## 存入 SPL Token 并调用通用应用（Deposit SPL Tokens and Call a Universal App）

可以使用 `deposit_spl_token_and_call` 指令向通用应用发送 SPL token 并进行调用：

```rust
pub fn deposit_spl_token_and_call(ctx: Context<DepositSplToken>, amount: u64, receiver: [u8; 20], message: Vec<u8>, revert_options: Option<RevertOptions>) -> Result<()>
```

`amount` 指定要存入的 SPL token 数量。  
当前协议版本中，每次仅支持存入一种 SPL token。

---

## 调用通用应用（Call a Universal App）

```rust
pub fn call(ctx: Context<Call>, receiver: [u8; 20], message: Vec<u8>, revert_options: Option<RevertOptions>) -> Result<()>
```

当只需在 ZetaChain 上执行逻辑而不涉及资产转移时，可使用该指令。

---

## 回退选项（Revert Options）

Solana Gateway 支持跨链执行失败时的回退选项。  
可在所有 Gateway 指令（`deposit`、`deposit_spl_token`、`deposit_and_call` 等）中传入可选参数 `revert_options`，以实现对失败场景的细粒度控制。

`RevertOptions` 结构体定义如下：

```rust
pub struct RevertOptions {
    pub revert_address: Pubkey,
    pub abort_address: [u8; 20],
    pub call_on_revert: bool,
    pub revert_message: Vec<u8>,
    pub on_revert_gas_limit: u64,
}
```

### 字段说明

- **revert_address**：Solana `Pubkey`，当交易在 ZetaChain 处理失败后，代币将回退至该地址。根据资产类型不同，可为 SPL token 或 SOL 账户。  
- **abort_address**：20 字节的以太坊风格地址，位于 ZetaChain。当调用通用合约的 `onCall` 函数失败且协议无法回退至 Solana 时（例如 gas 不足、回退路径错误或内部错误），代币将发送至该地址作为最终兜底。若 `call_on_revert` 为 `true`，该地址也可能通过合约的 `onRevert` 函数接收回退消息。  
- **call_on_revert**：布尔值，决定当交易失败时，是否调用 Solana 端的 `on_revert` 或 ZetaChain 端的 `onAbort`。  
- **revert_message**：传递至 `on_revert`（Solana）和 `onAbort`（ZetaChain）的自定义字节数据，可包含原始意图、失败原因或应用特定信息。  
- **on_revert_gas_limit**：ZetaChain 上为回退交易预留的 gas 限额。应确保足够执行 `onRevert` 钩子。

### 注意事项

- 如果省略 revert_options，发生回退(revert)时的默认行为是将代币转回给发送者。
- 为完全保护资产免受资金损失，我们建议始终指定 abort_address。

### 实现 `on_revert` 函数

当在 ZetaChain 上对通用合约的调用回退，且协议能够执行回退交易时，Gateway 会调用 Solana 程序中的 `on_revert` 函数。  
应用可在此函数中进行状态回滚、日志上报或用户补偿。

```rust
pub fn on_revert(
    ctx: Context<OnRevert>,
    amount: u64,      // 存入的资产数量（lamports 或 SPL）
    sender: Pubkey,   // 发起存入 / 调用的账户
    data: Vec<u8>,    // 通过 revert_message 传递的字节数据
) -> Result<()>
```

实现该函数可增强通用应用的可靠性与透明性，确保跨链失败时的安全恢复。

## 提现并调用 Solana 程序（Withdraw and Call a Solana Program）

若要从 ZetaChain 上的通用应用提现 ZRC-20 代币并调用 Solana 程序，请使用 ZetaChain Gateway 的 `withdrawAndCall` 函数。  
被调用的 Solana 程序必须实现 `on_call` 函数：

`on_call` 函数必须具有以下签名：

```rust
pub fn on_call(
    ctx: Context<OnCall>,
    amount: u64,
    sender: [u8; 20],
    data: Vec<u8>,
) -> Result<()>
```

该函数接收以下参数：

- `amount`：提现代币数量  
- `sender`：发起调用的 ZetaChain 通用应用地址  
- `data`：传入的附加数据  

程序可处理 SOL 与 SPL token 的提现。  
对于 SPL token，程序必须在上下文中包含相关的代币账户和 mint 账户。

从 ZetaChain 调用 Solana 程序时，消息负载需同时包含程序账户与传递数据，采用 ABI 编码为以下元组：

1. **账户元数据数组**：  
   每个账户包含以下字段：
   - `publicKey`：Solana 账户公钥  
   - `isWritable`：该账户是否可写  

2. **程序接收的数据字段**：  
   将传递给 `on_call` 函数。

账户数组必须包含程序执行所需的全部账户。

- 对于 **SOL 提现**，账户数组应包含：
  - 可写的 Program PDA  
  - 只读的 Gateway PDA  
  - 只读的 System program  

- 对于 **SPL token 提现**，账户数组应包含：
  - 可写的 Program PDA  
  - 可写的程序关联代币账户  
  - 只读的 mint 账户  
  - 只读的 Gateway PDA  
  - 只读的 Token program  
  - 只读的 System program  

`data` 字段可为程序 `on_call` 函数所需的任意字节数据。

完整的示例，包括消息编码与程序实现，请参考 [ZetaChain 示例仓库中的 Solana 示例](https://github.com/zeta-chain/example-contracts/tree/main/examples/call/solana)。

## 费用（Fees）

所有存入操作都会收取 2,000,000 lamports（约 0.002 SOL）作为手续费。

## 错误代码（Error Handling）

Solana Gateway 程序包含以下错误代码，用于处理不同的失败场景：

- `SignerIsNotAuthority`：签名者无权限执行此操作。  
- `DepositPaused`：当前暂停存入。  
- `NonceMismatch`：提供的 nonce 与预期不符。  
- `TSSAuthenticationFailed`：TSS 签名验证失败。  
- `DepositToAddressMismatch`：存入目标地址不匹配。  
- `MessageHashMismatch`：消息哈希验证失败。  
- `MemoLengthExceeded`：备注长度超过限制。  
- `SPLAtaAndMintAddressMismatch`：SPL token 账户与 mint 地址不匹配。  
- `EmptyReceiver`：接收地址为空。  
- `InvalidInstructionData`：指令数据无效。
