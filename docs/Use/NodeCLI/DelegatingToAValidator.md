# 委托给验证者

# 必要条件

本教程需要安装 `zetacored` CLI。请查看有关[安装 CLI](https://www.zetachain.com/docs/users/cli/setup) 的文档。

# 委托给验证者

ZetaChain 是一个权益证明区块链网络。验证者负责生产新区块并保护网络安全。您可以将您的 ZETA 委托给验证者以参与网络并获得奖励。

您可以在 [Ping Pub](https://ping.pub/zetachain/staking) 或[任何其他浏览器](https://www.zetachain.com/docs/about/services/)上找到验证器列表。

根据验证者的佣金率、在线时间、投票权大小等因素选择您要委托的验证者。通常来说，**不**委托给拥有最多投票权的验证者是一个好主意，这有助于确保网络的去中心化。

从区块浏览器复制验证者的运营者地址。地址应以 `zetavaloper`为前缀。

接下来，检查您的[账户余额](https://www.zetachain.com/docs/users/cli/balances)并决定您想要质押的数量。

在委托之前，重要的是要了解您的 ZETA 将被锁定一段时间。在此期间您将无法转移或使用它。锁定时间的长短取决于网络参数。您可以使用以下 API 检查参数：

https://zetachain-athens.blockpi.network/lcd/v1/public/cosmos/staking/v1beta1/params

运行以下命令将您的 ZETA 委托给验证者：

```shell
zetacored tx staking delegate zetavaloper167ns6zwczl9asjs47jwv3uhtkxfjcvx3fg3d4a 1000000000000000azeta --node https://zetachain-athens.blockpi.network:443/rpc/v1/public --from alice --chain-id athens_7001-1
```

- `zetavaloper167ns6zwczl9asjs47jwv3uhtkxfjcvx3fg3d4a`是验证者运营者地址
- `1000000000000000azeta`是委托金额（在本示例中为 0.001 ZETA）
- `--node https://zetachain-athens.blockpi.network:443/rpc/v1/public`是 Tendermint RPC URL
- `--chain-id athens_7001-1`是 ZetaChain 测试网的链 ID

终端将要求您确认交易：

```shel1
auth_info:
  fee:
    amount: []
    gas_limit: "200000"
    granter: ""
    payer: ""
  signer_infos: []
  tip: null
body:
  extension_options: []
  memo: ""
  messages:
  - "@type": /cosmos.staking.v1beta1.MsgDelegate
    amount:
      amount: "1000"
      denom: azeta
    delegator_address: zeta19nfaqu9wr0fktyyampva98ec025kjy0phww5um
    validator_address: zetavaloper167ns6zwczl9asjs47jwv3uhtkxfjcvx3fg3d4a
  non_critical_extension_options: []
  timeout_height: "0"
signatures: []
confirm transaction before signing and broadcasting [y/N]:
```

输入 `y`并按 Enter 键确认。

```shell
code: 0
codespace: ""
data: ""
events: []
gas_used: "0"
gas_wanted: "0"
height: "0"
info: ""
logs: []
raw_log: '[]'
timestamp: ""
tx: null
txhash: C86E7C0E98A16CA0EB63800DF6CBB80D492201E17AB57229790DCF3403B59D02
```

交易成功。您可以再次检查余额以确认金额已被扣除。

您也可以通过交易哈希在区块浏览器上确认交易：

https://ping.pub/zetachain/tx/C86E7C0E98A16CA0EB63800DF6CBB80D492201E17AB57229790DCF3403B59D02