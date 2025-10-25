在本教程中，您将通过添加基于 React 的前端来扩展 **Hello World 通用App**。该应用程序将连接到 EVM 测试网钱包，通过 ZetaChain 的网关发送跨链调用，并在 ZetaChain 上跟踪最终的执行结果。您将学习如何：

- 在 React 中导入并使用 ZetaChain Toolkit（`evmCall`）
- 配置网络和合约地址
- 从已连接的 EVM 链发送消息到您在 ZetaChain 上的 Hello 合约
- 轮询 ZetaChain 以获取跨链交易状态（CCTX）并显示到两个区块浏览器的链接

![](https://www.zetachain.com/docs/_next/image/?url=%2Fdocs%2F_next%2Fstatic%2Fmedia%2Ffrontend.95b49b7f.png&w=3840&q=75)

# App做的事情

Hello 前端提供了一个简单的 UI 来演示完整的跨链流程：

1. 在受支持的 EVM 测试网（例如 Arbitrum Sepolia）上连接钱包。
2. 使用 `evmCall`通过 ZetaChain Gateway 发送消息，目标是您在 ZetaChain 上部署的 Hello 合约。
3. 跟踪交易：应用程序保存源链交易哈希，轮询 ZetaChain 以获取跨链执行（CCTX），并显示到两个区块浏览器的链接。

# 预先准备

在开始之前，请确保您已完成以下教程：

- [通用App 简介](https://www.zetachain.com/docs/start/app/)
- [ZetaChain 入门](https://www.zetachain.com/docs/developers/tutorials/intro)
- [第一个通用App](https://www.zetachain.com/docs/developers/tutorials/hello)

# 配置你的环境

假设您已经拥有来自第一个 通用App 教程的 Hello 项目，只需进入 `frontend`目录并安装依赖项：

```shell
cd hello/frontend
yarn
```

如果您还没有该项目，请立即搭建它：

```shell
npx zetachain@latest new --project hello
cd hello/frontend
yarn
```

# 工作原理

前端通过导入辅助工具、连接钱包、准备调用参数和轮询跨链结果来与 ZetaChain 集成。让我们看看重要的部分。

## 导入 Toolkit

```typescript
frontend/src/MessageFlowCard.tsx
import { evmCall } from "@zetachain/toolkit/chains/evm";
import { ethers, ZeroAddress } from "ethers";
```

ZetaChain Toolkit 提供了用于发送跨链交易的 `evmCall`函数。除此之外，应用程序使用 `ethers`进行钱包和交易管理，使用 `ZeroAddress`进行 revert 配置。

## 从钱包获取 Signer

```typescript
frontend/src/MessageFlowCard.tsx
const ethersProvider = new ethers.BrowserProvider(selectedProvider.provider);
const signer = (await ethersProvider.getSigner()) as ethers.AbstractSigner;
```

应用程序通过 [EIP-6963](https://eips.ethereum.org/EIPS/eip-6963) 标准连接到钱包。需要 signer 来授权和发送跨链调用。

## 定义 Hello 合约地址

```typescript
frontend/src/constants/contracts.ts
export const HELLO_UNIVERSAL_CONTRACT_ADDRESS = "0x61a184EB30D29eD0395d1ADF38CC7d2F966c4A82";
```

将其替换为您在 ZetaChain 测试网上部署的 Hello 合约的地址。此地址将用作跨链调用的`接收者`。

## 构建调用参数

```typescript
frontend/src/MessageFlowCard.tsx
const evmCallParams = {
  receiver: helloUniversalContractAddress,
  types: ["string"],
  values: [stringValue],
  revertOptions: {
    callOnRevert: false,
    revertAddress: ZeroAddress,
    revertMessage: "",
    abortAddress: ZeroAddress,
    onRevertGasLimit: 1000000,
  },
};

const evmCallOptions = {
  signer,
  txOptions: {
    gasLimit: 1000000,
  },
};
```

在这里您定义有效负载和执行选项：

- `receiver`：ZetaChain 上的 Hello 合约。
- `types`/ `values`：传递给 `onCall`的 ABI 编码参数（在本示例中为单个字符串）。
- `revertOptions`：如何处理 revert 的可选指令。
- `txOptions`：交易设置，例如 gas 限制。

## 发送跨链调用

```typescript
frontend/src/MessageFlowCard.tsx
const result = await evmCall(evmCallParams, evmCallOptions);
await result.wait();
setConnectedChainTxHash(result.hash);
```

调用通过 Gateway 发送。`result.hash`是源 EVM 链上的交易哈希，应用程序会保存它用于区块浏览器链接和跟踪跨链状态。

## 配置网络和区块浏览器

```typescript
frontend/src/constants/chains.ts
export const SUPPORTED_CHAINS = [
  {
    explorerUrl: "https://sepolia.arbiscan.io/tx/",
    name: "Arbitrum Sepolia",
    chainId: 421614,
    icon: "/logos/arbitrum-logo.svg",
    colorHex: "#28446A",
  },
];

export const ZETACHAIN_ATHENS_BLOCKSCOUT_EXPLORER_URL = "https://zetachain-testnet.blockscout.com/tx/";
```

应用程序维护一个受支持网络及其区块浏览器 URL 的列表。发送调用后，它可以显示到源链和 ZetaChain 上相应交易的链接。

## 轮询跨链状态

```typescript
frontend/src/MessageFlowCard.tsx
const response = await fetch(`${CCTX_POLLING_URL}/${connectedChainTxHash}`);
if (response.ok) {
  const data = (await response.json()) as CrossChainTxResponse;
  const txHash = data.CrossChainTxs?.[0]?.outbound_params?.[0]?.hash;
  if (txHash) setZetachainTxHash(txHash);
}
```

应用程序使用源链交易哈希定期查询 ZetaChain 的公共 API。一旦 ZetaChain 处理了调用，响应中包含 ZetaChain 交易哈希，该哈希会显示在 UI 中。

# UI 中的端到端流程

前端引导用户完成一个简单但完整的跨链流程：

1. **连接钱包**：应用程序检测兼容 EIP-6963 的钱包并通过 `WalletProvider`连接。连接的账户用于签名和发送交易。
2. **选择网络**：用户必须从预定义的 `SUPPORTED_CHAINS`中选择一个源链。每个链都包含自己的名称、ID 和区块浏览器 URL。
3. **输入消息**：将纯文本消息输入到 UI 中。应用程序强制执行字节长度限制，以便可以安全地编码并在跨链调用中发送。
4. **发送调用**：当用户点击发送时，前端执行 `evmCall`，将 ZetaChain 上的 Hello 合约地址作为接收者传递。源链上产生的交易哈希被保存下来用于跟踪。
5. **跟踪结果**：UI 立即显示源链交易，然后开始轮询 ZetaChain 以获取跨链交易（CCTX）。一旦可用，应用程序会显示到源链和 ZetaChain 区块浏览器的链接。

# 安装并启动

从 `frontend`目录，安装依赖项并启动开发服务器：

```shell
cd hello/frontend
yarn
yarn dev
```

这将启动一个 Vite 开发服务器。默认情况下，应用程序将在 `http://localhost:5173`可用。

# 钱包

默认情况下，前端使用由 [Dynamic](https://www.dynamic.xyz/) 提供支持的 `@zetachain/wallet`，它支持 EVM、Solana、Sui 和 Bitcoin。通过一个切换开关，您可以切换到仅支持 EVM 链的 EIP-6963 钱包。

- 默认：`USE_DYNAMIC_WALLET = true`
- EIP-6963：设置 `USE_DYNAMIC_WALLET = false`

```typescript
frontend/src/constants/wallets.ts
export const USE_DYNAMIC_WALLET = true;
```

根组件根据此标志渲染，要么直接渲染，要么在 EIP-6963 provider 内部渲染：

```typescript
frontend/src/main.tsx
{
  USE_DYNAMIC_WALLET ? <App /> : (
    <Eip6963WalletProvider>
      <App />
    </Eip6963WalletProvider>
  );
}
```

两种钱包模式都为 EVM 链提供 signer 到相同的消息流，因此本教程的其余部分（发送 `evmCall`、跟踪 CCTX 和显示区块浏览器）是相同的。

## 配置合约地址（可选）

默认情况下，应用程序指向一个预设的 Hello 合约地址：

```typescript
frontend/src/constants/contracts.ts
export const HELLO_UNIVERSAL_CONTRACT_ADDRESS = "0x61a184EB30D29eD0395d1ADF38CC7d2F966c4A82";
```

如果您已经在 ZetaChain 测试网上部署了自己的 Hello 合约，请将此值替换为您部署的地址。否则，您可以使用默认地址来测试流程。

## 故障排除

- **错误的网络**：切换到受支持并已连接的 EVM 测试网。
- **无效的接收者**：确保 ZetaChain Hello 合约地址正确且已部署。
- **Toolkit/ethers 打包问题**：保持 `vite.config.ts`中的 `optimizeDeps`和 `resolve.dedupe`/`alias`设置如图所示。
- **尚未找到 CCTX**：跨链执行最终化可能需要片刻时间；应用程序每 15 秒轮询一次。

# 总结

有了这个前端，您现在拥有了 Hello World 通用App 的完整端到端流程：

- 一个部署在 ZetaChain 上的合约，用于响应跨链调用。
- 一个 React 应用程序，用于连接钱包，通过 Gateway 发送消息，并在 ZetaChain 上跟踪执行。

这个简单的示例演示了构建**通用Apps 的核心模式**：从任何连接的链接受调用，在 ZetaChain 上处理它，并通过区块浏览器向用户提供清晰的可见性。

从这里，您可以扩展应用程序以：

- 接受更丰富的有效负载（数字、地址、结构体）。
- 在您的 Universal Contract 中触发状态改变逻辑。
- 构建更高级的 UI 来管理跨链资产和操作。

ZetaChain 的 toolkit 和 API 使得将此 Hello 示例扩展到现实世界的 通用App 变得简单明了。