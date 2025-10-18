# 调用 Sui

| 标题 | 描述 |
| :- | :- |
| 调用 Sui | 提取资产并调用 Sui 上的合约 |

本教程演示如何在向 Sui 提取代币的同时调用一个 Sui 合约，实现无缝的跨链操作和强大的 DeFi 流程。

您将学习如何：

- 搭建包含 ZetaChain 与 Sui 的本地网络（localnet）环境
- 部署并配置一个可响应 ZetaChain 调用的 Sui 合约
- 执行 `withdrawAndCall()`，在发送代币的同时触发 Sui 上的合约逻辑

## 先决条件

开始之前，请确保已安装并配置以下工具：

- [Sui CLI](https://docs.sui.io/references/cli)：用于启动本地 Sui 节点并与其交互
- [Foundry](https://getfoundry.sh/)：用于使用 ABI 对有效负载进行编码
- [jq](https://jqlang.org/)：用于解析 Sui CLI 的 JSON 输出

## 合约概述

该示例合约演示 ZetaChain 与 Sui 之间的跨链交互。合约实现了 `connected` 模块，该模块：

- 通过 `on_call` 函数从 ZetaChain 接收代币
- 使用模拟的 Cetus DEX 实现进行代币交换
- 将交换后的代币转移至指定接收者地址

Sui 合约使用 `0x2::coin` 与自定义 `token::TOKEN` 类型表示跨链转移的资产。

## 克隆示例项目

首先创建示例项目并安装依赖：

```bash
npx zetachain@next new --project call
cd call
yarn
```

## 启动本地网络（Localnet）

启动本地开发环境，将同时拉起 ZetaChain 与 Sui 实例：

```bash
npx zetachain localnet start
```

请保持该终端窗口打开。启动后会显示包含部署详情的表格，其中包括网关（Gateway）模块与对象 ID。

## 在 Sui 上部署合约

进入 Sui 合约目录并部署合约：

```bash
cd sui
```

```bash
sui move build --force
```

从水龙头（Faucet）获取一些 SUI：

```bash
sui client faucet
```

发布合约包并记录包 ID：

```bash
PUBLISHED=$(sui client publish --skip-dependency-verification --json)
PACKAGE=$(echo $PUBLISHED | jq -r '.objectChanges[] | select(.type == "published") | .packageId') && echo $PACKAGE
```

## 设置流动性池（Pool）

部署后，通过铸造代币并创建初始流动性来设置池。

获取 treasury cap（TreasuryCap）：

```bash
TREASURY=$(echo $PUBLISHED | jq -r --arg pkg "$PACKAGE" '.objectChanges[] | select(.type == "created" and .objectType == "0x2::coin::TreasuryCap<\($pkg)::token::TOKEN>") | .objectId') && echo $TREASURY
```

获取池 ID：

```bash
POOL=$(echo $PUBLISHED | jq -r --arg pkg "$PACKAGE" '.objectChanges[] | select(.type == "created" and .objectType == "\($pkg)::cetusmock::Pool<0x2::sui::SUI, \($pkg)::token::TOKEN>") | .objectId') && echo $POOL
```

向您的地址铸造代币：

```bash
RECIPIENT=$(sui client active-address) && echo $RECIPIENT

sui client call \
  --package "$PACKAGE" \
  --module token \
  --function mint_and_transfer \
  --args "$TREASURY" 1000000 "$RECIPIENT"
```

获取代币 ID：

```bash
TOKEN=$(sui client objects --json | jq -r --arg pkg "$PACKAGE" '.[].data | select(.type == "0x2::coin::Coin<\($pkg)::token::TOKEN>") | .objectId') && echo $TOKEN
```

将代币存入池：

```bash
sui client call \
  --package "$PACKAGE" \
  --module cetusmock \
  --function deposit \
  --type-args "0x2::sui::SUI" "$PACKAGE::token::TOKEN" \
  --args "$POOL" "$TOKEN"
```

## 将 SUI 存入网关

为启用跨链操作，需要将 SUI 存入 ZetaChain 网关。首先获取您的 SUI Gas 币 ID：

```bash
COIN=$(sui client gas --json | jq -r '.[0].gasCoinId') && echo $COIN
```

准备地址（以下为示例占位符，实际值以 localnet 输出为准）：

```bash
ETH_ADDRESS=0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
GATEWAY_PACKAGE=0xa3ce10f68ed22d2cbbc31eaa709ee15e2e30348bfc6ff97b7d128d03b679c5c2
GATEWAY_OBJECT=0xe925d4059435083b70bc504ce912202214edd06f693bdc3f9573a996292780c7
```

将 SUI 存入网关：

```bash
sui client call \
  --package "$GATEWAY_PACKAGE" \
  --module gateway \
  --function deposit \
  --type-args 0x2::sui::SUI \
  --args "$GATEWAY_OBJECT" "$COIN" "$ETH_ADDRESS"
```

> 注意：请将 `GATEWAY_PACKAGE` 与 `GATEWAY_OBJECT` 替换为您本地网络输出中的值，这些地址会在启动 localnet 时显示在表格里。

## 准备提款并调用

现在可以执行提款并调用操作：从 ZetaChain 将代币提至 Sui，并同时调用 Sui 上的合约。

获取所需合约 ID：

```bash
CONFIG=$(echo $PUBLISHED | jq -r --arg pkg "$PACKAGE" '.objectChanges[] | select(.type == "created" and .objectType == "\($pkg)::cetusmock::GlobalConfig") | .objectId') && echo $CONFIG
CLOCK=$(echo $PUBLISHED | jq -r --arg pkg "$PACKAGE" '.objectChanges[] | select(.type == "created" and .objectType == "\($pkg)::cetusmock::Clock") | .objectId') && echo $CLOCK
PARTNER=$(echo $PUBLISHED | jq -r --arg pkg "$PACKAGE" '.objectChanges[] | select(.type == "created" and .objectType == "\($pkg)::cetusmock::Partner") | .objectId') && echo $PARTNER
```

准备有效负载：

```bash
MESSAGE=$RECIPIENT
TOKEN_TYPE="$PACKAGE::token::TOKEN" && echo $TOKEN_TYPE
PAYLOAD=$(npx ts-node ./setup/encodeCallArgs.ts "$TOKEN_TYPE" "$CONFIG,$POOL,$PARTNER,$CLOCK" "$MESSAGE") && echo $PAYLOAD
```

## 执行提款并调用

先批准网关使用 ZRC-20 Sui：

```bash
cast send 0xd97B1de3619ed2c6BEb3860147E30cA8A7dC9891 "approve(address,uint256)" 0x2279B7A0a67DB372996a5FaB50D91eAA73d2eBe6 1000000000000000000000000 --private-key ac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
```

执行提款并调用：

```bash
cast send 0x2279B7A0a67DB372996a5FaB50D91eAA73d2eBe6 "withdrawAndCall(bytes,uint256,address,bytes,(uint256,bool),(address,bool,address,bytes,uint256))" \
  "$PACKAGE" \
  "1000000" \
  "0xd97B1de3619ed2c6BEb3860147E30cA8A7dC9891" \
  "$PAYLOAD" \
  "(10000,false)" \
  "(0xB0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48,true,0xC0b86991c6218b36c1d19D4a2e9Eb0cE3606eB49,0xdeadbeef,50000)" \
  --private-key ac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
```

该交易将：

1. 从 ZetaChain 提取代币到 Sui。
2. 使用指定参数调用 Sui 合约。

以上流程演示了如何执行结合资产提取与合约调用的跨链操作，从而在 ZetaChain 与 Sui 之间实现更复杂的 DeFi 交互。
