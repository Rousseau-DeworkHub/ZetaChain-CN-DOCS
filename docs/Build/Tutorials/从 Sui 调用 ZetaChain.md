# 从 Sui 调用 ZetaChain

| 标题 | 描述 |
| :- | :- |
| 从 Sui 调用 ZetaChain | 在 Sui 中存入资产并调用通用应用 |

ZetaChain 允许基于 Sui 的应用程序与部署在 ZetaChain 上的通用智能合约直接交互。使用 ZetaChain 的通用互操作性层，Sui 应用程序可以：

- 将 SUI 和受支持的同质化代币存入 ZetaChain
- 对通用合约进行跨链调用
- 从通用合约接收跨链调用和代币转移

在本教程中，您将学习如何：

- 建立一个同时包含 ZetaChain 和 Sui 的本地开发环境
- 在 ZetaChain 上部署一个通用合约
- 从 Sui 地址将 SUI 代币存入 ZetaChain
- 发起一个跨链调用以触发通用合约上的函数

到最后，您将理解如何从 Sui（无论是通过客户端钱包还是 Sui 智能合约）向 ZetaChain 转移资产并触发逻辑。

## 先决条件

在开始之前，请确保已安装以下工具：

| 工具 | 用途 |
| --- | --- |
| [Sui CLI](https://docs.sui.io/references/cli) | 运行本地 Sui 验证器、管理地址和对象、部署合约 |
| [Foundry](https://getfoundry.sh/) | 使用 `cast` 为跨链调用编码 ABI 有效负载 |
| [Node.js](https://nodejs.org/en) | 运行 ZetaChain CLI 和基于 JavaScript 的工具 |
| [Yarn](https://yarnpkg.com/) | 安装和管理项目依赖 |
| [jq](https://jqlang.org/) | 在 shell 脚本中解析 JSON 输出 |

## 克隆示例项目

首先，使用 ZetaChain CLI 生成一个新项目：

```bash
npx zetachain@latest new --project call
cd call
```

这将设置一个包含 Sui 和 ZetaChain 合约的即用型示例。

安装依赖：

```bash
yarn
forge soldeer update
```

项目现在已准备好进行本地开发和测试。

## 启动本地网络 (Localnet)

启动一个同时运行 ZetaChain 和 Sui 的本地开发环境：

```bash
yarn zetachain localnet start --chains sui
```

此命令将启动：

- 一个本地 ZetaChain 实例
- 一个本地 Sui 验证器
- 在两个网络上预部署的网关 (gateway) 合约

让这个终端保持打开状态。启动后，您将看到如下表格：

```text
SUI
┌──────────────────┬──────────────────────────────────────────────────────────────────────────────────┐
│ (index)          │ Values                                                                           │
├──────────────────┼──────────────────────────────────────────────────────────────────────────────────┤
│ gatewayPackageId │ '0x17360c15c10bbc4ebc57e9872f2993dc4376f7f0bb78920fe5fa9ad276ac7f86'             │
│ gatewayObjectId  │ '0x9a26d6b6f413228bb120446977a8d8003eceb490cb7afd8921494815adc0a497'             │
│ userMnemonic     │ 'grape subway rack mean march bubble carry avoid muffin consider thing street'   │
│ userAddress      │ '0x2fec3fafe08d2928a6b8d9a6a77590856c458d984ae090ccbd4177ac13729e65'             │
│ tokenUSDC        │ '6b0b8d1bbc40893a7f793f52c46aeea9db9f2f710c6a623c666bff712e26c94a::token::TOKEN' │
└──────────────────┴──────────────────────────────────────────────────────────────────────────────────┘
```

> 💡 请妥善保管此输出。您将在后续步骤中引用 `gatewayPackageId`、`gatewayObjectId` 和 `userMnemonic`。

## 部署通用合约

您现在将部署一个通用智能合约到 ZetaChain。

首先，从您的本地网络设置中获取本地网关 (Gateway) 地址和一个已充值的私钥：

```bash
GATEWAY_ZETACHAIN=$(jq -r '.["31337"].contracts[] | select(.contractType == "gateway") | .address' ~/.zetachain/localnet/registry.json) && echo $GATEWAY_ZETACHAIN
```

```bash
PRIVATE_KEY=$(jq -r '.private_keys[0]' ~/.zetachain/localnet/anvil.json) && echo $PRIVATE_KEY
```

编译合约：

```bash
forge build
```

然后部署 `Universal` 合约：

```bash
UNIVERSAL=$(forge create Universal \
  --rpc-url http://localhost:8545 \
  --private-key $PRIVATE_KEY \
  --broadcast \
  --json \
  --constructor-args $GATEWAY_ZETACHAIN | jq -r .deployedTo) && echo $UNIVERSAL
```

## 存入 ZetaChain

现在您的通用合约已部署在 ZetaChain 上，您可以从 Sui 网关合约将 SUI 代币存入该合约地址。

使用以下命令将代币从 Sui 存入您在 ZetaChain 上的通用合约：

```bash
npx zetachain sui deposit \
  --mnemonic "grape subway rack mean march bubble carry avoid muffin consider thing street" \
  --receiver $UNIVERSAL \
  --gateway-package 0x17360c15c10bbc4ebc57e9872f2993dc4376f7f0bb78920fe5fa9ad276ac7f86 \
  --gateway-object 0x9a26d6b6f413228bb120446977a8d8003eceb490cb7afd8921494815adc0a497 \
  --amount 0.001 \
  --chain-id 104
```

> 🔎 请将 `--gateway-package` 和 `--gateway-object` 替换为您本地网络输出表中的值。

此命令调用 Sui 网关合约上的 `deposit` 函数。ZetaChain 观测到存款事件，并通过铸造 ZRC-20 SUI 代币并将其转移到您的通用合约，将存款传播到 ZetaChain。

## 存入并调用

在此步骤中，您将从 Sui 存入 SUI 代币，并同时触发 ZetaChain 上部署的通用合约的函数调用。

```bash
npx zetachain sui deposit-and-call \
  --mnemonic "grape subway rack mean march bubble carry avoid muffin consider thing street" \
  --receiver $UNIVERSAL \
  --gateway-package 0x17360c15c10bbc4ebc57e9872f2993dc4376f7f0bb78920fe5fa9ad276ac7f86 \
  --gateway-object 0x9a26d6b6f413228bb120446977a8d8003eceb490cb7afd8921494815adc0a497 \
  --amount 0.001 \
  --chain-id 104 \
  --types string \
  --values hello
```

此命令调用 Sui 网关合约上的 `deposit_and_call` 函数，转移指定的 SUI 金额，使用提供的 `--types` 和 `--values` 编码有效负载 (`"hello"`)，并触发部署在 ZetaChain 上的通用合约的 `onCall` 函数。

## 构建和部署 Sui 合约

为了完成整个往返流程，您还可以部署一个 Sui 合约，从链上逻辑发起对 ZetaChain 的存款。

进入 Sui 合约目录：

```bash
cd sui
```

检查 `Move.toml`：

```toml filename="sui/Move.toml"
[dependencies]
gateway = { local = "/usr/local/share/localnet/protocol-contracts-sui" }
```

这个示例项目已经从 Localnet 导入了网关 (Gateway) 模块。当使用测试网或主网时，将从公共来源导入网关。

构建 Sui 合约：

```bash
sui move build --force
```

将包发布到您的本地 Sui 实例：

```bash
SUI_CONTRACT=$(sui client publish \
  --skip-dependency-verification \
  --json 2>/dev/null | jq -r '.objectChanges[] | select(.type == "published") | .packageId') && echo $SUI_CONTRACT
```

## 从 Faucet (水龙头) 获取 Gas 币

您的 Sui 账户需要一些 SUI 代币来支付交易费用。

要从本地 Faucet 请求代币，请运行：

```bash
sui client faucet
```

这将向本地验证器发送 Faucet 请求，并为您的活动地址存入测试 SUI。

## 从 Sui 合约存入并调用

在 Sui 中，从 Move 合约调用通用合约是通过可编程交易块 (Programmable Transaction Block, PTB) 完成的。

PTB 允许您将多个操作组合成一个原子事务：您可以调用一个 Move 函数，捕获其返回值，并将该值馈送到下一个调用中（例如 Sui 网关的 `deposit_and_call`）。客户端应用（例如，Web 应用）构建并签署 PTB，将其提交给 Sui，Sui 会将该序列作为一笔交易执行。

在创建的项目中，有一个 TypeScript 命令 `commands/suiDepositAndCall.ts` 用于构建这样的 PTB。默认情况下，它会 ABI 编码一个有效负载并将其直接发送到 Sui 网关。我们将修改它以实现：

1. 首先调用我们的 Sui 合约，并获取其返回值。
2. 将该返回值作为有效负载传递给 Sui 网关。

打开 `commands/suiDepositAndCall.ts` 并替换有效负载的构建逻辑：

```ts filename="commands/suiDepositAndCall.ts"
// const payload = tx.pure.vector("u8", utils.arrayify(payloadABI));

const payload = tx.moveCall({
  target: `${options.connected}::connected::hello`,
  arguments: [tx.pure.string(params.values[0] as string)],
});
```

这将使用提供的第一个值（在本例中为字符串）调用您的 Sui 模块函数 `connected::hello`。从 Move 调用返回的值将成为 `payload` 参数，然后在同一个 PTB 中转发给 Sui 网关的 `deposit_and_call`。

因为 Sui 合约不能轻易地为 EVM 进行 ABI 编码，我们将更新通用 Solidity 合约以接受 `bytes` 类型的原始消息有效负载。

更新通用合约的 `onCall` 签名和逻辑，以接受 `bytes` 并将其解释为 UTF-8 字符串：

```solidity
function onCall(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    bytes calldata message
) external override onlyGateway {
    // string memory name = abi.decode(message, (string));
    emit HelloEvent("Hello on ZetaChain", string(message));
}
```

在您的本地 ZetaChain 上重新构建并部署合约：

```bash
forge build
```

```bash
UNIVERSAL=$(forge create Universal \
  --rpc-url http://localhost:8545 \
  --private-key $PRIVATE_KEY \
  --broadcast \
  --json \
  --constructor-args $GATEWAY_ZETACHAIN | jq -r .deployedTo) && echo $UNIVERSAL
```

现在执行 PTB，它将调用您的 Sui 合约，获取其返回值，并将其传递给 Sui 网关，后者接着调用您在 ZetaChain 上的通用合约：

```bash
npx tsx commands deposit-and-call \
  --private-key suiprivkey1qrqtrevmd40vxlv3q6fcgmm09af5p8f8j67ezve0u3nhrs0psslgjnw3y5p \
  --receiver $UNIVERSAL \
  --gateway-package 0xc52d19fd2f0bcb94d0c285d480b6a8af515f5ec19d0cff8818fc9bf0d3731b85 \
  --gateway-object 0xa755a1106ae7039a25c10578b6f3c5b73963055e0d6fc40e8abcebea454a6389 \
  --amount 0.001 \
  --chain-id 104 \
  --types string \
  --values alice \
  --connected $SUI_CONTRACT
```

您应该在终端中看到类似以下的事件日志：

```text
[ZetaChain] Event from onCall: {"_type":"log","address":"0xa6e99A4ED7498b3cdDCBB61a6A607a4925Faa1B7","blockHash":"0x694028003ddc35ab9da2a18c262f8df88f882f3a4c3db8d9935b6346ed9f9b7f","blockNumber":192,"data":"0x00000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000001248656c6c6f206f6e205a657461436861696e0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000b68656c6c6f20616c696365000000000000000000000000000000000000000000","index":2,"removed":false,"topics":["0x39f8c79736fed93bca390bb3d6ff7da07482edb61cd7dafcfba496821d6ab7a3"],"transactionHash":"0x82e7ed404b1c3bfb06677174b74d54d1bb5b1b6248433ead6bd48c0cda519777","transactionIndex":0}
```

要检查它，您可以解码日志数据：

```bash
cast abi-decode "data()(string,string)" \
  0x00000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000001248656c6c6f206f6e205a657461436861696e0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000b68656c6c6f20616c696365000000000000000000000000000000000000000000
```

预期输出：

```text
"Hello on ZetaChain"
"hello alice"
```
