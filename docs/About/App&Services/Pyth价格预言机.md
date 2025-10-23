# 概述

[Pyth 网络](https://docs.pyth.network/home)是一个价格预言机，为多种资产提供高频、低延迟的价格馈送。它与 Chainlink 具有可比性和竞争力。它专为高频交易系统和其他需要高度准确性和可靠性的应用而设计。

Pyth 已部署在 ZetaChain 上，并为多种资产提供价格馈送，包括加密货币、法币和股票。

Pyth 合约地址：

| 网络         | 地址                                                         |
| ------------ | ------------------------------------------------------------ |
| Mainnet Beta | [0x2880aB155794e7179c9eE2e38200202908C17B43](https://zetascan.com/address/0x2880aB155794e7179c9eE2e38200202908C17B43) |
| Testnet      | [0x0708325268dF9F66270F1401206434524814508b](https://zetachain-athens-3.blockscout.com/address/0x0708325268dF9F66270F1401206434524814508b) |

源地址：https://docs.pyth.network/price-feeds/core/contract-addresses/evm

Pyth Network 是一个无需许可的系统，这意味着任何人都可以向预言机提交价格。该系统使用去中心化的共识机制来确保价格的准确性和可靠性。

ZetaChain 贡献者团队运行一个 Pyth 调度程序，该程序向 Pyth 预言机提交价格。该调度程序定期更新预言机上的资产价格，确保价格馈送准确且最新。

ZetaChain 的 Pyth 调度程序作为公共服务提供给社区，以增强开发者体验并使其更容易测试 dapp。如果您正在构建生产级别的 dapp，您应该考虑运行自己的调度程序。在 Pyth 文档中了解更多信息。

当前支持的代币：BTC, BNB, MATIC, ETH, USDC, ZETA, USDT.

价格feed IDs: https://pyth.network/developers/price-feed-ids

# Pyth Entropy

[Pyth Entropy](https://docs.pyth.network/entropy) 允许开发者快速轻松地在区块链上生成安全的随机数。Entropy 的快速响应时间使开发者能够构建具有响应式 UX 的应用，例如 NFT 铸造和游戏。Entropy 还提供强大的安全保证，确保用户和应用开发者都可以信任结果是随机的。

Pyth Entropy 目前可在 Zetachain 上使用。[了解有关](https://docs.pyth.network/entropy/generate-random-numbers)如何通过熵生成随机数的更多信息。

Pyth 合约地址：

| 网络         | 地址                                                         |
| ------------ | ------------------------------------------------------------ |
| Mainnet Beta | [0x36825bf3Fbdf5a29E2d5148bfe7Dcf7B5639e320](https://zetascan.com/address/0x36825bf3Fbdf5a29E2d5148bfe7Dcf7B5639e320) |
| Testnet      | [0x4374e5a8b9C22271E9EB878A2AA31DE97DF15DAF](https://zetachain-athens-3.blockscout.com/address/0x4374e5a8b9C22271E9EB878A2AA31DE97DF15DAF) |

创建你的第一个Entropy-powered应用通过这个[示例](https://docs.pyth.network/entropy/create-your-first-entropy-app)。