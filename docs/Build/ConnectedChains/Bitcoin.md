# Bitcoin

| 标题 | 描述 |
| :- | :- |
| Bitcoin | 调用通用应用并从比特币存入 BTC |

从 Bitcoin 调用 ZetaChain 上的通用合约（Universal Contract）是通过 **Bitcoin 网关（Bitcoin Gateway）** 实现的。  
该网关是一个基于 **阈值签名方案（Threshold Signature Scheme，TSS）** 的地址，其私钥通过 **多方计算（MPC）** 分布在 ZetaChain 的验证者集合中。

Bitcoin 网关支持以下操作：

- **存入（Deposit）**：将 BTC 发送至 ZetaChain 上的账户或智能合约。
- **调用（Call）**：使用 BTC 交易触发 ZetaChain 上的智能合约。
- **存入并调用（Deposit and Call）**：存入 BTC 的同时立即调用合约。

与 Bitcoin 网关交互的方式有两种：

| 方法 | 最大载荷 | 成本 | 回退地址 | 最适用场景 |
| ---- | -------- | ---- | -------- | ----------- |
| **Inscriptions** | 400 KB* | 较高（2 笔交易） | 可自定义 | 结构化跨链调用与自定义逻辑 |
| **OP_RETURN** | 60 字节** | 较低（1 笔交易） | 与发送方一致 | 简单的存入操作或小数据负载 |

\* 仅受 Bitcoin 交易和见证大小限制。典型载荷范围为 1–30 KB，过大载荷可能无法通过标准节点中继。  
\*\* 不包含通用合约地址所需的 20 字节。

> 📝 **推荐用法**
>
> 对于大多数调用（Call）和存入并调用（Deposit and Call）操作，推荐使用带 ABI 编码的 **inscriptions**。  
> 它支持结构化数据、复杂合约交互与自定义回退逻辑。  
> 对于简单的存入操作（尤其是目标为外部拥有账户 EOA 时），可使用 **OP_RETURN**，其成本更低且构造更简单。

## Inscription 概述 ⚡️

Inscription 允许通过在 Bitcoin 交易中嵌入结构化元数据，实现 Bitcoin 与 ZetaChain 之间的丰富交互。  
该方法使用 **commit-reveal 流程** 来将 ABI 数据和可选的回退逻辑编码进 Bitcoin 区块链。

每次交互包含两笔 Bitcoin 交易：

- **Commit**：将载荷编码为 Taproot-inscribed 输出，提交但暂不公开数据。
- **Reveal**：广播已提交的数据，包括在 ZetaChain 上执行合约的逻辑。

### 封装格式（Witness Script）

```text
OP_PUSHBYTES_32 <32-byte public key> OP_CHECKSIG
OP_FALSE
OP_IF
    OP_PUSH 0x...
    OP_PUSH 0x...
OP_ENDIF
```

### 载荷格式

Inscription 数据由一个 4 字节的 ZetaChain 头部和编码字段组成（ABI 或 Compact 编码）。

#### Header（头部）

| 字节索引 | 描述 |
| -------- | ---- |
| 0 | 固定标识符：`0x5a`（ASCII `'Z'`），代表 ZetaChain inscription |
| 1 | 编码格式（低 4 位）。例如：`0x00` = ABI，`0x01` = CompactShort，`0x02` = CompactLong |
| 2 | 操作码（高 4 位）。例如：`0x20` 表示 Call = `0x02 << 4` |
| 3 | 标志位掩码，指示设置了哪些字段。常见值：`0x07`（包含接收者 + 载荷 + 回退地址） |

#### 编码格式说明

| 格式 | 值 |
| ---- | -- |
| `EncodingFmtABI` | `0b0000` |
| `EncodingFmtCompactShort` | `0b0001` |
| `EncodingFmtCompactLong` | `0b0010` |

Compact 编码更节省空间，适合优化交易大小。  
当所有动态字段（payload 与回退地址）小于 255 字节时，使用 `CompactShort`；  
当任一字段可能超过该阈值时，使用 `CompactLong`。

#### ABI 编码

对于包含结构化输入的调用，ZetaChain 使用 Ethereum 风格的 **ABI 编码**，以保持与 Solidity 合约完全兼容。  
这允许传递复杂类型（如 address、bytes、uint256[] 等），并在客户端侧编码后嵌入 inscription 中。

- **接收者地址**：ZetaChain 上账户或通用合约的 20 字节 Ethereum 风格地址。  
- **载荷（payload）**：可选的 ABI 编码数据，用于合约的 `onCall` 处理函数。  
- **回退地址（revert address）**（可选）：跨链调用失败时用于退回资金的 Bitcoin 地址。

| 字段 | 值 |
| ---- | -- |
| Header | 4 字节 |
| ABI 数据 | `abi.encode(receiver, payload, revertAddress)` |

> 注意：ABI 编码数据必须排除 4 字节的函数选择器，仅包含参数值的打包部分。

#### Compact 编码

每个字段使用更紧凑的形式编码：

```text
[receiver (20 bytes)] + [len][payload bytes] + [len][revert address bytes]
```

- 接收者为原始 20 字节。  
- Payload 和回退地址前带长度前缀：
  - CompactShort：1 字节长度前缀（最大 255 字节）。
  - CompactLong：2 字节长度前缀（最大 65535 字节）。

| 字段 | 值 |
| ---- | -- |
| Header | 4 字节 |
| Receiver | 20 字节 |
| Payload | [长度:1 或 2] + 数据字节 |
| Revert | [长度:1 或 2] + 地址字节 |

