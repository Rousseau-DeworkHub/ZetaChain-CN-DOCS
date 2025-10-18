| **标题**                  | **描述**                                                     |
| ------------------------- | :----------------------------------------------------------- |
| **ZRC-20 跨链费用与管理** | 了解 ZRC-20 提现、消息传递的费用机制，以及通过 Gas 限制和回退选项管理跨链交易（CCTX）成本和失败的流程。 |

# ZetaChain

从通用应用中发起调用并将代币提取到连接链

要从通用应用向连接链上的合约发起调用或提取代币，请使用 ZetaChain 网关。

ZetaChain 网关支持以下功能：

- 将 ZRC-20 代币作为原生 Gas 或 ERC-20 代币提取到连接链。
- 提取代币并向连接链上的合约发起调用。
- 调用连接链上的合约。

注意：目前不支持提取 ZETA 代币，该操作将因 ZETANotSupported() 而回退。

## 提取 ZRC-20 代币

要将 ZRC-20 代币提取到连接链上的 EOA 或合约，请使用网关合约的 `withdraw` 函数：

```
function withdraw(bytes memory receiver, uint256 amount, address zrc20, RevertOptions calldata revertOptions) external;
```

`receiver` 可以是连接链上的外部拥有账户（EOA）或合约。即使接收者是具有标准 `receive` 函数的智能合约，`withdraw` 函数也不会触发合约调用。如果你需要在提取的同时调用连接链上的合约，请改用 `withdrawAndCall` 函数。

`receiver` 的类型是 `bytes`，以适应不同链使用的各种地址格式（例如，比特币的 Bech32）。这种类型确保了接收者地址与链无关。提取到 EVM 链时，请确保将 `address` 转换为 `bytes`。

提取到非 EVM 链时，请确保将 `receiver` 地址作为字符串编码为 `bytes`，这意味着你将地址视为字符字符串并将其转换为字节。

例如，如果 Solana 上的接收者地址是：

GBwCxLUt5qn12aCD4uVKMWnoXPn2DoH126p8FrFmGNUy

那么 receiver 的 bytes 应该是：

0x47427743784c557435716e31326143443475564b4d576e6f58506e32446f4831323670384672466d474e5579

`amount` 指定了要提取的数量，而 `zrc20` 是正在被提取的 ZRC-20 代币的地址。

注意：一些连接链强制要求最小提取金额。例如，将 ZRC-20 SOL 提取到 Solana 需要至少 1,000,000（lamports）以满足租金豁免要求。

revertOptions.revertMessage 的长度不得超过 1024 字节。

你无需指定目标链，因为每个 ZRC-20 代币都与其存入（Deposit）的原始链绑定。一个 ZRC-20 代币只能提取到其原始链。例如，要将 ZRC-20 USDC.ETH 提取到 BNB 链，你必须首先将其兑换为 ZRC-20 USDC.BNB。

## 提取 ZRC-20 代币并调用连接链上的合约

要提取 ZRC-20 代币并调用连接链上的合约，请使用 `withdrawAndCall` 函数：

```
function withdrawAndCall(bytes memory receiver, uint256 amount, address zrc20, bytes calldata message, CallOptions calldata callOptions, RevertOptions calldata revertOptions) external;
```

此函数会提取代币并向由 zrc20 地址标识的连接链上的合约发起调用。例如，如果提取 ZRC-20 ETH，则该调用是向 Ethereum 上的合约发起。

message 和 revertOptions.revertMessage 的组合长度不得超过 1024 字节。

## 调用连接链上的合约

要在不提取代币的情况下调用连接链上的合约，请使用 `call` 函数：

```
function call(bytes memory receiver, address zrc20, bytes calldata message, CallOptions calldata callOptions, RevertOptions calldata revertOptions) external;
```

此处，zrc20 代表目标链的 Gas 代币的 ZRC-20 代币地址。此地址用作目标链的标识符。例如，要调用 Ethereum 上的合约，请使用 ZRC-20 ETH 代币地址。

message 和 revertOptions.revertMessage 的组合长度不得超过 1024 字节。

## 调用选项

`CallOptions` 参数指定了向连接链上的合约发起调用的详细信息。它在 `call` 和 `withdrawAndCall` 函数中均有使用：

```
struct CallOptions {
    uint256 gasLimit;
    bool isArbitraryCall;
}
```

- gasLimit: 跨链交易（Cross-chain Transaction，CCTX）合约调用可消耗的最大 Gas 量。如果 Gas 使用量超过此限制，则交易回退。
- isArbitraryCall: 确定调用是“任意”（`true`）还是“已认证”（`false`）。
  - 任意调用（Arbitrary call）调用连接链上的任何函数，但不会保留原始调用者的身份——在目标合约中，`msg.sender` 是 Gateway 地址，而不是发起调用的通用合约。这适用于代币兑换等不需要调用者身份的场景。
  - 已认证调用（Authenticated call）专门针对连接链上合约的 `onCall` 函数。通过 `onCall` 函数接收 `context.sender` 参数（引用原始通用合约）来实现认证。这允许目标合约验证并信任发起调用的通用应用，从而拒绝未经授权的调用。

## `message` 参数的格式

对于任意调用（当 `isArbitraryCall` 为 `true` 时），`withdrawAndCall` 和 `call` 函数中的 `message` 参数包含目标合约的编码函数选择器和参数：

