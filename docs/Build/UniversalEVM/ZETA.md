|标题|描述|
|:-|:-|
|ZETA|ZETA 是 ZetaChain 的原生代币，用于质押（staking）、支付 Gas 费用以及治理|

## ZetaChain 的原生代币 ZETA

ZetaChain 的原生代币称为 **ZETA**。它是一个用于 **质押（staking）** 的代币，同时也用于 **支付交易手续费**。 

ZetaChain 节点基于 **Cosmos SDK** 框架构建，而 ZETA 代币在链上以 `sdk.Coin` 的形式实现。  

ZETA 是该代币的用户友好符号，其链上单位名称（denom）为 `azeta`。

1 ZETA = 10¹⁸ azeta。

你可以使用 Cosmos 的 HTTP API [`balances` 端点](https://zetachain-athens.blockpi.network/lcd/v1/public/cosmos/bank/v1beta1/balances/zeta19nfaqu9wr0fktyyampva98ec025kjy0phww5um) 查询账户余额：

```json
{
  "balances": [
    {
      "denom": "azeta",
      "amount": "10000000000000000000"
    }
  ]
}
```

要将金额从 azeta 转换为 ZETA，只需除以 10¹⁸。

以上示例中的余额为 10 ZETA。

## ZetaChain 上的包装 ZETA（Wrapped ZETA）

ZETA 也可以以 包装代币（Wrapped Token） 的形式存在于 ZetaChain 上，
即 [WETH9](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/WZETA.sol) 标准代币。当代币（此处为 ZETA）被包装时，它会被锁定在智能合约中，并且会按 1:1 的比例铸造出等量的 包装代币（WZETA）。包装代币可随时兑换回原生代币。WZETA 与 ERC-20 标准兼容，因此可以被其他需要或支持 ERC-20 代币的 dApp 使用。WZETA 主要用于 ZetaChain 内部的流动性池中，与连接区块链的原生 Gas 代币配对（例如：sETH/WZETA 交易对）。

要将原生 ZETA 包装为 WZETA，可以将其发送到或使用 `zetaToken` 智能合约的 `deposit` 方法 [zetaChain 智能合约](https://www.zetachain.com/docs/reference/network/contracts)。

## 已连接区块链上的 ZETA
在与 ZetaChain 连接的 EVM 相容链上（如 Ethereum、Polygon 和 BSC），
ZETA 被实现为 [ERC-20](https://www.zetachain.com/docs/developers/evm/erc20) 代币。
你可以在[合约页面](https://www.zetachain.com/docs/reference/network/contracts/) 查找各连接区块链上 zetaToken 的合约地址。
