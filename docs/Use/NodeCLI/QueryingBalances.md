# 查询余额

# 必要条件

本教程需要安装 `zetacored` CLI。请查看有关[安装 CLI](https://www.zetachain.com/docs/users/cli/setup) 的文档。

# 查询余额

要查询 `alice`账户的余额，请运行以下命令：

```shell
zetacored q bank balances $(zetacored keys show alice -a) --node https://zetachain-athens.blockpi.network:443/rpc/v1/public
```

使用 `--node`标志提供有效的节点 RPC URL。你可以使用[文档](https://www.zetachain.com/docs/reference/network/api)中标记为 "Tendermint RPC" 的可用 RPC 之一。请注意，你需要在 URL 中指定端口号。如果协议方案是 `https://`，则端口为 443，除非另有说明。

```shell
balances:
- amount: "11345716912473012386685"
  denom: azeta
```

金额以 `azeta`为单位，这是最小的单位。要将其转换为 ZETA，请将其除以 10¹⁸。在上面的示例中，余额约为 11345 ZETA。