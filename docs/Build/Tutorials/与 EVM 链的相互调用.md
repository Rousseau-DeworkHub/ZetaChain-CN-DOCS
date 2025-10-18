# 与 EVM 链的相互调用

|标题|描述|
|:-|:-|
|与 EVM 链的相互调用|了解消息传递和跨链合约调用的基础知识|

在本教程中，您将学习如何在 ZetaChain 上构建一个通用应用（Universal App）。该应用能够：

- 处理来自已连接 EVM 链的传入调用
- 向已连接 EVM 链上的合约发起传出调用
- 使用回滚处理优雅地应对失败

您将部署两个合约：

- 部署在 ZetaChain 上的**通用应用**，它负责处理跨链调用并可以（可选地携带代币）回调至已连接链。
- 部署在已连接 EVM 链上的**已连接合约**（Connected Contract），它可以调用您的通用应用并接收回调。

这一模式演示了 ZetaChain 与已连接链之间双向通信的核心流程：

- 传入调用：已连接链 → ZetaChain
- 传出调用：ZetaChain → 已连接链
- 任意方向调用时可选的代币转移
- 回滚处理，以便在调用失败时从容恢复

完成本教程后，您将拥有一个最小可运行的双向合约调用示例，其中包含可选的代币转移和健壮的错误处理。

## 先决条件

在开始之前，请确保您已完成以下教程：

- [通用应用简介](/start/app/)
- [ZetaChain 入门](/developers/tutorials/intro)
- [第一个通用应用](/developers/tutorials/hello)

## 设置环境

首先，使用 `call` 模板创建一个新项目：

```bash
zetachain new --project call
cd call
```

安装依赖：

```bash
yarn
```

拉取 Solidity 依赖并编译合约：

```bash
forge soldeer update
forge build
```

现在，您的工作区已经为添加通用应用与已连接合约的逻辑做好准备。接下来，我们将逐步介绍通用应用如何处理传入调用并向已连接链发起传出调用。

## 通用应用

通用应用运行在 ZetaChain 上，并实现 `UniversalContract` 接口。它通过网关（Gateway）接收来自已连接链的调用，并可以将调用（可选携带代币）发送回去。

### 处理传入调用

当已连接链调用您的通用应用时，网关会执行 `onCall`。在这里，您需要解码消息并运行自己的业务逻辑：

```solidity
function onCall(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    bytes calldata message
) external override onlyGateway {
    string memory name = abi.decode(message, (string));
    emit HelloEvent("Hello on ZetaChain", name);
}
```

- `context` 标识源链和发送者。
- `zrc20` 是代表源链 Gas 资产或所发送代币的代币地址。
- `amount` 是交付的代币金额。
- `message` 是在源链上编码的任意 calldata。

### 发起传出调用

要从通用应用调用已连接链上的合约，首先需要授权网关使用 Gas 代币：

```solidity
IZRC20(zrc20).approve(address(gateway), gasFee);
```

随后使用 `gateway.call` 发送跨链请求：

```solidity
gateway.call(
        receiver,      // bytes：已连接链上目标合约地址
        zrc20,         // ZRC-20：目标链 Gas 代币
        message,       // calldata：目标合约所需参数
        callOptions,   // 调用类型与 Gas 限制
        revertOptions  // 回滚处理配置
);
```

### 一步完成提款并调用

若要在同一笔交易中发送代币并调用已连接链上的函数，请使用：

```solidity
gateway.withdrawAndCall(
        receiver,
        amount,
        zrc20,
        message,
        callOptions,
        revertOptions
);
```

该调用会在 ZetaChain 上销毁代币的 ZRC-20 表示，并在目标链释放对应的原生资产或 ERC-20，同时执行目标函数。

## 已连接合约

已连接合约运行在任意已连接的 EVM 链上，并通过 EVM 网关与 ZetaChain 上的通用应用交互。

调用通用应用并不一定需要已连接合约，您也可以直接在外部账户（EOA）中调用网关来触发跨链调用。本教程中的已连接合约仅作为示例，展示如何在链上工作流中以编程方式与通用应用交互。

### 调用通用应用（EVM → ZetaChain）

向 ZetaChain 上的通用应用发送任意 calldata：

```solidity
gateway.call(
        receiver,     // address：ZetaChain 上通用应用的 EVM 地址
        message,      // bytes：传递给通用应用 onCall 的 ABI 编码负载
        revertOptions // 回滚或交付失败时的处理策略
);
```

