# 参数变更提案

# 概览

参数变更提案是一种治理行动，旨在提议更改网络的特定模块参数。

创建提案 JSON 文件：

```json
{
  "messages": [
    {
      "@type": "/cosmos.gov.v1.MsgExecLegacyContent",
      "authority": "zeta10d07y265gmmuvt4z0w9aw880jnsr700jvxasvr",
      "content": {
        "@type": "/cosmos.params.v1beta1.ParameterChangeProposal",
        "changes": [
          {
            "subspace": "gov",
            "key": "votingparams",
            "value": "{ \"voting_period\": \"86400000000000\" }"
          }
        ],
        "description": "Update voting period to 24 hours",
        "title": "Gov Param Change"
      }
    }
  ],
  "deposit": "1000000azeta",
  "metadata": "https://example.org/metadata.json"
}
```

上面的提案使用 `MsgExecLegacyContent`消息类型来包装 `ParameterChangeProposal`消息。

`changes`数组包含要对网络参数进行的更改列表。每个更改都是一个包含以下字段的 JSON 对象：

- `subspace`：参数被更改的模块。
- `key`：参数键。
- `value`：参数的新值。

# [subspaces and keys](https://www.zetachain.com/docs/users/cli/governance/parameter#subspaces-and-keys)

要查询参数的当前值，请使用以下端点。使用上表中的值填写 `subspace`和 `key`查询参数。

例如：http://zetachain-athens.blockpi.network/lcd/v1/public/cosmos/params/v1beta1/params?subspace=staking&key=MaxValidators

返回：

```json
{
  "param": {
    "key": "MaxValidators",
    "subspace": "staking",
    "value": "100"
  }
}
```

现在你知道 `staking`子空间中 `MaxValidators`键的值是一个整数（当前为 100）。你可以使用参数变更提案将此值更改为其他值。