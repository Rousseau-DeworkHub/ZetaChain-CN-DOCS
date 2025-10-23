# 概览

Particle Network 提供一套全面的工具和服务，旨在增强 ZetaChain 上 去中心化应用的用户体验。Particle Network 的堆栈原生支持 ERC-4337 账户抽象，使开发者能够从初始用户引导到最终构建和赞助用户操作实现智能账户。

Particle Network 提供钱包即服务（WaaS），作为基于扩展的钱包的替代方案，允许用户使用类似于传统 Web 应用程序的机制（例如 social login 和邮箱/密码）创建 non-custodial accounts。WaaS 嵌入到 Web 应用程序中，因此用户无需安装任何额外软件即可与 dApps 交互。

- [Wallet as a Service](https://particlenetwork.readme.io/docs/understanding-wallet-as-a-service)：WaaS 允许用户使用 social login 或 email/password 登录 dApp。在“经典” Wallet-as-a-Service 中，Externally-Owned-Account 是登录后的终点。或者使用抽象账户，此 EOA 被用作中介，而是为用户分配一个智能账户用于交互。
- Account abstraction 
  - [Bundler](https://particlenetwork.readme.io/docs/bundler)：作为 AA 堆栈的一部分，Particle Network 提供了一个开源的 Bundler，所有 `userOperations`都在其中构建和发送。
  - [Paymaster](https://particlenetwork.readme.io/docs/paymaster)：与 Bundler 一起，Particle Network 还提供了一个 paymaster，用于 multi-chain gas sponsorship。

Particle Network 的堆栈是模块化的，因此开发者可以仅选择使用他们需要的组件。

# 下一步

要了解更多关于如何使用 Particle Network WaaS 在 ZetaChain 上构建 dApps 的信息，请查看关于将钱包集成到基于React Web 应用程序的全面教程：https://particlenetwork.readme.io/docs/leveraging-particle-network-on-zetachain