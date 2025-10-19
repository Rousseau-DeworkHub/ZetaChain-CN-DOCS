# OnFinality

| 标题 | 描述 |
| :- | :- |
| OnFinality | 在 OnFinality 上托管与部署 ZetaChain 的 SubQuery/Subgraph 项目 |

## Subgraph 和 SubQuery 的索引器

[OnFinality](https://onfinality.io) 是一个区块链基础设施平台，可节省 Web3 构建者的时间，让他们的工作更轻松。OnFinality 为区块链领域最大的团队提供可扩展的 API 端点、节点和行业领先的数据索引器托管服务。

OnFinality 索引服务现在向 ZetaChain 提供我们易于使用、企业级的 SubQuery 和 Subgraph 托管服务，因此您可以高枕无忧，知道您最重要的资产——您的数据——处于安全的手中。

在本教程中，我们将运行一个新的 ZetaChain SubQuery 项目。[Subgraph 索引](https://documentation.onfinality.io/support/publishing-your-subgraph-project)的过程几乎相同，可参考上述文档。

## 准备工作

在开始之前，请确保您拥有：

- 一个可用于 ZetaChain 网络的 SubQuery 项目
- 您的项目的 GitHub 仓库或 IPFS 托管版本——在本教程中我们将使用 'QmeUwNvKGoaL211UfgEm2kbSztFCTJ2RuCXzbRRUacCaFx'
- 一个 OnFinality 索引服务账户

## 创建您的 ZetaChain 索引项目

要创建您的第一个项目，请前往 [OnFinality 索引](https://indexing.onfinality.io/) 服务。您需要使用 GitHub 账号进行身份验证才能登录。

![OnFinality](/docs/images/About/AppsAndServices/onfinality-1.webp)

首先点击“创建项目”。您将被带到新项目表单。首先选择您想要部署的项目类型 (SubQuery)，然后输入名称和描述。

![OnFinality](/docs/images/About/AppsAndServices/onfinality-2.webp)

## 部署您的项目

创建项目会设置项目的显示详情，但您必须部署一个版本才能使其运行。部署版本会触发索引操作开始，并设置所需的查询服务以开始接受 GraphQL 请求。您也可以在此处将新版本部署到现有项目。
对于您的新项目，您会看到一个“部署您的第一个版本”按钮。

![OnFinality](/docs/images/About/AppsAndServices/onfinality-3.webp)

点击此按钮，并填写有关部署的所需信息：

![OnFinality](/docs/images/About/AppsAndServices/onfinality-3.webp)

- **CID:** 提供您在“准备工作”中获取的 IPFS 部署 CID
- **Manifest:** 详细信息从所提供 CID 的内容中获取，用于确认您拥有正确的部署

![OnFinality](/docs/images/About/AppsAndServices/onfinality-4.webp)

- **Query Version:** 这是您希望运行此项目的 SubQuery 查询服务版本。建议使用最新版本
- **Advanced Settings:** 有许多高级设置，通过内置帮助功能进行了解释。
  
  ![OnFinality](/docs/images/About/AppsAndServices/onfinality-5.webp)

- **Network Endpoints:** 用于从 ZetaChain 读取数据的 RPC 端点

![OnFinality](/docs/images/About/AppsAndServices/onfinality-6.webp)

提交后，OnFinality 将开始索引您的项目。根据 ZetaChain 网络的链状态和您的查询配置，这可能需要几分钟才能完全同步。

## 连接到您的项目

一旦您的部署成功完成，并且我们的节点已从链中索引了您的数据，您将能够通过显示的 GraphQL 查询端点连接到您的项目。

![OnFinality](/docs/images/About/AppsAndServices/onfinality-7.webp)

或者，您可以点击项目标题旁边的三个点，在 SubQuery 浏览器中查看它。在那里您可以使用浏览器内的演练场开始使用。

恭喜！您现在已经具备在 ZetaChain 上创建快速、可扩展、数据丰富 dApp 的一切准备。

如果您需要帮助，请联系 <mailto:support@onfinality.io>。
