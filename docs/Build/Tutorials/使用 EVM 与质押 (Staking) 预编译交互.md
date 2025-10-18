# 使用 EVM 与质押（Staking）预编译交互

|标题|描述|
|:-|:-|
|使用 EVM 与质押（Staking）预编译交互|从 EVM 中委托和撤销 ZETA|

ZetaChain 是一个使用 Cosmos SDK 构建的权益证明（Proof-of-Stake）区块链，由质押原生 ZETA 代币的验证器保护。委托人（Delegator，普通用户）可以将 ZETA 质押给验证器以参与网络安全，并获得奖励。由于 ZetaChain 也是一个 EVM 环境，智能合约可通过特殊的质押预编译（staking precompile）直接访问 Cosmos 的质押功能。这允许合约、脚本与前端使用熟悉的 EVM 工具进行委托、取消委托、领取奖励等操作。

在本教程中，我们将使用 Foundry（`cast`）与 curl 交互质押预编译。相同功能也可从 Solidity 合约或 Web 前端调用。

- 预编译地址：`0x0000000000000000000000000000000000000800`
- 文档：[质押预编译（Staking Precompile）](https://evm.cosmos.network/v0.4.x/documentation/smart-contracts/precompiles/staking)
- 接口：[StakingI.sol](https://github.com/cosmos/evm/blob/v0.4.0/precompiles/staking/StakingI.sol)

## 先决条件

- [Foundry](https://getfoundry.sh/)（包含 `cast`）
- `jq`（用于处理 JSON）
- 一个已在测试网充值 ZETA 的私钥

### 快速环境设置

```bash
export RPC_URL="https://zetachain-athens-evm.blockpi.network/v1/rpc/public"
export PRIVATE_KEY="YOUR_PRIVATE_KEY_HEX"

cast wallet address $PRIVATE_KEY
cast balance --rpc-url "$RPC_URL" $(cast wallet address $PRIVATE_KEY)

export STAKING_PRECOMPILE=0x0000000000000000000000000000000000000800
```

## 列出验证器（Listing Validators）

在委托之前，您需要知道 ZetaChain 上有哪些可用的验证器。每个验证器都有一个操作员地址（`zetavaloper...`），委托将发送到该地址。

Cosmos SDK 暴露了一个 REST API（LCD）来列出验证器。以下示例列出处于 bonded 状态（积极参与共识）的验证器：

```bash
curl -s \
  "https://zetachain-athens.blockpi.network/lcd/v1/public/cosmos/staking/v1beta1/validators?status=BOND_STATUS_BONDED&pagination.limit=1000" \
| jq -r '.validators[] | [ .operator_address, (.description.moniker) ] | @tsv'
```

示例输出：

```text
zetavaloper1qumrwnz9x2emzd5yjylp8pf9w2wh3my0gag27y    LiveRaveN
zetavaloper1p3emgemv8q0fmtw70kfzwecmcvyd9ztqlzudwn    RockX
zetavaloper1ymnrwg9e3xr9xkw42ygzjx34dyvwvtc24ct0t5    validator1-us-west-2
zetavaloper1xkddnhcdy5j4auzefjqkt3kp56t6vq7sm5xlga    BlockPI
...
```

这是获取用于质押的验证器操作员地址的最简单方法。若您更倾向在 EVM 内部获取数据，也可以从合约或前端直接调用预编译的 `validators` 函数。您还可以在 [ZetaChain 浏览器](https://testnet.zetachain.exploreme.pro/validators) 上查看验证器。

## 委托（Delegating）

委托会将您的原生 ZETA 发送给验证器，以帮助保护网络并赚取质押奖励。通过质押预编译，您可以直接使用 EVM 工具完成此操作。

- `amount` 以 wei 为单位（1 ZETA = `1e18` wei）。
- 在 `--value` 中发送相同金额，因为委托会消耗原生 ZETA。

```bash
cast send $STAKING_PRECOMPILE \
  "delegate(address,string,uint256)" \
  $(cast wallet address $PRIVATE_KEY) \
  "zetavaloper1ymnrwg9e3xr9xkw42ygzjx34dyvwvtc24ct0t5" \
  1000000000000000000 \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY
```

该交易会向该验证器绑定（bond）1 ZETA。

### 验证您的委托

可通过 `delegation` 函数查询已委托给验证者的ZETA数量。返回值为 `(uint256 shares, (string denom, uint256 amount))`。

```bash
cast call $STAKING_PRECOMPILE \
  "delegation(address,string)(uint256,(string,uint256))" \
  $(cast wallet address $PRIVATE_KEY) \
  "zetavaloper1ymnrwg9e3xr9xkw42ygzjx34dyvwvtc24ct0t5" \
  --rpc-url $RPC_URL
```

示例输出：

```text
(1000000000000000000, (azeta, 1000000000000000000))
```

- shares：您在该验证器池中的质押份额。
- balance：您委托的金额（以 wei 计，`denom` 为 `azeta`）。

## 取消委托（Undelegating）

取消委托会启动解绑期（unbonding period）：质押的 ZETA 将停止获得奖励，并在解绑期结束后才可提取。您可以部分或全部取消委托。

- `amount` 以 wei 为单位（1 ZETA = `1e18` wei）。
- 使用与委托时相同的验证器操作员地址。
- 对于此预编译调用模式，请将 `--value` 设为与 `amount` 相同。

```bash
cast send $STAKING_PRECOMPILE \
  "undelegate(address,string,uint256)" \
  $(cast wallet address $PRIVATE_KEY) \
  "zetavaloper1ymnrwg9e3xr9xkw42ygzjx34dyvwvtc24ct0t5" \
  1000000000000000000 \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY
```

该交易将提交一个从该验证器取消 1 ZETA 委托的请求。

### 验证变更

您对该验证器的激活委托应减少相应的取消委托数量：

```bash
cast call $STAKING_PRECOMPILE \
  "delegation(address,string)(uint256,(string,uint256))" \
  $(cast wallet address $PRIVATE_KEY) \
  "zetavaloper1ymnrwg9e3xr9xkw42ygzjx34dyvwvtc24ct0t5" \
  --rpc-url $RPC_URL

```

取消 1 ZETA 后的示例：

```text
(0, (azeta, 0))
```

若进行部分取消委托，则余额将低于先前值。

### 注意事项（Notes）

- 解绑期适用。取消委托的金额会被锁定，直至解绑时间结束，之后将成为您账户中的可用 ZETA。
- 您可以提交多个取消委托请求（会生成多个解绑条目）。
- 试图取消超过当前委托数量的金额将导致交易回滚（revert）。

## 结论

通过使用质押预编译，您可以在 EVM 中直接与 ZetaChain 的权益证明系统交互。无需单独的 Cosmos 工具，即可使用相同的 `cast` 命令、Solidity 合约或前端应用完成委托、取消委托与验证器数据查询。

您也可以构建通用合约，处理来自已连接链的传入调用并代表用户质押 ZETA。这为强大的跨链应用打开了大门，例如：

- 自动质押来自多条链的奖励或闲置余额的协议
- 结合跨链流动性与质押的收益策略
- 为用户提供统一界面管理委托，而无需离开其主链

质押是保护网络与赚取奖励中最基础但至关重要的功能之一。接下来，您可以探索更多高级预编译函数，例如重新委托（redelegation）、查询解绑条目与奖励分配。