跨链交易处理完成后，目标通用应用的 `onCall` 会以提供的 calldata 执行。

### 存入代币

将原生 Gas（例如 ETH）存入 ZetaChain 上的地址或合约：

```solidity
gateway.deposit{value: msg.value}(receiver, revertOptions);
```

存入受支持的 ERC-20：

```solidity
IERC20(asset).transferFrom(msg.sender, address(this), amount);
IERC20(asset).approve(address(gateway), amount);
gateway.deposit(receiver, amount, asset, revertOptions);
```

`deposit` 只会将代币转移到 ZetaChain 上的 `receiver`（EOA 或合约），不会执行任何代码。代币将以 ZRC-20 的形式到达。

### 存入并调用

在同一笔交易中发送价值并执行 ZetaChain 上的逻辑。

原生 Gas：

```solidity
gateway.depositAndCall{value: msg.value}(
        receiver,
        message,
        revertOptions
);
```

ERC-20：

```solidity
IERC20(asset).transferFrom(msg.sender, address(this), amount);
IERC20(asset).approve(address(gateway), amount);
gateway.depositAndCall(
        receiver,
        amount,
        asset,
        message,
        revertOptions
);
```

跨链交易处理完毕后，目标通用应用的 `onCall` 会执行，并在同一次执行中接收转移的代币和提供的 calldata。

## 回滚处理

跨链调用可能因为多种原因失败：目标链 Gas 不足、目标合约缺少对应函数，或所调用的逻辑发生回滚。为优雅处理这些情况，您可以在发起调用时传入 `RevertOptions` 结构体。

若调用失败，网关会调用发起合约的 `onRevert` 函数，并传入包含失败细节的 `RevertContext`。

### 示例：通用应用的 onRevert

```solidity
function onRevert(RevertContext calldata revertContext)
        external
        onlyGateway
{
        emit RevertEvent("Revert on ZetaChain", revertContext);
}
```

您可以利用该钩子：

- 发出事件，供链下监控。
- 将代币退回给原始发送者。
- 重试调用或执行补偿性操作。

### 传递 RevertOptions

在调用或提款并调用时，通过 `RevertOptions` 指定以下配置：

- 回滚地址（接收退款的地址）。
- 是否调用 `onRevert`。
- 自定义回滚消息。
- 回滚调用的 Gas 限制。

发起传出调用时的示例：

```solidity
gateway.call(
        receiver,
        zrc20,
        message,
        callOptions,
        RevertOptions({
                revertAddress: msg.sender,
                callOnRevert: true,
                abortAddress: address(0),
                revertMessage: abi.encode("refund"),
                onRevertGasLimit: 500_000
        })
);
```

## 选项 1：部署到测试网

部署之前，您需要一个同时在 ZetaChain 测试网与目标 EVM 测试网（例如 Base Sepolia）充值的私钥，以及各链的网关地址。

```bash
GATEWAY_ZETACHAIN=0x6c533f7fe93fae114d0954697069df33c9b74fd7
GATEWAY_BASE=0x0c487a766110c85d301d96e33579c5b317fa4995

RPC_ZETACHAIN=https://zetachain-athens-evm.blockpi.network/v1/rpc/public
RPC_BASE=https://sepolia.base.org
```

### 将通用应用部署到 ZetaChain 测试网

```bash
UNIVERSAL=$(forge create Universal \
    --rpc-url $RPC_ZETACHAIN \
    --private-key $PRIVATE_KEY \
    --broadcast \
    --json \
    --constructor-args $GATEWAY_ZETACHAIN | jq -r .deployedTo) && echo $UNIVERSAL
```

### 将已连接合约部署到 Base Sepolia

```bash
CONNECTED=$(forge create Connected \
    --rpc-url $RPC_BASE \
    --private-key $PRIVATE_KEY \
    --broadcast \
    --json \
    --constructor-args $GATEWAY_BASE | jq -r .deployedTo) && echo $CONNECTED
```

### 调用通用应用

调用 Base Sepolia 上的已连接合约。它会通过网关转发请求到 ZetaChain 上的通用应用。跨链交易处理完成后，通用应用的 `onCall` 会执行。