#### 操作类型（OpCode）

| 操作 | 代码 | 描述 |
| ---- | ---- | ---- |
| `Deposit` | `0b0000` | 仅指定接收者，无载荷。可选回退地址。 |
| `DepositAndCall` | `0b0001` | 转移 BTC 并调用 `onCall()`，要求提供回退地址。 |
| `Call` | `0b0010` | 不转移 BTC，仅调用合约逻辑。回退地址可选。 |
| `Invalid` | `0b0011` | 保留字段。 |

## Inscription：Deposit

- 不包含调用数据。  
- BTC 将以 ZRC-20 BTC 形式存入 ZetaChain。  
- 适用于向 ZetaChain 上的外部账户（EOA）转账 BTC。

**示例：**

- [Commit 交易](https://mempool.space/signet/tx/eaaabfe041c0784d31a5bb8db3ff255b31ae5bd4a81f918a73e39ab3d4f3cd8c)
- [Reveal 交易](https://mempool.space/signet/tx/b1934876ab53b211fc1e3168bd0b4e2df6a5d9f3bd1be6c77a88666a7c9e926e)
- [跨链交易](https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/inboundHashToCctxData/b1934876ab53b211fc1e3168bd0b4e2df6a5d9f3bd1be6c77a88666a7c9e926e)

## Inscription：Call

- 编码数据包含：
  - 合约地址（接收者）。
  - 载荷（payload）。
- 不向合约转移 BTC，仅进行逻辑调用。  
- 适合执行不涉及 BTC 转账的通用合约逻辑。

**示例：**

- [Commit 交易](https://mempool.space/signet/tx/6c92cb80f093176b865c1431770e43c9264074d797acabbfee244f96751aac61)
- [Reveal 交易](https://mempool.space/signet/tx/cdb52721e9787c94cda196304d9f699cc89d661c9946bac32f7bdfcf17e08eaa)
- [跨链交易](https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/inboundHashToCctxData/cdb52721e9787c94cda196304d9f699cc89d661c9946bac32f7bdfcf17e08eaa)

## Inscription：Deposit and Call

- 结合前两种操作：
  - 同时转移 BTC 并调用合约函数。  
- 支持复杂交互，如「发送 BTC 并触发兑换」、「存入并铸造」等跨链复合逻辑。

**示例：**

- [Commit 交易](https://mempool.space/signet/tx/ec1d9078affd6ce20b0b57a2cdd853b9224a2a9fae9ddf759082d7a944dddab4)
- [Reveal 交易](https://mempool.space/signet/tx/0a05ed49545204d03db88daf5bfa93cc5e9177075701a4f27a3cb97d898a45)
- [跨链交易](https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/inboundHashToCctxData/0a05ed49545204d03db88daf5bfa93cc5e9177075701a4f27a3cb97d898a45)


## 何时使用 Inscriptions

在以下情况中应使用 Inscriptions：

- 载荷超过 60 字节（OP_RETURN 无法处理）。  
- 需要编码结构化 ABI 参数。  
- 需要自定义回退地址以增强安全性。  
- 需要触发逻辑而非仅转移 BTC。

## Memo（OP_RETURN）概述 💾

该方法通过标准 Bitcoin 交易实现，使用一个包含 `OP_RETURN` 输出的交易，编码接收方（通用合约或 EOA）及可选的短消息。

要从 Bitcoin 发起跨链交易，交易必须至少包含两个输出：

1. **第一个输出**：将 BTC 金额发送至 Bitcoin 网关（TSS 地址）。  
2. **第二个输出**：`OP_RETURN PUSH_x [DATA]`。

> ⚠️ 若交易未按正确顺序包含这两个输出，ZetaChain 将不会发起跨链交易。  
> BTC 仍会发送至网关地址，但不会触发智能合约调用或代币铸造。

## Memo：Deposit

将 BTC 存入 ZetaChain 上的外部账户（EOA）或通用合约：

```text
[DATA] = [EOA 或合约地址（20 字节）]
```

**示例：**

- [交易](https://blockstream.info/testnet/tx/952d60fd9efc1aad4b87a8a7a6d57a972d49e084de8b5dc524e163216c11c04f)
- [跨链交易](https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/inboundHashToCctxData/952d60fd9efc1aad4b87a8a7a6d57a972d49e084de8b5dc524e163216c11c04f)

## Memo：Call

调用 ZetaChain 上的通用合约：

```text
[DATA] = [合约地址（20 字节）] + [调用载荷（最大 60 字节）]
```

这将执行目标合约的 `onCall` 方法。

> ⚠️ 若载荷超过 60 字节，请改用 inscriptions。

## Memo：Deposit and Call

在 ZetaChain 上同时存入 BTC 并调用通用合约：

```text
[DATA] = [合约地址（20 字节）] + [调用载荷（最大 60 字节）]
```

## 手续费

与基于 EVM 的链不同，每笔存入的 Bitcoin 输出在花费时都会产生费用。  
为此，存入方与提现方共同分担这笔费用，该费用会作为**存入手续费（deposit fee）**预先收取。

Bitcoin 存入手续费的计算公式如下：

```text
depositFee = (txFee / txVsize) * 68 vB * 2
```

其中：

- `txFee = totalInputValue - totalOutputValue`
- `txVsize` 表示 Bitcoin 交易的虚拟大小。
