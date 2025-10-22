| 标题      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| The Graph | 了解 The Graph 如何通过subgraphs提供去中心化的索引协议，使开发者能够轻松查询智能合约的历史数据。 |

# The Graph

subgraphs、去中心化索引协议

## The Graph

在构建 dapp 时，获取智能合约的历史数据可能会令人沮丧。The Graph 提供了一种简便的方法，通过被称为subgraphs的 API来查询智能合约 数据。The Graph 的底层架构依赖于一个由许多索引人员组成的去中心化网络，正是这种结构使得您的 dapp 能够真正实现去中心化。

## 快速上手

这些subgraphs只需几分钟即可设置完成。要开始操作，请遵循以下三个步骤：

1. 初始化您的subgraph 项目
2. 部署并发布
3. 从你的dapp中查询

以下是分步演示：

### 1. 初始化您的 subgraph 项目

**在 Subgraph Studio 上创建 subgraph**

前往 [Subgraph Studio](https://thegraph.com/studio/) 并连接您的钱包。一旦您的钱包连接成功，您可以通过点击 “Create a Subgraph” 来开始。在选择名称时，建议使用首字母大写：例如 “Subgraph Name Chain Name”。

![](C:\Users\ASUS\Desktop\备份\studio-create-subgraph.png)

您随后将进入您的subgraph 页面。您需要的所有 CLI 命令 都将显示在页面右侧：

![](C:\Users\ASUS\Desktop\备份\studio-graphcli-commands.png)

**安装 The Graph CLI**

在您的电脑上运行以下命令：

```
npm install -g @graphprotocol/graph-cli
```

**初始化您的 Subgraph**

您可以直接从您的 subgraph 页面复制此命令，以包含您的特定的subgraph slug：

```
graph init --studio <SUBGRAPH_SLUG>
```

系统将提示您提供有关 subgraph 的一些信息，如下所示：

![](C:\Users\ASUS\Desktop\备份\cli-sample.png)

只需在 区块链浏览器上验证您的合约，**CLI** 就会自动获取 **ABI** 并设置您的 **subgraph**。如果获取 **ABI** 或其他信息失败，通常只需重试即可解决问题。

### 2. 部署并发布

**部署到 Subgraph Studio**

首先运行这些命令：

```
$ graph codegen
$ graph build
```

然后运行这些命令来授权和部署您的 **subgraph**。您可以直接从 Studio 中您的 **subgraph** 页面复制这些命令，以包含您的特定的 deploy key和 subgraph slug：

```
$graph auth --studio <DEPLOY_KEY>$ graph deploy --studio <SUBGRAPH_SLUG>
```

系统将要求您输入一个version labe。您可以输入类似 `v0.0.1` 的内容，但您可以自由选择格式。

**测试您的 subgraph**

您可以通过在 **playground section** 中进行 **sample 查询** 来测试您的 **subgraph**。**Details tab** 将向您显示一个 **API endpoint**。您可以使用该 **endpoint** 从您的 **dapp** 进行测试。

![](C:\Users\ASUS\Desktop\备份\studio-playground.png)

**将您的Subgraph 发布 到 The Graph 的 去中心化网络**

一旦您的 subgraph 准备好投入生产，您可以将其发布到去中心化网络。在 Subgraph Studio 中您的subgraph 页面上，点击 “Publish” 按钮：

![](C:\Users\ASUS\Desktop\备份\studio-publish-button.png)



您需要一些 Arbitrum One上的ETH来创建一个链上交易。即使您的 subgraph 正在索引的数据来自另一条区块链，The Graph的智能合约也都在 Arbitrum One 上。

![](C:\Users\ASUS\Desktop\备份\studio-publish-modal.png)

提示：发布时，会出现“Partial Indexer Support”警报，这意味着此链上的Subgraph由 The Graph 的默认索引器索引，而不是由独立索引器索引。测试网始终存在此限制。对于主网，在投票过程为链启用索引器奖励后，此警告将会消失，此时您可以将多个索引器吸引到您的Subgraph中。

### 3. 查询你的Subgraph

恭喜！您现在可以在去中心化网络上查询您的subgraph了！

对于去中心化网络 上的任何 subgraph，您可以通过将 GraphQL 查询传递到 subgraph的查询URL 来开始查询，该 查询 URL 可以在其 Explorer page 顶部找到。

以下是 Messari 提供的[CryptoPunks Ethereum subgraph](https://thegraph.com/explorer/subgraphs/HdVdERFUe8h61vm2fDyycHgxjsde5PbB832NHgJfZNqK?view=Query&chain=arbitrum-one) 的一个实例：

![](C:\Users\ASUS\Desktop\备份\explorer-query-url.png)

该 **subgraph** 的 查询 URL 是： `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/HdVdERFUe8h61vm2fDyycgxjsde5PbB832NHgJfZNqK`

现在，您只需填入您自己的 API Key 即可开始向此 **endpoint** 发送 **GraphQL queries**。

**获取您自己的 API Key**

在 **Subgraph Studio** 中，您将在页面顶部看到“API Keys” 选项。您可以在此处创建 API Keys。

![](C:\Users\ASUS\Desktop\备份\getting-api-key.png)

## 附录 

示例查询

此查询 显示了售出价格最高的 CryptoPunks。

```
{
  trades(orderBy: priceETH, orderDirection: desc) {
    priceETH
    tokenId
  }
}
```

将此内容传递给查询 URL 返回以下结果：

```
{
  "data": {
    "trades": [
      {
        "priceETH": "124457.067524886018255505",
        "tokenId": "9998"
      },
      {
        "priceETH": "8000",
        "tokenId": "5822"
      },
//      ...
```

💡 Trivia：查看 [**CryptoPunks website**](https://www.cryptopunks.app/cryptopunks/topsales) 上的最高销售额，看起来最高销售额是 **Punk #5822**，而不是 **#9998**。为什么？因为它们 **censor** 了发生的 **flash-loan sale**。

示例代码

```
const axios = require('axios');
 
const graphqlQuery = `{
  trades(orderBy: priceETH, orderDirection: desc) {
    priceETH
    tokenId
  }
}`;
const 查询Url = '[https://gateway-arbitrum.network.thegraph.com/api/](https://gateway-arbitrum.network.thegraph.com/api/)[api-key]/subgraphs/id/HdVdERFUe8h61vm2fDyycHgxjsde5PbB832NHgJfZNqK'
 
const graphQLRequest = {
  method: 'post',
  url: 查询Url,
  data: {
    查询: graphqlQuery,
  },
};
 
// Send the GraphQL 查询
axios(graphQLRequest)
  .then((response) => {
    // Handle the response here
    const data = response.data.data
    console.log(data)
 
  })
  .catch((error) => {
    // Handle any errors
    console.error(error);
  });
```

**其他资源:**

要探索优化和自定义subgraph以获得更好性能的所有方法，请在[此处](https://thegraph.com/docs/en/subgraphs/developing/creating/starting-your-subgraph/)阅读有关 creating a subgraph的更多信息。

有关从您的subgraph查询数据的更多信息，请在[此处](https://thegraph.com/docs/en/subgraphs/querying/introduction/)阅读更多信息。