```bash
cast send $CONNECTED \
    --rpc-url $RPC_BASE \
    --private-key $PRIVATE_KEY \
    --json \
    "call(address,bytes,(address,bool,address,bytes,uint256))" \
    $UNIVERSAL \
    $(cast abi-encode "f(string)" "hello") \
    "(0x0000000000000000000000000000000000000000,false,$UNIVERSAL,0x,0)" | jq -r '.transactionHash'
```

`call` 函数的第三个参数是 `RevertOptions` 结构体：

```text
(revertAddress, callOnRevert, abortAddress, revertMessage, onRevertGasLimit)
```

- `revertAddress`：回滚时接收退款代币的地址。对于无代币转移的 `call`，使用零地址。
- `callOnRevert`：调用失败时是否执行 `onRevert`。网关的 `call` 不支持该功能，因此必须为 `false`。
- `abortAddress`：交付失败时视为中止（abort）的地址。请使用通用合约地址，这样失败时会触发通用合约的 `onAbort`。
- `revertMessage`：回滚上下文返回的任意字节。
- `onRevertGasLimit`：为 `onRevert` 分配的 Gas。因为 `callOnRevert` 为 `false`，该值应为 `0`。

您也可以使用命令行工具运行相同的调用：

```bash
npx tsx ./commands connected call \
    --rpc $RPC_BASE \
    --contract $CONNECTED \
    --private-key $PRIVATE_KEY \
    --receiver $UNIVERSAL \
    --types string \
    --values hello \
    --name Connected
```

在测试网上广播交易后，可通过 ZetaChain CLI 跟踪全流程进度：

```bash
zetachain query cctx --hash $HASH
```

该命令会展示完整的跨链交易（CCTX）生命周期，包括当前状态、源链与目标链事件，以及在执行失败时的错误或回滚详情。这是确认跨链调用已成功交付并处理的最简单方式。

## 从通用应用发起调用

您在 ZetaChain 上的通用应用也可以向已连接 EVM 链上的合约发起传出调用。通用应用会拉取目标链 Gas ZRC-20 的费用，然后调用网关。

首先，基于目标 Gas 限制获取精确费用报价：

```bash
GAS_LIMIT=500000
ZRC20_BASE=0x236b0DE675cC8F46AE186897fCCeFe3370C9eDeD

GAS_FEE=$(cast call --json $ZRC20_BASE \
    "withdrawGasFeeWithGasLimit(uint256)(address,uint256)" \
    $GAS_LIMIT \
    --rpc-url $RPC_ZETACHAIN | jq -r '.[1]') && echo $GAS_FEE
```

授权通用应用花费该费用：

```bash
cast send $ZRC20_BASE \
    "approve(address,uint256)" \
    $UNIVERSAL \
    $GAS_FEE \
    --rpc-url $RPC_ZETACHAIN \
    --private-key $PRIVATE_KEY
```

发起跨链调用：

```bash
cast send --json \
    --rpc-url $RPC_ZETACHAIN \
    --private-key $PRIVATE_KEY \
    $UNIVERSAL \
    "call(bytes,address,bytes,(uint256,bool),(address,bool,address,bytes,uint256))" \
    $(cast abi-encode "f(bytes)" $CONNECTED) \
    $ZRC20_BASE \
    $(cast abi-encode "f(string)" "hello") \
    "($GAS_LIMIT,false)" \
    "($UNIVERSAL,false,$UNIVERSAL,0x,0)" | jq -r '.transactionHash'
```

- `$GAS_LIMIT` 是转发给目标调用的 Gas 数量，必须与 `withdrawGasFeeWithGasLimit` 中使用的值一致。
- `isArbitraryCall` 控制调用类型。经身份验证的消息使用 `false`，任意函数调用的负载使用 `true`。

`RevertOptions` 配置如下：

- `revertAddress` 使用通用合约地址，若传出调用失败，会向该合约发送回滚交易。
- `callOnRevert` 为 `true`。从 ZetaChain 发出的调用支持回滚调用，因为已连接链向 ZetaChain 的交易不会产生 Gas 费。
- `abortAddress` 同样使用通用合约地址，若调用失败且无法回滚，将由通用合约处理中止。
- `revertMessage` 此处留空，以减小负载。
- `onRevertGasLimit` 设为 `0`，因为从已连接链到 ZetaChain 的回滚调用不会产生 Gas 费。

您也可以通过命令行工具运行相同的调用：

