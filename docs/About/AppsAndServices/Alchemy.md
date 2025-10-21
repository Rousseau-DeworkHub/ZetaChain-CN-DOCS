# Alchemy

Alchemy 是一个区块链开发平台，提供用于构建和扩展去中心化应用程序的工具和基础设施。作为一个以开发人员为中心的平台，Alchemy 帮助公司创建可扩展且可靠的 dApp，而无需内部管理区块链基础设施的困难。它通过提供一套 API 和服务来简化开发过程，使开发人员能够有效地与区块链网络交互。

Alchemy 的一个突出产品是 Alchemy Supernode，它提供了一种可靠且可扩展的方式来连接 ZetaChain 区块链并基于其进行构建。这确保了开发人员可以专注于创新和功能，而无需担心节点管理的复杂性。

借助 Alchemy，开发人员可以访问实时区块链数据、管理智能合约并监控其 dApp 在各种区块链上的性能，使其成为构建强大、可扩展且安全的基于区块链的应用程序的通用选择。

# 注册账户

访问 https://auth.alchemy.com/signup并注册一个 Alchemy 账户或使用您现有的账户登录。

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Falchemy-0.e40a58d6.png&w=3840&q=75)

# 创建一个新的 ZetaChain 项目

在 Alchemy 仪表板中，您可以概览账户中当前设置的所有项目。

点击 "Create new app" 为您的项目命名并添加描述。

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Falchemy-1.ba33ae3d.png&w=3840&q=75)

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Falchemy-1.5.ea99218a.png&w=3840&q=75)

Alchemy 上的所有应用默认都是多链的。这意味着您的 dApp 在创建后立即可以访问所有可用的 Alchemy 网络链。您可以在 "Networks" 选项卡中查看所有可用的网络及相关 API URL。如果可用，您还可以在主网和测试网之间切换。

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Falchemy-2.d7861416.png&w=3840&q=75)

# API Key和RPC节点

与您的 Alchemy RPC 实例的交互受 API 密钥保护。您的 API 密钥会自动生成，可以从应用页面的右上角复制。

在此页面上，您还可以找到所有可用链的 RPC 端点，包括 HTTP 和 WSS。搜索 ZetaChain 网络并记下主网 URL。您稍后将使用它向 ZetaChain 发出请求。

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Falchemy-3.66d91046.png&w=3840&q=75)

# 连接到 ZetaChain

如果您是从头开始，请创建一个新目录并初始化一个 npm 项目：

```shell
mkdir zetachain-app
cd zetachain-app
npm init -y 
```

使用 npm 安装 `axios`。Axios 是一个广泛使用的 HTTP 客户端，允许您发出 API 请求。

```shell
npm install axios
```

在您的项目目录中创建一个 `index.js`文件，并将以下代码粘贴到文件中以向 ZetaChain 网络发送请求。请务必将 `YOUR_API_KEY`替换为在您的 Alchemy 应用仪表板上找到的实际 API 密钥。

```javascript
const axios = require("axios");

const url = `https://zetachain-mainnet.g.alchemy.com/v2/${YOUR_API_KEY}`;
const payload = {
  jsonrpc: "2.0",
  id: 1,
  method: "eth_blockNumber",
  params: [],
};

axios
  .post(url, payload)
  .then((response) => {
    console.log("Block Number:", parseInt(response.data.result));
  })
  .catch((error) => {
    console.error(error);
  });
```

使用 Node.js 运行脚本：

```
node index.js
```

您应该会看到 ZetaChain 上的当前区块号输出到您的控制台：

```
Block Number: 3688095
```

您可以在 [Alchemy 文档](https://www.alchemy.com/docs/node/zetachain/zeta-chain-api-endpoints/eth-block-number)中找到 ZetaChain 上可用的完整 JSON-RPC 方法列表。