- 函数选择器（Function Selector）：函数签名的 Keccak-256 哈希值的前 $4$ 个字节。
- 参数（Arguments）：其余的字节，根据 Ethereum 规则进行 ABI 编码。

例如：

0xa777d0dc00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000005616c696365000000000000000000000000000000000000000000000000000000

- 函数选择器：`0xa777d0dc` 对应于 `hello(string)`。
- 参数：剩余的数据表示参数 `alice`，以十六进制编码（`616c696365`）。

对于已认证调用（Authenticated call），`message` 只是 ABI 编码的参数（开头没有函数选择器，因为已认证调用被路由到一个特定的 `onCall` 函数）。

## 交易回退

当跨链交易（CCTX）失败时，ZetaChain 使用 `RevertOptions` 结构体（struct）来确定如何处理失败。行为取决于交易的方向——无论是从连接链到 ZetaChain，还是从 ZetaChain 到连接链。

### 连接链 → ZetaChain（入站）

这种情况发生在连接链上的合约使用 Gateway 上的 `depositAndCall` 或 `call` 函数向 ZetaChain 发送代币或消息时。

1. 连接链上的合约调用 Gateway 上的 `depositAndCall` 或 `call`。
2. Gateway 将调用转发给 ZetaChain 上的通用合约（Universal contract）。
3. 如果 `onCall` 函数回退，协议启动回退流程。

图像说明：https://www.figma.com/board/RQ152Ha21syhRT8iKGXz3h/Incoming--Revert?node-id=1-345&t=wcjsbVftAJscCE4M-0

回退行为：

- 如果原始调用发送的 `amount` **足以支付回退 Gas 费用**：
  - ZetaChain 将一部分 `amount` 兑换为连接链的 Gas 代币（ZRC-20）。
  - 协议将剩余代币和回退消息发送给连接链上的 `revertAddress`。
  - 如果 `callOnRevert` 为 `true`，Gateway 调用 `onRevert` 函数。
- 如果 `amount` **不足**或为零（例如，在无资产调用时），Gateway 调用 ZetaChain 上 `abortAddress` 的 `onAbort` 函数。

### ZetaChain → 连接链（出站）

这种情况发生在 ZetaChain 上的通用合约调用 Gateway 上的 withdrawAndCall 或 call 来与连接链上的合约交互时。

流程：

1. ZetaChain 上的通用合约通过 `withdrawAndCall` 或 `call` 向连接链发起调用。
2. Gateway 将消息和/或代币转发给连接链上的目标合约。
3. 如果目标合约回退，ZetaChain 启动回退流程。

图像说明：https://www.figma.com/file/4VGffjhDTeZMP3FFxxODpI?type=whiteboard&node-id=0%3A1

回退行为：

- 如果 `callOnRevert` 为 `true`：
  - Gateway 调用 ZetaChain 上 `revertAddress` 的 `onRevert` 函数。
  - 剩余的 ZRC-20 代币会随回退上下文一起传递。
  - 如果 `onRevert` 调用**本身回退**，Gateway 会将 ZRC-20 代币转移并调用 ZetaChain 上 `abortAddress` 的 `onAbort` 函数。
- 如果 `callOnRevert` 为 `false`：
  - Gateway 将代币转移到 `revertAddress`，但不调用任何函数。

`RevertOptions` 结构体指定了在跨链交易（CCTX）回退时如何处理资产。

### `RevertOptions` 结构体

```
struct RevertOptions {
    address revertAddress;
    bool callOnRevert;
    address abortAddress;
    bytes revertMessage;
    uint256 onRevertGasLimit;
}
```

- revertAddress: 接收代币或回退逻辑的地址。如果回退地址为零，回退的代币将转移给原始调用的发送者。
- callOnRevert: Gateway 是否应该调用 `onRevert`。
- abortAddress: 当 `onCall` 回退时（对于无资产调用）或回退失败时（对于资产调用）要调用的地址。
- revertMessage: 传递给 `onRevert` 和 `onAbort` 的消息。
- onRevertGasLimit: 允许 `onRevert` 的最大 Gas 限制。决定将使用多少代币。

### onRevert

```
struct RevertContext {
    address asset;
    uint64 amount;
    bytes revertMessage;
}

interface Revertable {
    function onRevert(RevertContext calldata revertContext) external;
}
```

在连接链上，asset 是最初存入的 ERC-20（对于 Gas 资产则为零地址）。

在 ZetaChain 上，asset 是原始调用期间提取的 ZRC-20。

### onAbort

```
struct AbortContext {
    bytes sender;
    address asset;
    uint256 amount;
    bool outgoing;
    uint256 chainID;
    bytes revertMessage;
}

interface Abortable {
    function onAbort(AbortContext calldata abortContext) external;
}
```

当回退执行失败时，在 ZetaChain 上作为备用处理被调用。

用于入站和出站交易。

### 总结

|      **方向**      | **触发器**                   | **回退路径**                                                 | **回退失败时的备用处理**   |
| :----------------: | ---------------------------- | ------------------------------------------------------------ | -------------------------- |
| 连接链 → ZetaChain | 通用合约中的 `onCall()` 失败 | 连接链上的 `onRevert()`（如果资金充足）                      | ZetaChain 上的 `onAbort()` |
| ZetaChain → 连接链 | 连接链上的目标合约失败       | ZetaChain 上的 `onRevert()`（如果 `callOnRevert` 为 `true`） | ZetaChain 上的 `onAbort()` |