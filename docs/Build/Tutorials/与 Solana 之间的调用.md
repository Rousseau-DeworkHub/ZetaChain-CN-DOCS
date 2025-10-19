# 与 Solana 之间的调用

从 Solana 存入资产并调用通用应用，向 Solana 发起出站调用

阅读大约需要 60 分钟

使用 ZetaChain 和 Solana 构建通用应用程序非常简单。您可以直接从 Solana 将 SOL 和 SPL-20 代币存入 ZetaChain 上的账户或智能合约。ZetaChain 上的通用合约可以处理这些存款，并执行从 Solana 区块链发起的合约调用。

在本教程中，您将：
- 使用 localnet 设置本地开发环境
- 在 ZetaChain 上部署通用合约
- 从 Solana 向 ZetaChain 存入代币（SOL 和 SPL-20）
- 执行存款并调用交易，同时存入代币并调用通用应用程序
- 将代币提现回 Solana，可选择在提现过程中调用 Solana 程序

与 Solana 的通用应用程序交互由 Solana Gateway 程序处理，更多相关信息请在[文档中了解](https://www.zetachain.com/docs/developers/chains/solana)。

## 前置条件

开始前，请确保已安装并配置以下工具：

- `solana` CLI

## 克隆示例项目

首先创建项目并安装必要的依赖：

```bash
npx zetachain@latest new --project call
cd call
yarn
```

## 启动本地网络

此命令将启动包含 ZetaChain 和 Solana 的本地开发环境：

```bash
yarn zetachain localnet start
```

让该命令在一个终端窗口中持续运行。

## 编译和部署示例通用合约

在新的终端窗口中，编译并部署通用合约：

```bash
npx hardhat compile --force
npx hardhat deploy --name Universal --network localhost --gateway 0x5FC8d32690cc91D4c39d9d3abcBD16989F875707
```

您将看到包含合约地址的确认信息：

```
🚀 Successfully deployed "Universal" contract on localhost.
📜 Contract address: 0x8198f5d8F8CfFE8f9C413d98a0A55aEB8ab9FbB7
```

请记下合约地址以备后用（在此示例中为 `0x8198f5d8F8CfFE8f9C413d98a0A55aEB8ab9FbB7`）。

## 存款

从 Solana 向 ZetaChain 存入 SOL 代币：

```bash
npx hardhat localnet:solana-deposit \
  --receiver 0x8198f5d8F8CfFE8f9C413d98a0A55aEB8ab9FbB7 \
  --amount 0.1
```

- `--receiver`：ZetaChain 上的通用合约地址
- `--amount`：要存入的 SOL 数量

## 存款并调用

存入代币并同时调用已部署的通用合约：

```bash
npx hardhat localnet:solana-deposit-and-call \
  --receiver 0x8198f5d8F8CfFE8f9C413d98a0A55aEB8ab9FbB7 \
  --amount 0.1 \
  --types '["string"]' hello
```

此命令存入代币，并使用参数 "hello" 触发通用合约函数。

## 将代币提取到 Solana

从 ZetaChain 提现代币回 Solana：

```bash
npx hardhat zetachain-withdraw \
  --gateway-zeta-chain 0x5FC8d32690cc91D4c39d9d3abcBD16989F875707 \
  --receiver DrexsvCMH9WWjgnjVbx1iFf3YZcKadupFmxnZLfSyotd \
  --network localhost \
  --zrc20 0xd97B1de3619ed2c6BEb3860147E30cA8A7dC9891 \
  --amount 0.1
```

- `--gateway-zeta-chain`：ZetaChain 网关地址
- `--receiver`：接收提现代币的 Solana 钱包地址
- `--zrc20`：要提现的代币在 ZetaChain 上的表示（ZRC-20 地址）
- `--amount`：提现金额

## 提现并调用 Solana 程序

除了简单地将代币从 ZetaChain 提现回 Solana 之外，您还可以在提现过程中执行 Solana 程序。这允许更复杂的交互，例如在收到资金后立即触发链上逻辑。例如，您可以在单笔交易中提取 SOL 或 SPL-20 代币并调用 Solana 程序，实现自动质押、交换或合约执行等用例。

`solana` 目录包含一个示例 Solana 程序，其中包含 `on_call` 函数，在提取过程中，ZetaChain 上的通用应用可以调用该函数。

以下步骤将指导您设置示例 Solana 程序，并使用 ZetaChain Gateway 执行"提现并调用"。

### 构建和设置示例 Solana 程序

设置 SPL-20 USDC 地址。您可以在 localnet 输出的表格中找到此地址：

```bash
USDC_SPL=3Kx5SY7SwzdUZSorLVSpPgxBL8DZFiu8mg4FWduu2tQp
```

```bash
cd solana && anchor build && npx ts-node setup/main.ts "$USDC_SPL" && cd -
```

运行此命令后，您应该看到指示程序已成功部署的输出，例如：

```
Connected program deployment output: Program Id: 9BjVGjn28E58LgSi547JYEpqpgRoo1TErkbyXiRSNDQy
```

### 提现 SOL 并调用 Solana 程序

调用 ZetaChain 网关以提现 SOL 并调用 Solana 程序：

```bash
npx hardhat zetachain-withdraw-and-call \
  --receiver 9BjVGjn28E58LgSi547JYEpqpgRoo1TErkbyXiRSNDQy \
  --gateway-zeta-chain 0x5FC8d32690cc91D4c39d9d3abcBD16989F875707 \
  --zrc20 0xd97B1de3619ed2c6BEb3860147E30cA8A7dC9891 \
  --amount 0.01 \
  --network localhost \
  --types '["bytes"]' $(npx ts-node solana/setup/encodeCallArgs.ts "sol" "$USDC_SPL")
```

- `--receiver`：要调用的 Solana 程序 ID
- `--types '["bytes"]'`：指定合约调用参数是字节数组（编码的 Solana 调用数据）
- `"$ENCODED_ACCOUNTS_AND_DATA"`：我们在上一步中生成的编码 Solana 程序调用参数
- `--zrc20`：SOL 在 ZetaChain 上的 ZRC-20 地址

### 提现 SPL-20 并调用 Solana 程序

调用 ZetaChain 网关以提现 ZRC-20 SPL-20 USDC 并调用 Solana 程序：

```bash
npx hardhat zetachain-withdraw-and-call \
  --receiver 9BjVGjn28E58LgSi547JYEpqpgRoo1TErkbyXiRSNDQy \
  --gateway-zeta-chain 0x5FC8d32690cc91D4c39d9d3abcBD16989F875707 \
  --zrc20 0x48f80608B672DC30DC7e3dbBd0343c5F02C738Eb \
  --amount 0.01 \
  --network localhost \
  --types '["bytes"]' $(npx ts-node solana/setup/encodeCallArgs.ts "spl" "$USDC_SPL")
```

- `--zrc20`：SPL-20 USDC 在 ZetaChain 上的 ZRC-20 地址

在本教程中，您学习了如何在 ZetaChain 上部署通用合约、从 Solana 存入 SOL 和 SPL-20 代币、在存款期间调用合约、将资产提现回 Solana，甚至在提现时触发 Solana 程序。