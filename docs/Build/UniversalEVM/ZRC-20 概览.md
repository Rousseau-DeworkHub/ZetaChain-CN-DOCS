| **标题** |                           **描述**                           |
| -------- | :----------------------------------------------------------: |
| **ZETA** | ZETA 是 ZetaChain 的原生代币，用于质押    支付 Gas 费用以及治理。 |

# ZRC-20 on ZetaChain

来自连接链的原生 Gas 代币和受支持的 ERC-20 代币，在 ZetaChain 上均以 ZRC-20 的形式表示。

ZRC-20 是一种集成到 ZetaChain 全链智能合约平台的代币标准。借助 ZRC-20，开发者可以构建 dApps，以协调任意连接链上的原生资产。这使得从单一位置构建跨多链可互换代币的 Omnichain DeFi 协议 和 dApps 变得极其简单——例如 Omnichain DEXs、Omnichain Lending、Omnichain Portfolio Management，以及任何涉及多个链上可互换代币 的应用，就像它们都在一条链上一样。

## 总结

连接链的原生 Gas 代币和白名单 ERC-20 代币可以作为 ZRC-20 代币存入到 ZetaChain。

- 在存入过程中，原生/ERC-20 代币会被转移并锁定在 TSS 地址/ERC-20 托管合约中，同时 ZetaChain 上会铸造 ZRC-20 代币并存入到接收者地址。

- ZRC-20 代币可以从 ZetaChain 提取到连接链。

- 在提取过程中，ZRC-20 代币会被销毁 ，然后原生/ERC-20 代币会从 TSS 地址/ERC-20 托管合约转移到连接链上的接收者地址。

   TSS 地址是 ZetaChain 用于托管或锁定连接链上原生资产（如 ERC-20 代币或 Gas 代币）的地址。

ZRC-20 代币只能由 ZetaChain协议铸造。部署在 ZetaChain 上的 ERC-20 代币不具备 ZRC-20 的属性，因此不能从 ZetaChain 提取到连接链。

来自两条连接链的“相同” ERC-20 代币在 ZetaChain 上表示为两个不同的 ZRC-20 代币。例如，来自 Ethereum 的 USDT 被表示为来自 Ethereum 的 ZRC-20 USDT，而来自 BSC 的 USDT 则被表示为来自 BSC 的 ZRC-20 USDT。ZetaChain 不将它们视为同一资产，但它们可以被兑换。这就是如何在 ZetaChain 上实现“相同” ERC-20 资产的转移：通过存入一个 ERC-20（A 链），将此 ZRC-20（A 链）兑换到 ZRC-20（B 链），然后将 ZRC-20（B 链）作为 ERC-20 提取到 B 链。

## 支持的资产

以下是当前支持的资产列表：

 支持的主网和测试网：https://www.zetachain.com/docs/developers/evm/zrc20#supported-assets

相关资源：https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/fungible/foreign_coins

新资产可以通过向 ZetaChain 上的 `fungible` Module（系统中负责处理同质化代币逻辑的特定模块） 广播包含相应信息的交易来添加或移除。

从高层次上看，ZRC-20 代币是 Ethereum 生态系统中标准 ERC-20 代币的扩展。ZRC-20 代币增加了管理所有 ZetaChain 连接链上资产的能力。任何可互换代币，包括 Bitcoin、ETH、其他 Gas 资产以及其他链上的 ERC-20 等效代币，都可以在 ZetaChain 上以 ZRC-20 的形式表示和编排，就像它们是任何其他可互换代币（如 ERC-20）一样。

## 区块确认数

当存入或提取到 ZetaChain 时,协议要求在连接链上达到一定数量的确认数 (confirmations) 后，交易才会被视为最终确定。每个链所需的确认数不同。你可以在连接链表格中查看所需的确认数。

## 流动性上限

每个 ZRC-20 都有一个总上限 ，用于限制协议可以接受的存入代币数量。任何超出此上限的资产，如果从连接链存入到 ZetaChain，都将被退还给发送者。