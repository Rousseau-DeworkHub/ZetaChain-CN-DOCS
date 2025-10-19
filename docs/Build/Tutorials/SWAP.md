| 标题 | 描述                                                         |
| :--- | :----------------------------------------------------------- |
| Swap | 实现一个兼容 Ethereum、Solana 和 Bitcoin 等链的通用兑换（swap）应用 |

# 介绍

在本教程中，你将构建一个运行在 ZetaChain 上的通用应用（Universal App），用于实现无缝的跨链代币兑换（swap）。该应用允许用户从某条连接链发送原生 Gas 代币或 ERC-20 代币，并在另一条链上于一次交易中接收不同的代币。例如，用户可以在 Ethereum 上用 USDC 兑换 Bitcoin 上的 BTC，而无需使用跨链桥或中心化交易所。

你将学习：

- 创建一个可在多链间执行代币兑换的通用应用
- 将其部署到 ZetaChain
- 从已连接的 EVM 链触发一次跨链兑换

兑换逻辑以部署在 ZetaChain 上的智能合约形式实现，并符合 `UniversalContract` 接口。这使得合约可以通过 Gateway 从任意连接链发起调用。当代币从连接链发送时，它们会以 [ZRC-20](/developers/evm/zrc20) 代币的形式到达 ZetaChain，ZRC-20 是外部资产在 ZetaChain 上的原生表示。ZRC-20 代币在启用可编程行为（包括跨链提取）的同时，保留了原资产的属性。

Swap 合约执行以下步骤：

1. 接收来自连接链的跨链调用以及随附的原生或 ERC-20 代币。
2. 解码消息载荷，以提现：
   - 目标代币（ZRC-20）的地址
   - 目标链上收件人的地址
3. 查询将目标代币发送回目标链所需的提现 Gas 费用。
4. 使用 Uniswap v2 资金池，将部分入站代币兑换为 ZRC-20 Gas 代币以覆盖提现费用。
5. 将剩余余额兑换为目标代币。
6. 将兑换后的代币提取并发送至目标链上的收件人。

这种方式允许用户从任意受支持的链上，通过一次交易发起复杂的多链操作，同时屏蔽了跨链间的流动性路由、Gas 支付以及跨链执行的复杂性。

