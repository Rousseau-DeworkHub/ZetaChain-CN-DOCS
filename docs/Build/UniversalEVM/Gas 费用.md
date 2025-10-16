|标题|描述|
|:-|:-|
|Gas 费|了解更多关于 ZRC-20 的提现费用和消息传递费用|

# Gas 费

## 调用通用应用

当你通过 Gateway 从外部连接链与 ZetaChain 上的通用应用进行交互时，所支付的手续费以源链的原生 Gas 代币计价，与普通链上交易相同。这意味着无需任何额外费用，从连接链发起的通用应用调用，在 ZetaChain 上的执行操作几乎可以视作免 Gas。

举个例子，当你从 Ethereum 存入 ETH 至 ZetaChain 时，所需费用将以 ETH 支付，与 Ethereum 网络的常规 Gas 费结构一致。如需了解 Ethereum Gas 的更多细节，请参考其[官方文档](https://ethereum.org/en/developers/docs/gas/)。

若直接在 ZetaChain 的 EVM 上调用合约（即非跨链调用），则用户需像在以太坊上那样，为每笔交易提供 Gas 费。ZetaChain 的 EVM 采用由 [Cosmos EVM](https://evm.cosmos.network/protocol/concepts/gas-and-fees) 实现的 Gas 市场机制，并遵循 EIP-1559 的费用模型，以维护网络安全并防止垃圾交易。

## 外部调用与提取

ZetaChain 上的通用应用不仅可以主动调用外部链上的智能合约，还可发起 ZRC-20 代币的跨链提取。这类操作需要支付提取所需的 Gas 费，该费用根据目标链的 Gas Limit 进行计算。

在从通用应用调用外部链上的合约前，可以先查询提取所需的 Gas 费：

```solidity
(address gasZRC20, uint256 gasFee) = IZRC20(zrc20).withdrawGasFeeWithGasLimit(gasLimit);
```

- `gasZRC20` 表示目标链的 Gas 代币地址。例如，对于 Ethereum USDC 与 ETH，其 Gas 代币均为 ZRC-20 ETH。
- `gasFee` 表示指定 Gas Limit 所需的费用，用于确保你能准确估算执行所需的成本。

若要提取 ZRC-20 代币至连接链，可直接查询提取所需的 Gas 费：

```solidity
(address gasZRC20, uint256 gasFee) = IZRC20(zrc20).withdrawGasFee();
```

ZRC-20 代币的跨链提取仅涉及代币转移，无需显式指定 Gas 上限。

有个非常重要的提示，在执行提取前，请务必查询当前提取 Gas 费，授权 Gateway 消耗所需的额度，最后确保充当 Gas 的 ZRC-20 代币余额充足。若 Gateway 无法从用户账户中转移足额 Gas 费，操作将失败。

## 当前 Gas 费（Current Fees）

下表展示了基于默认 `Gas Limit = 500,000` 的当前提取费用。所有费用均以目标链的原生 Gas 代币计价。详见[当前 Gas 费用](http://zetachain.com/docs/developers/evm/gas#current-fees)。

若你需要计算不同 Gas Limit 下的费用，可使用以下命令：

```
npx zetachain query fees
```