```bash
npx tsx ./commands universal call \
    --rpc $RPC_ZETACHAIN \
    --contract $UNIVERSAL \
    --private-key $PRIVATE_KEY \
    --receiver $CONNECTED \
    --types string \
    --values hello \
    --name Universal \
    --zrc20 $ZRC20_BASE
```

## 选项 2：部署到本地网络（Localnet）

Localnet 允许您在本地机器上同时部署并测试这两个合约。它会运行一个本地 ZetaChain 实例和已连接的 EVM 链，让您无需等待测试网确认或处理水龙头即可快速迭代。

```bash
npx zetachain localnet start
```

该命令会启动带有预充值账户的 Anvil，并在本地部署 ZetaChain 核心合约。部署元数据保存在 `~/.zetachain/localnet/`。

从 localnet 注册表中提取 RPC URL、预充值私钥以及相关合约地址：

```bash
RPC=http://localhost:8545
ZRC20_ETHEREUM=$(jq -r '."11155112".chainInfo.gasZRC20' ~/.zetachain/localnet/registry.json) && echo $ZRC20_ETHEREUM
PRIVATE_KEY=$(jq -r '.private_keys[0]' ~/.zetachain/localnet/anvil.json) && echo $PRIVATE_KEY
GATEWAY_ETHEREUM=$(jq -r '."11155112".contracts[] | select(.contractType == "gateway") | .address' ~/.zetachain/localnet/registry.json) && echo $GATEWAY_ETHEREUM
GATEWAY_ZETACHAIN=$(jq -r '."31337".contracts[] | select(.contractType == "gateway") | .address' ~/.zetachain/localnet/registry.json) && echo $GATEWAY_ZETACHAIN
```

部署通用应用：

```bash
UNIVERSAL=$(forge create Universal \
    --rpc-url $RPC \
    --private-key $PRIVATE_KEY \
    --broadcast \
    --json \
    --constructor-args $GATEWAY_ZETACHAIN | jq -r .deployedTo) && echo $UNIVERSAL
```

部署已连接合约：

```bash
CONNECTED=$(forge create Connected \
    --rpc-url $RPC \
    --private-key $PRIVATE_KEY \
    --broadcast \
    --json \
    --constructor-args $GATEWAY_ETHEREUM | jq -r .deployedTo) && echo $CONNECTED
```

模拟已连接链向通用应用发送消息：

```bash
npx tsx ./commands connected call \
    --rpc $RPC \
    --contract $CONNECTED \
    --private-key $PRIVATE_KEY \
    --receiver $UNIVERSAL \
    --types string \
    --values hello \
    --name Connected
```

跨链交易在本地处理完成后，通用应用的 `onCall` 会执行。

模拟从 ZetaChain 向已连接链发送消息：

```bash
npx tsx ./commands universal call \
    --rpc $RPC \
    --contract $UNIVERSAL \
    --private-key $PRIVATE_KEY \
    --receiver $CONNECTED \
    --types string \
    --values hello \
    --name Universal \
    --zrc20 $ZRC20_ETHEREUM
```

该命令会依次执行：

1. 获取 `$ZRC20_ETHEREUM` 的目标 Gas 费报价。
2. 授权通用应用花费该费用。
3. 通过网关发送跨链调用。

## 结论

您现在已经构建并测试了一个通用应用，它演示了 ZetaChain 上双向合约通信的核心机制。通过部署通用应用（位于 ZetaChain）和已连接合约（位于已连接的 EVM 链），您学会了如何：

- 通过网关接收并处理来自已连接链的传入调用。
- 从 ZetaChain 向已连接链发起调用。
- 使用回滚处理优雅地应对失败，保持跨链逻辑的稳健性。
- 在测试网或本地网络上运行相同流程，以加快开发迭代。

该模式是构建通用 dApp 的基础，让应用不受限于单条链，而是可以从同一处协调跨多个生态的逻辑、资产与数据。

接下来，您可以：

- 增加更多已连接链，扩展应用覆盖范围。
- 扩展合约逻辑，支持交换、质押或 NFT 转移等复杂工作流。
- 将通用应用集成至更大的协议，统一不同生态中的流动性与用户体验。

借助 ZetaChain，无论连接哪条链，这些模式都以同样方式工作，让您的应用从第一天起就具备面向未来且链无关的跨链能力。

您的下一步是将这个最小示例转变为您项目的真正跨链功能，而无需再以“单链”的思维方式进行思考。