> 注意：本教程在 ZetaChain 上使用 Uniswap v2 资金池。这些池主要用于小额兑换，例如在跨链交易回退时获取所需 Gas 费用。它们可能不具备进行大额兑换所需的流动性。在生产环境中，建议使用由活跃 DEX 维护的资金池，例如 [Beam](https://docs.beamdex.xyz/) 或 [Zuno](https://docs.zunodex.xyz/)，或任何部署在 ZetaChain 上的其他 DEX。

## 前置条件

开始之前，请确保你已完成以下教程：

- [通用应用简介](/start/app/)
- [ZetaChain 入门](/developers/tutorials/intro)
- [第一个通用应用](/developers/tutorials/hello)

## 环境配置

使用 CLI 创建一个新的 ZetaChain 项目：

```bash
zetachain new --project swap
```

安装依赖：

```bash
cd swap
yarn
```

使用 Foundry 的包管理器拉取 Solidity 依赖：

```bash
forge soldeer update
```

编译合约：

```bash
forge build
```

完成以上步骤后，你将获得一个已集成 Foundry 与 ZetaChain CLI 的工作环境，并为本地部署与测试做好准备。

## 理解 Swap 合约

`Swap` 合约是部署在 ZetaChain 上的通用应用。它允许用户通过一次跨链调用完成跨链代币兑换。代币以 ZRC-20 形式接收，可选地利用 Uniswap v2 流动性进行兑换，然后再提取至连接链。

### 通用应用入口：on_call

合约部署在 ZetaChain 上并实现 `UniversalContract`，暴露单一入口。跨链投递仅通过 Gateway 执行，因此调用面最小且可信。

```solidity
function onCall(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    bytes calldata message
) external onlyGateway
```

- `onlyGateway` 确保 `onCall` 仅由 Gateway 调用。
- `MessageContext` 携带源链信息（`context.chainID`）和原始调用者（`context.sender`）。将其视为规范的来源身份。

### 资产模型：ZRC-20

从连接链到达的资产在 ZetaChain 上以 ZRC-20 表示。在 `onCall` 中，`zrc20` 为输入代币，`amount` 为送达数量。若要将资产发送到另一条链，合约会先授权 Gateway 可支配指定数量的 ZRC-20，然后调用 `withdraw`。

两个关键接口：

用于获取目标链的提现 Gas 报价：

```solidity
(address gasZRC20, uint256 gasFee) = IZRC20(targetToken).withdrawGasFee();
```

- `gasZRC20` 是表示目标链 Gas 代币的 ZRC-20 地址。
- `gasFee` 是在目标链上执行所需的数量。

向连接链发起提现（燃烧 ZRC-20，在对侧释放原生资产）：

```solidity
IZRC20(gasZRC20).approve(address(gateway), gasFee);
IZRC20(params.target).approve(address(gateway), out);

gateway.withdraw(
  abi.encodePacked(params.to), // 与链无关的收件人地址（bytes）
  out,                         // 目标代币的数量
  params.target,               // 要提取的 ZRC-20
  revertOptions                // 失败处理
);
```

### 使用用户输入为目标链提供执行 Gas

应用会从用户的输入中预留目标链所需的 Gas，因此用户无需在目标链预先持有 Gas。

流程：

1. 通过 `withdrawGasFee()` 报价目标链的 Gas 需求。
2. 使用 DEX 报价验证输入是否覆盖：
   ```solidity
   uint256 minInput = quoteMinInput(inputToken, targetToken);
   if (amount < minInput) revert InsufficientAmount(...);
   ```
3. 如果输入代币不是 `gasZRC20`，则兑换出刚好覆盖 `gasFee` 的数量：
   ```solidity
   inputForGas = SwapHelperLib.swapTokensForExactTokens(
     uniswapRouter, inputToken, gasFee, gasZRC20, amount
   );
   ```
4. 将剩余部分兑换为目标代币：
   ```solidity
   out = SwapHelperLib.swapExactTokensForTokens(
     uniswapRouter, inputToken, amount - inputForGas, targetToken, 0
   );
   ```

`quoteMinInput()` 使用 Uniswap v2 的定价（`getAmountsIn`）来确定覆盖 Gas 费用所需的最小输入。

### 与链无关的地址

收件人（以及事件中的发送者）以原始 `bytes` 携带，而非 `address`，因此同一个合约可以同时服务 EVM、Bitcoin、Solana 等。对于跨链提取：将 `bytes` 直接传递给 `gateway.withdraw`。

### 解码消息载荷

当跨链调用到达你的通用应用时，任何额外参数都会作为 ABI 编码的载荷传入。对于本兑换合约，该载荷包含三个值：

```
(address targetToken, bytes recipient, bool withdrawFlag)
```

- `targetToken`：兑换后要发送的资产对应的 ZRC-20 代币地址。
- `recipient`：目标链的收件人地址，以原始 `bytes` 形式表示，可适配任意受支持的链（EVM、Solana 等）。
- `withdrawFlag`：控制兑换后的代币是否发送到另一条链（`true`），或在 ZetaChain 本地转账（`false`）。

在 `onCall` 内，按如下方式解码：

```solidity
(address targetToken, bytes memory recipient, bool withdrawFlag) =
    abi.decode(message, (address, bytes, bool));
```

### 使用 `RevertOptions` 与 `onRevert` 进行回退

若目标链调用或转账失败，Gateway 会携带 `RevertContext` 触发 `onRevert`。合约会在 `revertMessage` 中预编码一个简短的恢复消息（原始发送者与原始输入代币），随后按确定性流程进行退款：

```solidity
function onRevert(RevertContext calldata context) external onlyGateway {
    (bytes memory sender, address zrc20) =
        abi.decode(context.revertMessage, (bytes, address));

    (uint256 out,,) = handleGasAndSwap(
        context.asset, context.amount, zrc20, true
    );

    gateway.withdraw(
        sender, // 与链无关的退款地址
        out,
        zrc20,
        RevertOptions({
            revertAddress: address(bytes20(sender)), // 对 EVM 的尽力而为
            callOnRevert: false,
            abortAddress: address(0),
            revertMessage: "",
            onRevertGasLimit: gasLimit
        })
    );
}
```

最终实现了跨链一致的退款流程，由应用逻辑进行治理。

### 通过流动性池进行兑换

通用合约可以通过 ZetaChain 上任意 DEX/AMM 进行路由。此处以 Uniswap v2 为例，使用 SwapHelperLib 封装常见路由器调用。

```solidity
// 购买精确的目标链 Gas
SwapHelperLib.swapTokensForExactTokens(
  uniswapRouter, inputToken, gasFee, gasZRC20, amount
);

// 将余量兑换为目标代币
SwapHelperLib.swapExactTokensForTokens(
  uniswapRouter, inputToken, swapAmount, targetToken, 0
);
```

你可以将 uniswapRouter 与辅助调用替换为任意 DEX 接口或自定义路由逻辑——合约的其他部分仅假设 ZRC-20 代币流和 Gateway 的提现语义（  semantics ）。

## 选项 1：部署到测试网

将 Swap 合约部署到 ZetaChain 测试网：

```bash
UNIVERSAL=$(npx tsx commands deploy --private-key $PRIVATE_KEY | jq -r .contractAddress) && echo $UNIVERSAL
```

该命令会使用指定的私钥部署预编译合约，并输出部署地址。

部署脚本会自动使用测试网正确的 Gateway 与 Uniswap 路由器地址。

部署完成后，环境变量 `UNIVERSAL` 将保存你在测试网上部署的 Swap 合约地址。你将在从连接链触发兑换时引用该地址。

从私钥获取你的 EVM 发送者地址：

```bash
RECIPIENT=$(cast wallet address $PRIVATE_KEY) && echo $RECIPIENT
```

在 Ethereum Sepolia 上查询代表 ETH 的地址：

```bash
ZRC20_ETHEREUM_ETH=$(zetachain q tokens show --symbol sETH.SEPOLIA -f zrc20) && echo $ZRC20_ETHEREUM_ETH
```

## 从 Base 兑换到 Ethereum

发起从 Base 到 Ethereum 的兑换：

```bash
npx zetachain evm deposit-and-call   --chain-id 84532   --amount 0.001   --types address bytes bool   --receiver $UNIVERSAL   --values $ZRC20_ETHEREUM_ETH $RECIPIENT true
```

该命令会从 Base Sepolia 发送 0.001 ETH 至 ZetaChain。其内部会在 Base Gateway 上调用 `depositAndCall`。Gateway 会将入站 ETH 包装为 ZRC-20 Base ETH，并连同编码载荷一起投递给 ZetaChain 上的通用兑换合约。

合约在 ZetaChain 上以 ZRC-20 形式接收 Base ETH，使用 Uniswap v2 流动性将其兑换为 ZRC-20 Ethereum ETH，然后将兑换所得提取至你在 Ethereum Sepolia 上的地址。

整个流程以单次跨链交易完成。你无需在目标链预先准备 Gas，也无需与桥或路由器交互——一切由 ZetaChain 上的通用合约编排。

Base 上的交易：

https://sepolia.basescan.org/tx/0x8def0ff44c0e45803f209bc864123a08a03e6e1fadc5ac6f28f4c17f1463aae9

你可以通过以下命令查看完整的跨链上下文：

```
zetachain query cctx --hash 0x8def0ff44c0e45803f209bc864123a08a03e6e1fadc5ac6f28f4c17f1463aae9
```

该查询会展示从 Base 到 ZetaChain 的入站投递，以及从 ZetaChain 到 Ethereum Sepolia 的出站投递，包括交易哈希、发送者与接收者地址，以及代币数量。

```
84532 → 7001 ✅ OutboundMined
CCTX:     0x11ff9e850f0974de3b23f5347feb8684a88c6124e972da725b854031a632ad37
Tx Hash:  0x8def0ff44c0e45803f209bc864123a08a03e6e1fadc5ac6f28f4c17f1463aae9 (on chain 84532)
Tx Hash:  0xe5e5f72154140f63673d8260ed638c7dbb8c5b6901bc19b1e93651fdb35c6a00 (on chain 7001)
Sender:   0x4955a3F38ff86ae92A914445099caa8eA2B9bA32
Receiver: 0x92ae647a9D8d09D58514037d6535ab93a2A8138f
Message:  00000000000000000000000005ba149a7bd6dc1f937fa9046a9e05c05f3b18b00000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000144955a3f38ff86ae92a914445099caa8ea2b9ba32000000000000000000000000
Amount:   1000000000000000 Gas tokens

7001 → 11155111 ✅ OutboundMined
CCTX:     0xfb6f6e1cb94e646fa7a8123082054aea08fa9a65a5f07e1e0dc48463ebfaf9dd
Tx Hash:  0x11ff9e850f0974de3b23f5347feb8684a88c6124e972da725b854031a632ad37 (on chain 7001)
Tx Hash:  0x285a47661b2216ff6d76cd811ca3e3de622b6927f9da94b1cb706f88ad86ef38 (on chain 11155111)
Sender:   0x92ae647a9D8d09D58514037d6535ab93a2A8138f
Receiver: 0x4955a3F38ff86ae92A914445099caa8eA2B9bA32
Amount:   17091458311542 Gas tokens
```

## 从 Solana 兑换到 Ethereum

发起从 Solana 到 Ethereum Sepolia 的兑换：

```bash
npx zetachain solana deposit-and-call   --recipient $UNIVERSAL   --types address bytes bool   --values $ZRC20_ETHEREUM_ETH $RECIPIENT true   --chain-id 901   --private-key $SOLANA_PRIVATE_KEY   --amount 0.01
```

该命令会向 ZetaChain 上的通用兑换合约发送 0.01 SOL。Solana Gateway 会锁定原生 SOL，并将其 ZRC-20 表示与兑换载荷一同投递给合约。

合约将 ZRC-20 SOL 兑换为 ZRC-20 Ethereum ETH，并将结果提取至 Ethereum Sepolia 上的 `RECIPIENT`。接收者地址以原始 bytes 形式传递，使同一个通用合约既可服务于 EVM，也可服务于像 Solana 这样的非 EVM 链的跨链兑换。

Solana 上的交易：

https://solana.fm/tx/28xsic7NqafyxqDjmqfYL5f6RoHFYLrCKvjSA4UJCXyESmdCb1bVpW3dqT2QJrwV6KmfdWuHrwj8uW4txHZiXLxm?cluster=devnet-solana

查看完整跨链上下文：

```bash
npx zetachain query cctx --hash 28xsic7NqafyxqDjmqfYL5f6RoHFYLrCKvjSA4UJCXyESmdCb1bVpW3dqT2QJrwV6KmfdWuHrwj8uW4txHZiXLxm
```

```
901 → 7001 ✅ OutboundMined
CCTX:     0xd6e73b3ce77bc16bfaf1b8449b46991476ea7a8cec7ab1f508cd14aaf972028b
Tx Hash:  28xsic7NqafyxqDjmqfYL5f6RoHFYLrCKvjSA4UJCXyESmdCb1bVpW3dqT2QJrwV6KmfdWuHrwj8uW4txHZiXLxm (on chain 901)
Tx Hash:  0x91001d6539c04bf3629d611543ccf8f819a9f7fdf1f1c76bfd695b7e46750bbe (on chain 7001)
Sender:   AS48jKNQsDGkEdDvfwu1QpqjtqbCadrAq9nGXjFmdX3Z
Receiver: 0x92ae647a9D8d09D58514037d6535ab93a2A8138f
Message:  00000000000000000000000005ba149a7bd6dc1f937fa9046a9e05c05f3b18b00000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000144955a3f38ff86ae92a914445099caa8ea2b9ba32000000000000000000000000
Amount:   10000000 Gas tokens

7001 → 11155111 ✅ OutboundMined
CCTX:     0xc718334a07bac99c6ac21bc8a69bf743eff5c391a3998d957bd51af6240b6d07
Tx Hash:  0xd6e73b3ce77bc16bfaf1b8449b46991476ea7a8cec7ab1f508cd14aaf972028b (on chain 7001)
Tx Hash:  0x791aade1bb72cf516f9a4c6d774237f7736fbe49430aa669fb82b34b27623a85 (on chain 11155111)
Sender:   0x92ae647a9D8d09D58514037d6535ab93a2A8138f
Receiver: 0x4955a3F38ff86ae92A914445099caa8eA2B9bA32
Amount:   8645129169842 Gas tokens
```

### 从 Bitcoin 兑换到 Ethereum

你也可以从 Bitcoin 触发同样的兑换流程。以下命令会通过铭文（inscription）发送 0.05 BTC，将 BTC 的 ZRC-20 表示与编码载荷一起投递到 ZetaChain 上的通用合约，在 ZetaChain 上兑换为 ZRC-20 Ethereum ETH，并提取至你在 Ethereum Sepolia 上的地址。

在运行命令前，将 `PRIVATE_KEY_BTC` 设置为你的比特币私钥。

```bash
zetachain bitcoin inscription deposit-and-call   --private-key $PRIVATE_KEY_BTC   --receiver $UNIVERSAL   --types address bytes bool   --values $ZRC20_ETHEREUM_ETH $RECIPIENT true   --amount 0.05
```

一旦 Bitcoin 交易被观测并处理，你的合约会在一次跨链流程中完成兑换与提取。

## 选项 2：部署到 Localnet

查询 Uniswap 路由器：

```bash
UNISWAP_ROUTER=$(jq -r '.["31337"].contracts[] | select(.contractType == "uniswapRouterInstance") | .address' ~/.zetachain/localnet/registry.json) && echo $UNISWAP_ROUTER
```

查询 Gateway 地址：

```bash
GATEWAY_ZETACHAIN=$(jq -r '.["31337"].contracts[] | select(.contractType == "gateway") | .address' ~/.zetachain/localnet/registry.json) && echo $GATEWAY_ZETACHAIN
```

获取 Localnet 私钥：

```bash
PRIVATE_KEY=$(jq -r '.private_keys[0]' ~/.zetachain/localnet/anvil.json) && echo $PRIVATE_KEY
```

部署合约：

```bash
UNIVERSAL=$(npx tsx commands/index.ts deploy   --private-key $PRIVATE_KEY   --rpc http://localhost:8545   --gateway $GATEWAY_ZETACHAIN   --uniswap-router $UNISWAP_ROUTER | jq -r .contractAddress) && echo $UNIVERSAL
```

该命令会将合约部署到本地网络，并将部署地址保存到 `UNIVERSAL`。

## 从 Ethereum 兑换到 BNB

要在 Localnet 上执行从 Ethereum 到 BNB 的跨链兑换，首先设置相关变量。

获取 Ethereum 的 Gateway 合约地址：

```bash
GATEWAY_ETHEREUM=$(jq -r '.["11155112"].contracts[] | select(.contractType == "gateway") | .address' ~/.zetachain/localnet/registry.json) && echo $GATEWAY_ETHEREUM
```

获取表示 BNB Gas 代币的 ZRC-20 地址：

```bash
ZRC20_BNB=$(jq -r '."98".chainInfo.gasZRC20' ~/.zetachain/localnet/registry.json) && echo $ZRC20_BNB
```

从私钥获取本地发送者地址：

```bash
RECIPIENT=$(cast wallet address $PRIVATE_KEY) && echo $RECIPIENT
```

然后触发 swap ：

```bash
npx zetachain evm deposit-and-call   --rpc http://localhost:8545   --chain-id 11155112   --gateway $GATEWAY_ETHEREUM   --amount 0.001   --types address bytes bool   --receiver $UNIVERSAL   --private-key $PRIVATE_KEY   --values $ZRC20_BNB $RECIPIENT true
```

该流程会从 Ethereum 向 Localnet 上的 ZetaChain 发送 0.001 ETH，在 ZetaChain 上将其兑换为 ZRC-20 BNB，随后提取至 BNB 本地链上的你的地址。

## 总结

在本教程中，你学习了如何定义一个执行跨链代币兑换的通用应用合约。你将 `Swap` 合约部署到本地开发网络，并通过从已连接的 EVM 链进行兑换与合约交互。同时你也理解了在跨链兑换中处理 Gas 费用与代币授权的机制。

## 源码

你可以在示例合约仓库中找到本教程的源码：

https://github.com/zeta-chain/example-contracts/tree/main/examples/swap
