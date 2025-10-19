# 文本提案

文本提案是一种提交以供审议、讨论和投票的治理行动形式。与直接修改网络操作或协议设置的升级或参数变更提案不同，文本提案不会对区块链协议产生直接影响。相反，它作为一种正式的方式，用于提出需要在实施或进一步行动之前获得社区共识的想法、指南、意图或建议。

创建提案 JSON 文件：

```json
{
  "messages": [
    {
      "@type": "/cosmos.gov.v1.MsgExecLegacyContent",
      "authority": "zeta10d07y265gmmuvt4z0w9aw880jnsr700jvxasvr",
      "content": {
        "@type": "/cosmos.gov.v1beta1.TextProposal",
        "title": "Important Proposal",
        "description": "Description of the proposal"
      }
    }
  ],
  "deposit": "1000000azeta",
  "metadata": "https://example.org/metadata.json"
}
```

提案文件包含一个消息数组、一个元数据 URL 和一个存款金额。

`messages`是要包含在提案中的消息数组。由于治理模块的 v1 版本没有专门用于文本提案的消息类型，因此 `messages`可以为空。然而，为了与某些区块浏览器兼容，我们将使用 `MsgExecLegacyContent`消息类型来包装 `/cosmos.gov.v1beta1.TextProposal`。

`authority`字段指定执行提案的实体地址。使用治理模块地址作为 `authority`。

 `content`字段包含提案的详细信息，包括标题和描述。

`deposit`指定随提案存入的代币金额。如果存款金额低于要求的最低存款金额，提案将进入存款期，并等待在最大存款期内存入所需的代币金额。在提案中提供最低存款将跳过存款期，直接进入投票期。

`metadata`：指向包含提案详细信息的 JSON 文件的 URL。

文本提案在去中心化决策过程中扮演着重要角色，为区块链网络的未来方向提出和审议提供了一种结构化和民主化的方法。