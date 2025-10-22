# ZetaChain CLI

一个用于构建 [ZetaChain](https://www.zetachain.com) 通用应用程序并与之交互的命令行界面。通过一个 CLI 无缝地与 EVM、Solana、Bitcoin、Sui 和 TON 交互。

## ✨ 特性

- 从模板**生成**新的 ZetaChain 通用应用脚手架
- 通过一个命令**启动**包含多链（EVM、Solana 等）的本地开发环境
- **查询**跨链费用、合约、余额、跨链交易、代币等
- 在 Solana、Sui、Bitcoin、TON 和 ZetaChain 上的通用应用之间进行**跨链调用**
- 在连接的链之间**转移**支持的代币

## ✅ 先决条件

- Node.js ≥ 18
- Git（用于克隆模板）
- 可选：Docker ≥ 24（用于 `localnet`）

-----

## 🚀 快速开始

无需安装即可运行：

```bash
npx zetachain@next new
```



或者全局安装：

```bash
npm install -g zetachain@latest
```

使用 `zetachain@next` 获取最新的前沿构建版本。

-----

## 📘 示例

创建一个新项目：

```bash
zetachain new
```

启动本地网络 (localnet)：

```bash
zetachain localnet start
```

查询跨链余额：

```bash
zetachain query balances
```

-----

## 🧭 CLI 参考

获取完整的命令文档：

```bash
zetachain docs
```

或者对任何命令使用 `--help`：

```bash
zetachain accounts --help
```

-----

## 🤝 贡献

我们欢迎贡献！请提交 issue 或 pull request。

-----

## 📚 了解更多

- [ZetaChain 文档](https://www.zetachain.com/docs)
- [CLI 文档](https://www.zetachain.com/docs/reference/cli/)
- [加入 Discord](https://discord.gg/zetachain)

-----

## zetachain new

```text
用法: zetachain new [选项]

创建一个新的通用合约项目。

选项:
  --verbose              启用详细日志记录
  --output <目录>        指定自定义输出目录或名称
  --project <项目名称>   指定要使用的示例项目并跳过提示
  -h, --help             显示命令的帮助信息
```

-----

## zetachain accounts

```text
用法: zetachain accounts [选项] [命令]

选项:
  -h, --help     显示命令的帮助信息

命令:
  create [选项]  创建一个新账户
  delete [选项]  删除一个现有账户
  import [选项]  使用私钥或助记词导入一个现有账户
  list [选项]    列出所有可用账户
  show [选项]    显示一个现有账户的详情
```

-----

## zetachain accounts create

```text
用法: zetachain accounts create [选项]

选项:
  --type <类型>  账户类型 (可选: "evm", "solana", "sui", "bitcoin", "ton")
  --name <名称>  账户名称 (默认: "default")
  -h, --help     显示命令的帮助信息
```

-----

## zetachain accounts delete

```text
用法: zetachain accounts delete [选项]

选项:
  --type <类型>  账户类型 (可选: "evm", "solana", "sui", "bitcoin", "ton")
  --name <名称>  账户名称
  -h, --help     显示命令的帮助信息
```

-----

## zetachain accounts import

```text
用法: zetachain accounts import [选项]

使用私钥或助记词导入一个现有账户

选项:
  --type <类型>        账户类型 (可选: "evm", "solana", "sui", "bitcoin", "ton")
  --name <名称>        账户名称 (默认: "default")
  --private-key <密钥>  十六进制格式的私钥
  --mnemonic <短语>    助记词短语
  -h, --help           显示命令的帮助信息
```

-----

## zetachain accounts list

```text
用法: zetachain accounts list [选项]

选项:
  --json      以 JSON 格式输出
  -h, --help  显示命令的帮助信息
```

-----

## zetachain accounts show

```text
用法: zetachain accounts show [选项]

选项:
  --type <类型>  账户类型 (可选: "evm", "solana", "sui", "bitcoin", "ton")
  --name <名称>  账户名称
  -h, --help     显示命令的帮助信息
```

-----

## zetachain query

```text
用法: zetachain query|q [选项] [命令]

选项:
  -h, --help     显示命令的帮助信息

命令:
  balances [选项]  获取原生代币和 ZETA 代币余额
  cctx [选项]      实时查询跨链交易数据
  fees [选项]      获取全链和跨链消息传递费用
  tokens|t         ZRC-20 代币相关命令
  chains|c         支持的链相关命令
```

-----

## zetachain query balances

```text
用法: zetachain query balances [选项]

选项:
  --evm <地址>       获取指定 EVM 地址的余额
  --solana <地址>    获取指定 Solana 地址的余额
  --bitcoin <地址>   获取指定 Bitcoin 地址的余额
  --sui <地址>       获取指定 Sui 地址的余额
  --ton <地址>       获取指定 TON 地址的余额
  --name <名称>      账户名称
  --network <网络>   要使用的网络 (可选: "mainnet", "testnet", 默认: "testnet")
  --json             以 JSON 格式输出余额
  --show-zero        包含零余额 (默认: false)
  -h, --help         显示命令的帮助信息
```

-----

## zetachain query cctx

```text
用法: zetachain query cctx [选项]

实时查询跨链交易数据

选项:
  -h, --hash <哈希>    入站交易哈希
  -r, --rpc <rpc>      RPC 端点 (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public")
  -d, --delay <毫秒>   轮询间隔毫秒数 (默认: "2000")
  -t, --timeout <毫秒> 超时时长毫秒数 (默认: 0 表示无限)
  --help             显示命令的帮助信息
```

-----

## zetachain query fees

```text
用法: zetachain query fees [选项]

获取全链和跨链消息传递费用

选项:
  --api <url>          API 端点 URL (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public")
  --rpc <url>          RPC 端点 URL (默认: "https://zetachain-athens-evm.blockpi.network/v1/rpc/public")
  --gas-limit <限制>   提款并调用的 Gas 限制
  --json               以 JSON 格式输出结果
  -h, --help           显示命令的帮助信息
```

-----

## zetachain query tokens

```text
用法: zetachain query tokens|t [选项] [命令]

ZRC-20 代币相关命令

选项:
  -h, --help     显示命令的帮助信息

命令:
  list|l [选项]  列出所有 ZRC-20 代币
  show|s [选项]  显示特定 ZRC-20 代币的详细信息
```

-----

## zetachain query tokens list

```text
用法: zetachain query tokens list|l [选项]

列出所有 ZRC-20 代币

选项:
  --api <url>          API 端点 URL (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public")
  --json               以 JSON 格式输出代币
  --columns <值...>    要显示的额外列 (可选: "asset", "type", "decimals", 默认: [])
  -h, --help           显示命令的帮助信息
```

-----

## zetachain query tokens show

```text
用法: zetachain query tokens show|s [选项]

显示特定 ZRC-20 代币的详细信息

选项:
  --api <url>        API 端点 URL (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public")
  --symbol -s <符号>  代币符号 (例如: POL.AMOY, USDC.BSC)
  --field -f <字段>  返回特定字段值（用于脚本）。使用 'zrc20' 作为 'zrc20_contract_address' 的简写
  --json             以 JSON 格式输出代币
  -h, --help         显示命令的帮助信息
```

-----

## zetachain query chains

```text
用法: zetachain query chains|c [选项] [命令]

支持的链相关命令

选项:
  -h, --help     显示命令的帮助信息

命令:
  list|l [选项]  列出所有支持的链
  show|s [选项]  显示特定链的详细信息（通过链名称或链 ID）
```

-----

## zetachain query chains list

```text
用法: zetachain query chains list|l [选项]

列出所有支持的链

选项:
  --api <url>  API 端点 URL (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public")
  --json       以 JSON 格式输出链信息
  -h, --help   显示命令的帮助信息
```

-----

## zetachain query chains show

```text
用法: zetachain query chains show|s [选项]

显示特定链的详细信息（通过链名称或链 ID）

选项:
  --api-testnet <url>        测试网 API 端点 URL (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public")
  --api-mainnet <url>        主网 API 端点 URL (默认: "https://zetachain.blockpi.network/lcd/v1/public")
  --chain-name  <链名称>     链名称
  -c, --chain-id <链ID>    链 ID
  --field -f <字段>        返回特定字段值（用于脚本）
  --json                   以 JSON 格式输出链信息
  -h, --help               显示命令的帮助信息
```

-----

## zetachain faucet

```text
用法: zetachain faucet [选项]

从水龙头请求测试网 ZETA 代币。

选项:
  --address <地址>  接收者地址。
  --name <名称>     如果未提供地址，则使用的账户名称 (默认: "default")
  -h, --help        显示命令的帮助信息
```

-----

## zetachain zetachain

```text
用法: zetachain zetachain|z [选项] [命令]

选项:
  -h, --help               显示命令的帮助信息

命令:
  call [选项]              从 ZetaChain 调用连接链上的合约
  withdraw [选项]          从 ZetaChain 提款代币到连接链
  withdraw-and-call [选项] 从 ZetaChain 提款代币并调用连接链上的合约
```

-----

## zetachain zetachain call

```text
用法: zetachain zetachain call [选项]

选项:
  --zrc20 <地址>                   用于支付费用的 ZRC-20 地址
  --receiver <地址>                连接链上接收者合约的地址。非十六进制字符串将自动编码为十六进制。
  --name <名称>                    账户名称 (默认: "default")
  --chain-id <链ID>                网络的链 ID
  --private-key <密钥>             用于签署交易的私钥
  --rpc <url>                      网络的 RPC URL
  --gateway <地址>                 ZetaChain 上的网关合约地址
  --revert-address <地址>          回滚地址 (默认: "0x0000000000000000000000000000000000000000")
  --abort-address <地址>           中止地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert                 是否在回滚时调用 (默认: false)
  --on-revert-gas-limit <限制>     回滚交易的 Gas 限制 (默认: "1000000")
  --revert-message <消息>          回滚消息 (默认: "0x")
  --tx-options-gas-limit <限制>    交易的 Gas 限制 (默认: "1000000")
  --tx-options-gas-price <价格>    交易的 Gas 价格 (默认: "10000000000")
  --call-options-gas-limit <限制>  调用的 Gas 限制 (默认: "1000000")
  --call-options-is-arbitrary-call 调用任意函数 (默认: false)
  --yes                            跳过确认提示 (默认: false)
  --function <函数>                要调用的函数 (例如: "hello(string)")
  --types <类型...>                参数类型列表 (例如: uint256 address)
  --values <值...>                 函数调用的参数值
  --data <数据>                    用于非 EVM 链（如 Solana）的原始数据
  -h, --help                       显示命令的帮助信息
```

-----

## zetachain zetachain withdraw

```text
用法: zetachain zetachain withdraw [选项]

选项:
  --zrc20 <地址>                   用于支付费用的 ZRC-20 地址
  --receiver <地址>                连接链上接收者合约的地址。非十六进制字符串将自动编码为十六进制。
  --name <名称>                    账户名称 (默认: "default")
  --chain-id <链ID>                网络的链 ID
  --private-key <密钥>             用于签署交易的私钥
  --rpc <url>                      网络的 RPC URL
  --gateway <地址>                 ZetaChain 上的网关合约地址
  --revert-address <地址>          回滚地址 (默认: "0x0000000000000000000000000000000000000000")
  --abort-address <地址>           中止地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert                 是否在回滚时调用 (默认: false)
  --on-revert-gas-limit <限制>     回滚交易的 Gas 限制 (默认: "1000000")
  --revert-message <消息>          回滚消息 (默认: "0x")
  --tx-options-gas-limit <限制>    交易的 Gas 限制 (默认: "1000000")
  --tx-options-gas-price <价格>    交易的 Gas 价格 (默认: "10000000000")
  --call-options-gas-limit <限制>  调用的 Gas 限制 (默认: "1000000")
  --call-options-is-arbitrary-call 调用任意函数 (默认: false)
  --yes                            跳过确认提示 (默认: false)
  --amount <金额>                  要提取的代币数量
  -h, --help                       显示命令的帮助信息
```

-----

## zetachain zetachain withdraw-and-call

```text
用法: zetachain zetachain withdraw-and-call [选项]

选项:
  --zrc20 <地址>                   用于支付费用的 ZRC-20 地址
  --receiver <地址>                连接链上接收者合约的地址。非十六进制字符串将自动编码为十六进制。
  --name <名称>                    账户名称 (默认: "default")
  --chain-id <链ID>                网络的链 ID
  --private-key <密钥>             用于签署交易的私钥
  --rpc <url>                      网络的 RPC URL
  --gateway <地址>                 ZetaChain 上的网关合约地址
  --revert-address <地址>          回滚地址 (默认: "0x0000000000000000000000000000000000000000")
  --abort-address <地址>           中止地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert                 是否在回滚时调用 (默认: false)
  --on-revert-gas-limit <限制>     回滚交易的 Gas 限制 (默认: "1000000")
  --revert-message <消息>          回滚消息 (默认: "0x")
  --tx-options-gas-limit <限制>    交易的 Gas 限制 (默认: "1000000")
  --tx-options-gas-price <价格>    交易的 Gas 价格 (默认: "10000000000")
  --call-options-gas-limit <限制>  调用的 Gas 限制 (默认: "1000000")
  --call-options-is-arbitrary-call 调用任意函数 (默认: false)
  --yes                            跳过确认提示 (默认: false)
  --amount <金额>                  要提取的代币数量
  --function <函数>                要调用的函数 (例如: "hello(string)")
  --types <类型...>                参数类型列表 (例如: uint256 address)
  --values <值...>                 函数调用的参数值
  --data <数据>                    用于非 EVM 链（如 Solana）的原始数据
  -h, --help                       显示命令的帮助信息
```

-----

## zetachain evm

```text
用法: zetachain evm [选项] [命令]

选项:
  -h, --help               显示命令的帮助信息

命令:
  call [选项]              从 EVM 兼容链调用 ZetaChain 上的合约
  deposit-and-call [选项]  从 EVM 兼容链存入代币并调用 ZetaChain 上的合约
  deposit [选项]           从 EVM 兼容链存入代币到 ZetaChain
```

-----

## zetachain evm call

```text
用法: zetachain evm call [选项]

选项:
  --chain-id <链ID>                网络的链 ID
  --receiver <地址>                ZetaChain 上的接收者地址
  --name <名称>                    账户名称 (默认: "default")
  --private-key <密钥>             用于签署交易的私钥
  --rpc <url>                      源链的 RPC URL
  --gateway <地址>                 EVM 网关地址
  --revert-address <地址>          失败时回滚到的地址 (默认: 签名者地址)
  --abort-address <地址>           中止时接收资金的地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert                 失败时是否调用回滚地址 (默认: false)
  --on-revert-gas-limit <限制>     回滚操作的 Gas 限制 (默认: "200000")
  --revert-message <消息>          回滚时包含的消息 (默认: "")
  --gas-limit <限制>               交易的 Gas 限制
  --gas-price <价格>               交易的 Gas 价格
  --yes                            跳过确认提示 (默认: false)
  --types <类型...>                参数类型列表 (例如: uint256 address)
  --values <值...>                 函数调用的参数值
  -h, --help                       显示命令的帮助信息
```

-----

## zetachain evm deposit-and-call

```text
用法: zetachain evm deposit-and-call [选项]

选项:
  --chain-id <链ID>                网络的链 ID
  --receiver <地址>                ZetaChain 上的接收者地址
  --name <名称>                    账户名称 (默认: "default")
  --private-key <密钥>             用于签署交易的私钥
  --rpc <url>                      源链的 RPC URL
  --gateway <地址>                 EVM 网关地址
  --revert-address <地址>          失败时回滚到的地址 (默认: 签名者地址)
  --abort-address <地址>           中止时接收资金的地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert                 失败时是否调用回滚地址 (默认: false)
  --on-revert-gas-limit <限制>     回滚操作的 Gas 限制 (默认: "200000")
  --revert-message <消息>          回滚时包含的消息 (默认: "")
  --gas-limit <限制>               交易的 Gas 限制
  --gas-price <价格>               交易的 Gas 价格
  --yes                            跳过确认提示 (默认: false)
  --amount <金额>                  要存入的代币数量
  --erc20 <地址>                   ERC20 代币地址（对于原生代币存款可选）
  --types <类型...>                参数类型列表 (例如: uint256 address)
  --values <值...>                 函数调用的参数值
  -h, --help                       显示命令的帮助信息
```

-----

## zetachain evm deposit

```text
用法: zetachain evm deposit [选项]

选项:
  --chain-id <链ID>                网络的链 ID
  --receiver <地址>                ZetaChain 上的接收者地址
  --name <名称>                    账户名称 (默认: "default")
  --private-key <密钥>             用于签署交易的私钥
  --rpc <url>                      源链的 RPC URL
  --gateway <地址>                 EVM 网关地址
  --revert-address <地址>          失败时回滚到的地址 (默认: 签名者地址)
  --abort-address <地址>           中止时接收资金的地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert                 失败时是否调用回滚地址 (默认: false)
  --on-revert-gas-limit <限制>     回滚操作的 Gas 限制 (默认: "200000")
  --revert-message <消息>          回滚时包含的消息 (默认: "")
  --gas-limit <限制>               交易的 Gas 限制
  --gas-price <价格>               交易的 Gas 价格
  --yes                            跳过确认提示 (默认: false)
  --amount <金额>                  要存入的代币数量
  --erc20 <地址>                   ERC20 代币地址（对于原生代币存款可选）
  -h, --help                       显示命令的帮助信息
```

-----

## zetachain solana

```text
用法: zetachain solana [选项] [命令]

选项:
  -h, --help         显示命令的帮助信息

命令:
  call [选项]              调用 ZetaChain 上的通用合约
  deposit-and-call [选项]  从 Solana 存入代币并调用 ZetaChain 上的通用合约
  deposit [选项]           从 Solana 存入代币
  encode [选项]            为 Solana 编码有效负载数据
```

-----

## zetachain solana call

```text
用法: zetachain solana call [选项]

调用 ZetaChain 上的通用合约

选项:
  --recipient <接收者>            ZetaChain 上的 EOA 或合约地址
  --mnemonic <助记词>             助记词
  --name <名称>                 钱包名称 (默认: "default")
  --private-key <私钥>          Base58 或十六进制格式（可选 0x 前缀）的私钥
  --chain-id <链ID>             网络的链 ID
  --revert-address <回滚地址>     回滚地址
  --abort-address <中止地址>      中止地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert              在回滚时调用 (默认: false)
  --revert-message <回滚消息>     回滚消息 (默认: "")
  --on-revert-gas-limit <限制>    回滚 Gas 限制 (默认: "0")
  --types <类型...>             参数类型列表 (例如: uint256 address)
  --values <值...>              函数调用的参数值
  -h, --help                    显示命令的帮助信息
```

-----

## zetachain solana deposit-and-call

```text
用法: zetachain solana deposit-and-call [选项]

从 Solana 存入代币并调用 ZetaChain 上的通用合约

选项:
  --recipient <接收者>            ZetaChain 上的 EOA 或合约地址
  --mnemonic <助记词>             助记词
  --name <名称>                 钱包名称 (默认: "default")
  --private-key <私钥>          Base58 或十六进制格式（可选 0x 前缀）的私钥
  --chain-id <链ID>             网络的链 ID
  --revert-address <回滚地址>     回滚地址
  --abort-address <中止地址>      中止地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert              在回滚时调用 (默认: false)
  --revert-message <回滚消息>     回滚消息 (默认: "")
  --on-revert-gas-limit <限制>    回滚 Gas 限制 (默认: "0")
  --amount <金额>               要存入的代币数量
  --token-program <代币程序>      代币程序 (默认: "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA")
  --types <类型...>             参数类型列表 (例如: uint256 address)
  --values <值...>              函数调用的参数值
  --mint <铸币地址>             SPL 代币铸币地址
  -h, --help                    显示命令的帮助信息
```

-----

## zetachain solana deposit

```text
用法: zetachain solana deposit [选项]

选项:
  --recipient <接收者>            ZetaChain 上的 EOA 或合约地址
  --mnemonic <助记词>             助记词
  --name <名称>                 钱包名称 (默认: "default")
  --private-key <私钥>          Base58 或十六进制格式（可选 0x 前缀）的私钥
  --chain-id <链ID>             网络的链 ID
  --revert-address <回滚地址>     回滚地址
  --abort-address <中止地址>      中止地址 (默认: "0x0000000000000000000000000000000000000000")
  --call-on-revert              在回滚时调用 (默认: false)
  --revert-message <回滚消息>     回滚消息 (默认: "")
  --on-revert-gas-limit <限制>    回滚 Gas 限制 (默认: "0")
  --amount <金额>               要存入的代币数量
  --token-program <代币程序>      代币程序 (默认: "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA")
  --mint <铸币地址>             SPL 代币铸币地址
  -h, --help                    显示命令的帮助信息
```

-----

## zetachain solana encode

```text
用法: zetachain solana encode [选项]

选项:
  --connected <地址>      已连接的 PDA 账户地址
  --data <数据>           要编码的数据
  --gateway <地址>        网关程序地址
  --mint <地址>           用于 SPL 代币操作的铸币地址
  --accounts <账户...>    附加账户，格式为 '地址:isWritable'
  -h, --help              显示命令的帮助信息
```

-----

## zetachain sui

```text
用法: zetachain sui [选项] [命令]

选项:
  -h, --help         显示命令的帮助信息

命令:
  deposit-and-call [选项]  从 Sui 存入代币并调用 ZetaChain 上的合约
  deposit [选项]           从 Sui 存入代币
  encode [选项]            为 SUI 编码有效负载数据
```

-----

## zetachain sui deposit-and-call

```text
用法: zetachain sui deposit-and-call [选项]

选项:
  --mnemonic <助记词>          账户的助记词
  --private-key <私钥>       账户的私钥
  --gateway-object <对象ID>    网关对象 ID
  --gateway-package <包ID>   网关包 ID
  --receiver <接收者>        ZetaChain 上的接收者地址
  --amount <金额>            以小数格式表示的存款金额
  --chain-id <链ID>          链 ID
  --coin-type <币种类型>     要存入的币种类型 (默认: "0x2::sui::SUI")
  --gas-budget <预算>        以 MIST 为单位的 Gas 预算 (默认: "10000000")
  --name <名称>              账户名称 (默认: "default")
  --decimals <小数位数>      币种类型的小数位数 (默认: "9")
  --values <值...>           函数调用的参数值
  --types <类型...>          参数类型列表 (例如: uint256 address)
  -h, --help                 显示命令的帮助信息
```

-----

## zetachain sui deposit

```text
用法: zetachain sui deposit [选项]

选项:
  --mnemonic <助记词>          账户的助记词
  --private-key <私钥>       账户的私钥
  --gateway-object <对象ID>    网关对象 ID
  --gateway-package <包ID>   网关包 ID
  --receiver <接收者>        ZetaChain 上的接收者地址
  --amount <金额>            以小数格式表示的存款金额
  --chain-id <链ID>          链 ID
  --coin-type <币种类型>     要存入的币种类型 (默认: "0x2::sui::SUI")
  --gas-budget <预算>        以 MIST 为单位的 Gas 预算 (默认: "10000000")
  --name <名称>              账户名称 (默认: "default")
  --decimals <小数位数>      币种类型的小数位数 (默认: "9")
  -h, --help                 显示命令的帮助信息
```

-----

## zetachain sui encode

```text
用法: zetachain sui encode [选项]

选项:
  --data <数据>                   要编码的数据
  --type-arguments <类型参数...>   用于编码的类型参数
  --objects <对象...>             要包含在编码中的对象 (逗号分隔)
  -h, --help                      显示命令的帮助信息
```

-----

## zetachain ton

```text
用法: zetachain ton [选项] [命令]

TON 相关命令

选项:
  -h, --help         显示命令的帮助信息

命令:
  deposit-and-call [选项]  存入 TON 并调用 ZetaChain 上的通用合约
  deposit [选项]           将 TON 存入 ZetaChain 上的 EOA 或合约
```

-----

## zetachain ton deposit-and-call

```text
用法: zetachain ton deposit-and-call [选项]

存入 TON 并调用 ZetaChain 上的通用合约

选项:
  --mnemonic <助记词>    账户的助记词
  --name <名称>          账户名称 (默认: "default")
  --gateway <网关地址>   网关合约地址 (默认: testnet)
  --receiver <接收者>    接收者地址
  --rpc <rpc>            RPC 端点 (默认: testnet) (默认: "https://testnet.toncenter.com/api/v2/jsonRPC")
  --api-key <API密钥>    API 密钥
  --chain-id <链ID>      链 ID
  --amount <金额>        以 TON 为单位的金额
  --types <类型...>      ABI 类型
  --values <值...>       与类型对应的值
  --data <数据>          用于调用合约的数据
  -h, --help             显示命令的帮助信息
```

-----

## zetachain ton deposit

```text
用法: zetachain ton deposit [选项]

将 TON 存入 ZetaChain 上的 EOA 或合约

选项:
  --mnemonic <助记词>    账户的助记词
  --name <名称>          账户名称 (默认: "default")
  --gateway <网关地址>   网关合约地址 (默认: testnet)
  --receiver <接收者>    接收者地址
  --rpc <rpc>            RPC 端点 (默认: testnet) (默认: "https://testnet.toncenter.com/api/v2/jsonRPC")
  --api-key <API密钥>    API 密钥
  --chain-id <链ID>      链 ID
  --amount <金额>        以 TON 为单位的金额
  -h, --help             显示命令的帮助信息
```

-----

## zetachain bitcoin

```text
用法: zetachain bitcoin|b [选项] [命令]

Bitcoin 相关命令

选项:
  -h, --help     显示命令的帮助信息

命令:
  inscription|i  使用铭文进行交易
  memo|m         使用备注 (OP_RETURN) 进行交易
```

-----

## zetachain bitcoin inscription

```text
用法: zetachain bitcoin inscription|i [选项] [命令]

选项:
  -h, --help     显示命令的帮助信息

命令:
  call [选项]              调用 ZetaChain 上的合约
  deposit-and-call [选项]  存入 BTC 并调用 ZetaChain 上的合约
  deposit [选项]           将 BTC 存入 ZetaChain
  encode [选项]            使用 ABI 编码为 Bitcoin 交易编码数据
```

-----

## zetachain bitcoin inscription call

```text
用法: zetachain bitcoin inscription call [选项]

选项:
  --yes                  跳过确认提示 (默认: false)
  -r, --receiver <地址>  ZetaChain 接收者地址
  --commit-fee <费用>    提交费用 (单位: sats) (默认: "15000")
  -g, --gateway <地址>   Bitcoin 网关 (TSS) 地址 (默认: "tb1qy9pqmk2pd9sv63g27jt8r657wy0d9ueeh0nqur")
  --private-key <密钥>   Bitcoin 私钥
  --name <名称>          账户名称 (默认: "default")
  --revert-address <地址>回滚地址
  --network <网络>       网络 (可选: "signet", "mainnet", 默认: "signet")
  --format <格式>        编码格式 (可选: "ABI", "CompactLong", "CompactShort", 默认: "ABI")
  --data <数据>          传递原始数据
  --bitcoin-api <url>    Bitcoin API (默认: "https://mempool.space/signet/api")
  --gas-price-api <url>  ZetaChain API (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/gasPrice/18333")
  -t, --types <类型...>  ABI 类型
  -v, --values <值...>   与类型对应的值
  -h, --help             显示命令的帮助信息
```

-----

## zetachain bitcoin inscription deposit-and-call

```text
用法: zetachain bitcoin inscription deposit-and-call [选项]

选项:
  --yes                  跳过确认提示 (默认: false)
  -r, --receiver <地址>  ZetaChain 接收者地址
  --commit-fee <费用>    提交费用 (单位: sats) (默认: "15000")
  -g, --gateway <地址>   Bitcoin 网关 (TSS) 地址 (默认: "tb1qy9pqmk2pd9sv63g27jt8r657wy0d9ueeh0nqur")
  --private-key <密钥>   Bitcoin 私钥
  --name <名称>          账户名称 (默认: "default")
  --revert-address <地址>回滚地址
  --network <网络>       网络 (可选: "signet", "mainnet", 默认: "signet")
  --format <格式>        编码格式 (可选: "ABI", "CompactLong", "CompactShort", 默认: "ABI")
  --data <数据>          传递原始数据
  --bitcoin-api <url>    Bitcoin API (默认: "https://mempool.space/signet/api")
  --gas-price-api <url>  ZetaChain API (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/gasPrice/18333")
  -t, --types <类型...>  ABI 类型
  -v, --values <值...>   与类型对应的值
  -a, --amount <btc金额>  要发送的 BTC 金额 (单位: BTC)
  -h, --help             显示命令的帮助信息
```

-----

## zetachain bitcoin inscription deposit

```text
用法: zetachain bitcoin inscription deposit [选项]

选项:
  --yes                  跳过确认提示 (默认: false)
  -r, --receiver <地址>  ZetaChain 接收者地址
  --commit-fee <费用>    提交费用 (单位: sats) (默认: "15000")
  -g, --gateway <地址>   Bitcoin 网关 (TSS) 地址 (默认: "tb1qy9pqmk2pd9sv63g27jt8r657wy0d9ueeh0nqur")
  --private-key <密钥>   Bitcoin 私钥
  --name <名称>          账户名称 (默认: "default")
  --revert-address <地址>回滚地址
  --network <网络>       网络 (可选: "signet", "mainnet", 默认: "signet")
  --format <格式>        编码格式 (可选: "ABI", "CompactLong", "CompactShort", 默认: "ABI")
  --data <数据>          传递原始数据
  --bitcoin-api <url>    Bitcoin API (默认: "https://mempool.space/signet/api")
  --gas-price-api <url>  ZetaChain API (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/gasPrice/18333")
  -a, --amount <btc金额>  要发送的 BTC 金额 (单位: BTC)
  -h, --help             显示命令的帮助信息
```

-----

## zetachain bitcoin inscription encode

```text
用法: zetachain bitcoin inscription encode [选项]

选项:
  -r, --receiver <地址>      接收者地址
  -t, --types <类型...>      ABI 类型 (例如: string uint256) (默认: [])
  -v, --values <值...>       与类型对应的值 (默认: [])
  -a, --revert-address <地址> Bitcoin 回滚地址
  -o, --op-code <代码>       操作码 (可选: "Call", "Deposit", "DepositAndCall", "Invalid", 默认: "DepositAndCall")
  -f, --format <格式>        编码格式 (可选: "ABI", "CompactLong", "CompactShort", 默认: "ABI")
  -h, --help                 显示命令的帮助信息
```

-----

## zetachain bitcoin memo

```text
用法: zetachain bitcoin memo|m [选项] [命令]

选项:
  -h, --help     显示命令的帮助信息

命令:
  call [选项]              调用 ZetaChain 上的合约
  deposit-and-call [选项]  存入 BTC 并调用 ZetaChain 上的合约
  deposit [选项]           将 BTC 存入 ZetaChain
```

-----

## zetachain bitcoin memo call

```text
用法: zetachain bitcoin memo call [选项]

选项:
  --yes                  跳过确认提示 (默认: false)
  -r, --receiver <地址>  ZetaChain 接收者地址
  --commit-fee <费用>    提交费用 (单位: sats) (默认: "15000")
  -g, --gateway <地址>   Bitcoin 网关 (TSS) 地址 (默认: "tb1qy9pqmk2pd9sv63g27jt8r657wy0d9ueeh0nqur")
  --private-key <密钥>   Bitcoin 私钥
  --name <名称>          账户名称 (默认: "default")
  -d, --data <数据>      传递原始数据
  --network-fee <费用>   网络费用 (单位: sats) (默认: "1750")
  --network <网络>       网络 (可选: "signet", "mainnet", 默认: "signet")
  --bitcoin-api <url>    Bitcoin API (默认: "https://mempool.space/signet/api")
  --gas-price-api <url>  ZetaChain API (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/gasPrice/18333")
  -h, --help             显示命令的帮助信息
```

-----

## zetachain bitcoin memo deposit-and-call

```text
用法: zetachain bitcoin memo deposit-and-call [选项]

选项:
  --yes                  跳过确认提示 (默认: false)
  -r, --receiver <地址>  ZetaChain 接收者地址
  --commit-fee <费用>    提交费用 (单位: sats) (默认: "15000")
  -g, --gateway <地址>   Bitcoin 网关 (TSS) 地址 (默认: "tb1qy9pqmk2pd9sv63g27jt8r657wy0d9ueeh0nqur")
  --private-key <密钥>   Bitcoin 私钥
  --name <名称>          账户名称 (默认: "default")
  -d, --data <数据>      传递原始数据
  --network-fee <费用>   网络费用 (单位: sats) (默认: "1750")
  --network <网络>       网络 (可选: "signet", "mainnet", 默认: "signet")
  --bitcoin-api <url>    Bitcoin API (默认: "https://mempool.space/signet/api")
  --gas-price-api <url>  ZetaChain API (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/gasPrice/18333")
  -a, --amount <btc金额>  要发送的 BTC 金额 (单位: BTC)
  -h, --help             显示命令的帮助信息
```

-----

## zetachain bitcoin memo deposit

```text
用法: zetachain bitcoin memo deposit [选项]

选项:
  --yes                  跳过确认提示 (默认: false)
  -r, --receiver <地址>  ZetaChain 接收者地址
  --commit-fee <费用>    提交费用 (单位: sats) (默认: "15000")
  -g, --gateway <地址>   Bitcoin 网关 (TSS) 地址 (默认: "tb1qy9pqmk2pd9sv63g27jt8r657wy0d9ueeh0nqur")
  --private-key <密钥>   Bitcoin 私钥
  --name <名称>          账户名称 (默认: "default")
  -d, --data <数据>      传递原始数据
  --network-fee <费用>   网络费用 (单位: sats) (默认: "1750")
  --network <网络>       网络 (可选: "signet", "mainnet", 默认: "signet")
  --bitcoin-api <url>    Bitcoin API (默认: "https://mempool.space/signet/api")
  --gas-price-api <url>  ZetaChain API (默认: "https://zetachain-athens.blockpi.network/lcd/v1/public/zeta-chain/crosschain/gasPrice/18333")
  -a, --amount <btc金额>  要发送的 BTC 金额 (单位: BTC)
  -h, --help             显示命令的帮助信息
```

-----

## zetachain localnet

```text
用法: zetachain localnet [选项] [命令]

本地开发环境

选项:
  -h, --help     显示命令的帮助信息

命令:
  start [选项]  启动本地网络
  stop          停止本地网络
  check [选项]  检查本地网络是否正在运行
  ton           TON 相关命令
```

-----

## zetachain localnet start

```text
用法: zetachain localnet start [选项]

启动本地网络

选项:
  -p, --port <端口号>     运行 anvil 的端口 (默认: "8545")
  -a, --anvil <字符串>    传递给 anvil 的附加参数 (默认: "-q")
  -f, --force-kill        强制终止端口上的任何进程而不提示 (默认: false)
  -s, --stop-after-init   成功初始化后停止本地网络 (默认: false)
  -e, --exit-on-error     如果调用回滚则退出并报错 (默认: false)
  -v, --verbosity <级别>  日志记录器详细程度级别 (可选: "emerg", "alert", "crit", "error", "warning", "notice", "info", "debug", 默认: "info")
  --chains [链...]        启动本地网络时要启动的链 (可选: "ton", "solana", "sui", 默认: [])
  -h, --help              显示命令的帮助信息
```

-----

## zetachain localnet stop

```text
用法: zetachain localnet stop [选项]

停止本地网络

选项:
  -h, --help  显示命令的帮助信息
```


-----

## zetachain localnet check

```text
用法: zetachain localnet check [选项]

检查本地网络是否正在运行

选项:
  -d, --delay <秒数>  检查本地网络前等待的秒数 (默认: "3")
  -h, --help          显示命令的帮助信息
```

-----

## zetachain localnet ton

```text
用法: zetachain localnet ton [选项] [命令]

TON 相关命令

选项:
  -h, --help     显示命令的帮助信息

命令:
  balance [选项]    按地址显示余额
  faucet [选项]     从水龙头请求 TON
  wallet [选项]     创建并充值钱包
  withdraw [选项]   从网关提取 TON
  help [命令]       显示命令的帮助信息
```

-----

## zetachain localnet ton balance

```text
用法: zetachain localnet ton balance [选项]

按地址显示余额

选项:
  -a, --address <地址>  地址
  -h, --help            显示命令的帮助信息
```

-----

## zetachain localnet ton faucet

```text
用法: zetachain localnet ton faucet [选项]

从水龙头请求 TON

选项:
  -a, --address <地址>  地址
  -m, --amount <金额>   以 TON 为单位的金额 (默认: "100")
  -h, --help            显示命令的帮助信息
```

-----

## zetachain localnet ton wallet

```text
用法: zetachain localnet ton wallet [选项]

创建并充值钱包

选项:
  -m, --amount <金额>  要充值的 TON 金额 (默认: "100")
  -h, --help           显示命令的帮助信息
```

-----

## zetachain localnet ton withdraw

```text
用法: zetachain localnet ton withdraw [选项]

从网关提取 TON

选项:
  -a, --address <地址>    接收者
  -m, --amount <金额>     以 TON 为单位的金额 (默认: "1")
  -k, --private-key <密钥> Zeta 上的发送者私钥
  -g, --gateway <网关>    ZEVM 上的网关地址
  -t, --token <代币>      ZEVM 上的 TON.TON 代币地址
  -p, --port <端口>       Anvil 端口 (默认: "8545")
  -h, --help              显示命令的帮助信息
```

-----

## zetachain docs

```text
用法: zetachain docs [选项]

显示所有可用命令及其子命令的帮助信息

选项:
  -h, --help  显示命令的帮助信息
```

-----

## zetachain ask

```text
用法: zetachain ask [选项] [提示...]

与 ZetaChain 文档 AI 聊天

参数:
  prompt      发送给 AI 的提示

选项:
  -h, --help  显示命令的帮助信息
```
