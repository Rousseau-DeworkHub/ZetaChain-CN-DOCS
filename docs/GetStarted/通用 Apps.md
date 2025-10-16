|标题|描述|
|:-|:-|
|通用 Apps|一类能够在 Ethereum、Bitcoin、Solana 等多条链之间自由沟通与协同执行的通用应用|

## 概述

通用应用是部署在 ZetaChain 上的智能合约，它原生连接着其他区块链，例如 Ethereum、BNB 和 Bitcoin 等 Layer1 。

与普通智能合约不同，通用应用不仅能接收来自任何连接链的合约调用、消息与代币转移，还可以向这些链发起合约调用与代币转移。这种双向可编排能力，使通用应用能够完成跨越多条链的复杂多步交易。

举例来说，一位 Bitcoin 用户可以通过通用应用，将 USDC 发送给 Ethereum 上的收款方。抑或是一位 Ethereum 用户可以在 ZetaChain 上购买 NFT，并将其转移至 BNB 链账户。

通用应用部署于 ZetaChain 的通用 EVM 上。该环境在传统 EVM 基础上扩展了**全链互操作**能力。这意味着你现有的智能合约无需重写即可直接运行在 ZetaChain 上，并且只需进行少量的修改，就可以获得强大的全链功能。

以下是一个通用应用的例子：

```solidity
pragma solidity 0.8.26;
 
import "@zetachain/protocol-contracts/contracts/zevm/interfaces/UniversalContract.sol";
 
contract UniversalApp is UniversalContract {
    function onCall(
        MessageContext calldata context,
        address zrc20,
        uint256 amount,
        bytes calldata message
    ) external virtual override {
        // ...
    }
}
```

## 调用通用应用

用户可通过连接链上的 **Gateway 合约**与通用应用交互。每条连接链都拥有一个唯一的 Gateway，负责接收用户的代币存入与调用请求。在调用通用应用时，用户可同时传递数据与代币。

举个例子，一位 Ethereum 用户向通用应用发送 1 ETH 与消息 "hello"。

<img src="../images/GetStarted/UniversalApps-1.png">

此操作将触发通用应用的 `onCall()` 方法。

在通用应用一侧所接收的内容就包括：

- 一条消息（例如 "hello"），其中可包含任意数据，比如说收款地址、代币地址、NFT 铸造属性等。

- 以 ZRC-20 形式表示的代币（在上图示例中为 1 ZRC-20 ETH）。

ZetaChain 上的每种原生 gas 代币与已支持的 ERC-20 代币，均在链上对应一种 ZRC-20 代币。ZRC-20 代币遵循 ERC-20 标准，并能够无需许可地回退至原链。例如，ZetaChain 上的 ZRC-20 ETH 可随时兑换为 Ethereum 上的原生 ETH。

此外，`onCall()` 函数还能访问更多上下文信息，比如原始发送者的地址与来源链的 chain ID。

通用应用除了以上的能力外，还可以主动发起代币转账，也能够对已连接链进行合约调用。

在如下图所示的通用应用案例中：
- 先从 Ethereum 接收 6 ETH 及消息 "I want BNB"（表示目标代币类型）；
- 然后在 ZetaChain 上通过 DEX 将 6 ZRC-20 ETH 兑换为 ZRC-20 BNB；
- 最后调用 Gateway 合约，将 ZRC-20 BNB 提现至 BNB 链，并触发目标链上的智能合约调用。

显而易见，通用应用的单次调用，可以同时触发对多条链的操作。

<img src="../images/GetStarted/UniversalApps-2.png">

借助通用应用，用户仅需一次签名交易，就可以触发一系列跨越多链的复杂交易和价值转移。

## 兼容 Bitcoin

通用应用与 Bitcoin 完全兼容。同一份通用应用合约可接收来自任意连接链的调用。

Bitcoin 用户只需向 Gateway 地址发送 BTC 与数据，并使用其钱包签署一笔交易，即可完成对通用应用的调用。由于通用应用内置 Gas 抽象机制，因此用户无需在非 Bitcoin 链上创建账户或购买 gas 代币。

## Gas 抽象机制

来自连接链的入站调用，除最初与 Gateway 合约交互外，不会产生额外 gas 成本。

而来自通用应用发起的出站调用（如跨链合约调用、代币提现），则需要支付 gas 费用。通用 EVM 提供了 gas 估算与查询工具，每个通用应用需确保自身持有足量的 ZRC-20 Gas 代币来支付费用。

在实际运行中，通用应用通常会将接收代币的一小部分兑换成目标链的 gas 代币对应的 ZRC-20，当进行跨链提现或调用时，系统会自动扣除相应的 gas 成本。

对终端用户而言，这一机制完全屏蔽了跨链 gas 的复杂性。只要用户在输入端有足量的（由用户选择的代币）作为输入，系统即会自动完成 gas 支付。

## 总结

- 通用应用：

  - 可接收来自连接链的合约调用与代币转账；

  - 可主动触发向连接链发起合约调用与代币转账；

  - 可自动处理跨链交易的 gas 成本；

  - 与 EVM 链（例如 Ethereum、BNB、Polygon）、Bitcoin、Solana 完全兼容；即将支持 TON 与 Cosmos（通过 IBC） 以及其他链；

- 所有原生 gas 与支持的 ERC-20 代币，均以 ZRC-20 代币形式存在；ZRC-20 可自由回退至原链，无需许可。