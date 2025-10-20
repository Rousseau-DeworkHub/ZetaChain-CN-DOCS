| 标题     | 描述              |
| :------- | :---------------- |
| GoldRush | 历史区块链数据API |

## 概述

GoldRush API 被设计为一个统一的接口，为开发者提供快速、可扩展的区块链历史数据访问。它解决了开发者在处理区块链数据时常见的挑战，例如：

- 运行或使用公共区块链节点的高成本和限制
- 编写自定义 SQL 查询的复杂性
- 等待数据索引完成的延迟

GoldRush 提供了一个 **RESTful API**，允许开发者以统一的请求与响应格式轻松获取数据。例如，只需更改 URL 中的网络名称，就可以查询任意地址在 200 多个支持网络中的所有代币余额。开发者只需集成一次，即可自动享受新网络支持、端点性能优化和其他更新。

## 注册 GoldRush API Key

在使用 GoldRush API 之前，你需要注册一个账户并获取 API 密钥。访问 [GoldRush 官网](https://goldrush.dev)，点击“Signup for free API Key”按钮，填写必要信息并提交申请。

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Fgoldrush-home.d611f69a.png&w=3840&q=75)

提交后，请等待一段时间。你将收到一封邀请邮件，其中包含完成注册的链接。注册完成后，你将获得一个 API Key，用于访问 GoldRush API。你可以在界面右上角复制 API Key 以备后用。

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Fgoldrush-key.48d69329.png&w=3840&q=75)

## 使用 GoldRush API

GoldRush API 提供多种数据查询接口，例如查询代币余额、交易记录、投资组合、区块信息等。除了直接发送 HTTP 请求，GoldRush API 还支持多种语言的 SDK，包括 Python、TypeScript、Go、Ruby 和 Shell。

### 初始化项目

首先，使用以下命令初始化一个 npm 项目：

```bash
mkdir zetachain-app
cd zetachain-app
npm init -y
```

安装依赖：

```bash
npm install @covalenthq/client-sdk axios
```

### 查询代币余额

我们将演示如何使用 GoldRush API 查询账户余额，分别展示通过 HTTP 请求和 TypeScript SDK 两种方式。

#### 使用 HTTP 请求

创建一个 `index.js` 文件，并添加以下代码：

```javascript
const axios = require("axios");

const apiKey = "your_api_key";
const network = "zetachain-mainnet";
const walletAddress = "your_wallet_address";
const url = `https://api.covalenthq.com/v1/${network}/address/${walletAddress}/balances_v2/`;

axios.get(url, {
  auth: {
    username: apiKey,
    password: ''
  },
  headers: {
    'Content-Type': 'application/json'
  }
})
.then((response) => {
  console.log(JSON.stringify(response.data, null, 2));
})
.catch((error) => {
  console.error('Request failed:', error);
});
```

运行代码：

```bash
node index.js
```

输出结果类似如下：

```json
{
  "data": {
    "address": "0xece40cbb54d65282c4623f141c4a8a0be7d6adec",
    "updated_at": "2024-08-28T10:17:28.671658047Z",
    "chain_name": "zetachain-mainnet",
    "items": [
      {
        "contract_name": "Zeta",
        "contract_ticker_symbol": "ZETA",
        "balance": "129029144648174752049",
        "quote_rate": 0.50380385,
        "pretty_quote": "$65.01"
      }
    ]
  },
  "error": false
}
```

#### 使用 TypeScript SDK

官方 SDK 使用起来更加方便。在 `index.js` 中添加以下内容：

```javascript
const { GoldRushClient } = require("@covalenthq/client-sdk");

const apiKey = "your_api_key";
const network = "zetachain-mainnet";
const walletAddress = "your_wallet_address";

const apiServices = async () => {
    try {
        const client = new GoldRushClient(apiKey);
        const resp = await client.BalanceService.getTokenBalancesForWalletAddress(network, walletAddress);
        console.log(resp.data);
    } catch (error) {
        console.error("An error occurred:", error);
    }
}

apiServices().catch(console.error);
```

运行：

```bash
node index.js
```

你将得到与上方类似的查询结果。

---

想要了解更多关于 GoldRush API 与 ZetaChain 集成的教程，请访问 [ZetaChain Blockchain Data Indexing API 文档](https://goldrush.dev/docs/networks/zetachain/)。
