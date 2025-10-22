# ZetaChain 节点 CLI

| 标题 | 描述 |
| :- | :- |
| ZetaChain 节点 CLI |  ZetaChain 节点程序（二进制文件）的命令行界面 |

## zetacored

Zetacore 守护进程（服务器）

### 选项

```
  -h, --help                help for zetacored
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored add-genesis-account](#zetacored-add-genesis-account)	 - 向 genesis.json 添加一个创世账户
* [zetacored add-observer-list](#zetacored-add-observer-list)	 - 向观察者映射器添加观察者列表，默认路径为 ~/.zetacored/os_info/observer_info.json
* [zetacored addr-conversion](#zetacored-addr-conversion)	 - 将 zeta1xxx 地址转换为验证者操作员地址 zetavaloper1xxx
* [zetacored collect-gentxs](#zetacored-collect-gentxs)	 - 收集创世交易并输出一个 genesis.json 文件
* [zetacored collect-observer-info](#zetacored-collect-observer-info)	 - 从文件夹收集观察者信息到创世文件中，默认路径为 ~/.zetacored/os_info/

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令
* [zetacored config](#zetacored-config)	 - 用于管理应用程序配置的实用工具
* [zetacored debug](#zetacored-debug)	 - 用于帮助调试应用程序的工具
* [zetacored docs](#zetacored-docs)	 - 为 zetacored 生成 Markdown 文档
* [zetacored export](#zetacored-export)	 - 将状态导出为 JSON
* [zetacored gentx](#zetacored-gentx)	 - 生成一个携带自我委托的创世交易
* [zetacored get-pubkey](#zetacored-get-pubkey)	 - 获取节点账户公钥
* [zetacored index-eth-tx](#zetacored-index-eth-tx)	 - 索引历史以太坊交易
* [zetacored init](#zetacored-init)	 - 初始化私有验证者、P2P、创世和应用程序配置文件
* [zetacored keys](#zetacored-keys)	 - 管理应用程序的密钥
* [zetacored parse-genesis-file](#zetacored-parse-genesis-file)	 - 解析提供的创世文件并将所需数据导入到可选提供的创世文件中
* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored rollback](#zetacored-rollback)	 - 将 Cosmos SDK 和 CometBFT 状态回滚一个高度
* [zetacored snapshots](#zetacored-snapshots)	 - 管理本地快照
* [zetacored start](#zetacored-start)	 - 运行全节点
* [zetacored status](#zetacored-status)	 - 查询远程节点状态
* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored upgrade-handler-version](#zetacored-upgrade-handler-version)	 - 打印默认的升级处理器版本
* [zetacored validate](#zetacored-validate)	 - 验证默认位置或作为参数传递的位置的创世文件
* [zetacored version](#zetacored-version)	 - 打印应用程序二进制版本信息

## zetacored add-genesis-account

添加一个创世账户到 genesis.json

### 概要

添加一个创世账户到 genesis.json。提供的账户必须指定账户地址或密钥名称以及初始代币列表。如果给出了密钥名称，地址将在本地 Keybase 中查找。初始代币列表必须包含有效的面额。账户可以可选地提供归属参数。

```
zetacored add-genesis-account [address_or_key_name] [coin][,[coin]] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询状态时使用的特定高度（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     add-genesis-account 命令的帮助信息
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端（os|file|kwallet|pass|test）
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式（text|json）
      --vesting-amount string    归属账户的代币数量
      --vesting-end-time int     归属账户的计划结束时间（Unix 时间戳）
      --vesting-start-time int   归属账户的计划开始时间（Unix 时间戳）
```

### 从父命令继承的选项

```
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored add-observer-list

向观察者映射器添加一个观察者列表，默认路径是 `~/.zetacored/os_info/observer_info.json`

```
zetacored add-observer-list [observer-list.json]  [flags]
```

### 选项

```
  -h, --help                帮助信息，用于 add-observer-list
      --keygen-block int    设置密钥生成区块，默认为 20（默认值 20）
      --tss-pubkey string   设置 TSS 公钥（如果使用旧版密钥生成）
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored addr-conversion

将 zeta1xxx 地址转换为验证者操作员地址 zetavaloper1xxx

### 概要

读取一个 zeta1xxx 或 zetavaloper1xxx 地址并将其转换为另一种类型；它总是输出 3 行；第 1 行是 zeta1xxx 地址，第 2 行是 zetavaloper1xxx 地址，第 3 行是以太坊地址。

```
zetacored addr-conversion [zeta address] [flags]
```

### 选项

```
  -h, --help   addr-conversion 的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored collect-gentxs

收集创世交易并输出一个 genesis.json 文件

```
zetacored collect-gentxs [flags]
```

### 选项

```
      --gentx-dir string   覆盖默认的 "gentx" 目录，从中收集并执行创世交易；默认为 [--home]/config/gentx/
  -h, --help               获取 collect-gentxs 命令的帮助信息
      --home string        应用主目录
```

### 从父命令继承的选项

```
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored collect-observer-info

将观察者信息从文件夹收集到创世文件中，默认路径为 `~/.zetacored/os_info/`

```
zetacored collect-observer-info [folder] [flags]
```

### 选项

```
  -h, --help   查看 collect-observer-info 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored comet

CometBFT 子命令

### 选项

```
  -h, --help   comet 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）
* [zetacored comet bootstrap-state](#zetacored-comet-bootstrap-state)	 - 使用轻客户端在任意区块高度引导 CometBFT 状态
* [zetacored comet reset-state](#zetacored-comet-reset-state)	 - 移除所有数据和 WAL
* [zetacored comet show-address](#zetacored-comet-show-address)	 - 显示此节点的 CometBFT 验证器共识地址
* [zetacored comet show-node-id](#zetacored-comet-show-node-id)	 - 显示此节点的 ID
* [zetacored comet show-validator](#zetacored-comet-show-validator)	 - 显示此节点的 CometBFT 验证器信息
* [zetacored comet unsafe-reset-all](#zetacored-comet-unsafe-reset-all)	 - （不安全）移除所有数据和 WAL，将此节点的验证器重置为创世状态
* [zetacored comet version](#zetacored-comet-version)	 - 打印 CometBFT 库的版本信息

## zetacored comet bootstrap-state

使用轻客户端在任意区块高度引导 CometBFT 状态

```
zetacored comet bootstrap-state [flags]
```

### 选项

```
      --height int   引导状态的区块高度，如果未提供则使用应用状态中的最新区块高度
  -h, --help         bootstrap-state 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令

## zetacored comet reset-state

移除所有数据和 WAL

```
zetacored comet reset-state [flags]
```

### 选项

```
-h, --help   reset-state 的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令

## zetacored comet show-address

显示此节点的 CometBFT 验证器共识地址。

```
zetacored comet show-address [flags]
```

### 选项

```
  -h, --help   show-address 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令

## zetacored comet show-node-id

显示本节点的 ID

```
zetacored comet show-node-id [flags]
```

### 选项

```
  -h, --help   显示 show-node-id 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令

## zetacored comet show-validator

显示此节点的 CometBFT 验证器信息

```
zetacored comet show-validator [flags]
```

### 选项

```
  -h, --help   show-validator 命令的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令

## zetacored comet unsafe-reset-all

（不安全操作）删除所有数据和 WAL，将此节点的验证器重置为创世状态

```
zetacored comet unsafe-reset-all [flags]
```

### 选项

```
  -h, --help              unsafe-reset-all 命令的帮助
      --keep-addr-book    保持地址簿不变
```

### 从父命令继承的选项

```
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令

## zetacored comet version

打印 CometBFT 库的版本信息

### 概要

打印此应用程序编译时所针对的协议和库的版本号。

```
zetacored comet version [flags]
```

### 选项

```
  -h, --help   查看 version 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored comet](#zetacored-comet)	 - CometBFT 子命令

## zetacored 配置

用于管理应用程序配置的工具

### 选项

```
  -h, --help   help for config
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）
* [zetacored config diff](#zetacored-config-diff)	 - 输出所有与 app.toml 默认值不同的配置值
* [zetacored config get](#zetacored-config-get)	 - 获取应用程序配置值
* [zetacored config home](#zetacored-config-home)	 - 输出用作二进制主目录的文件夹。当独立使用 `confix` 工具时，未设置主目录
* [zetacored config migrate](#zetacored-config-migrate)	 - 将 Cosmos SDK 应用程序配置文件迁移到指定版本
* [zetacored config set](#zetacored-config-set)	 - 设置应用程序配置值
* [zetacored config view](#zetacored-config-view)	 - 查看配置文件

## zetacored config diff

输出所有与 `app.toml` 默认值不同的配置值。

```
zetacored config diff [target-version] [app-toml-path] [flags]
```

### 选项

```
  -h, --help   显示 diff 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored config](#zetacored-config)	 - 用于管理应用程序配置的实用工具

## zetacored config get

获取应用程序配置值

### 概要

获取应用程序配置值。当独立使用 `confix` 工具时，[config] 参数必须是文件的路径，否则它必须是配置文件的名称（不带 .toml 扩展名）。

```
zetacored config get [config] [key] [flags]
```

### 选项

```
  -h, --help   help for get
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored config](#zetacored-config)	 - 用于管理应用程序配置的工具

## zetacored config home

输出用作二进制主目录的文件夹。当独立使用 `confix` 工具时，不会设置主目录。

### 概要

输出用作二进制主目录的文件夹。要更改主目录路径，请设置 `$APPD_HOME` 环境变量，或使用 `--home` 标志。

```
zetacored config home [flags]
```

### 选项

```
  -h, --help   关于 home 的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored config](#zetacored-config)	 - 用于管理应用程序配置的工具

## zetacored config migrate

迁移 Cosmos SDK 应用程序配置文件至指定版本

### 概要

将 Cosmos SDK 应用程序配置（app.toml）的内容迁移至指定版本。
除非提供 `--stdout` 选项，否则输出将就地写入。
如果在更新文件时出现任何错误，则不会写入任何输出。

```
zetacored config migrate [target-version] [app-toml-path] (options) [flags]
```

### 选项

```
  -h, --help             migrate 命令的帮助信息
      --skip-validate    跳过配置验证（允许迁移未知配置）
      --stdout           将更新后的配置打印到标准输出
      --verbose          将更改记录到标准错误输出
```

### 从父命令继承的选项

```
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored config](#zetacored-config)	 - 用于管理应用程序配置的实用工具

## zetacored config set

设置一个应用程序配置值

### 概要

设置一个应用程序配置值。当独立使用 `confix` 工具时，[config] 参数必须是文件的路径；否则，它必须是配置文件的名称（不带 .toml 扩展名）。

```
zetacored config set [config] [key] [value] [flags]
```

### 选项

```
-h, --help            设置命令的帮助信息
-s, --skip-validate   跳过配置验证（允许修改未知配置）
      --stdout          将更新后的配置打印到标准输出
-v, --verbose         将更改记录到标准错误
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored config](#zetacored-config)	 - 用于管理应用程序配置的工具

## zetacored config view

查看配置文件

### 概要

查看配置文件。当独立使用 `confix` 工具时，[config] 参数必须是文件路径；否则，它必须是不带 .toml 扩展名的配置文件名。

```
zetacored config view [config] [flags]
```

### 选项

```
  -h, --help                   查看命令的帮助信息
      --output-format string   输出格式 (json|toml) 
```

### 继承自父命令的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored config](#zetacored-config)	 - 用于管理应用程序配置的实用工具

## zetacored debug

用于帮助调试应用程序的工具

```
zetacored debug [flags]
```

### 选项

```
  -h, --help   help for debug
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）
* [zetacored debug addr](#zetacored-debug-addr)	 - 在十六进制和 bech32 之间转换地址
* [zetacored debug codec](#zetacored-debug-codec)	 - 用于帮助调试应用程序编解码器的工具
* [zetacored debug prefixes](#zetacored-debug-prefixes)	 - 列出 Bech32 中用于人类可读部分 (HRP) 的前缀
* [zetacored debug pubkey](#zetacored-debug-pubkey)	 - 从 proto JSON 解码公钥
* [zetacored debug pubkey-raw](#zetacored-debug-pubkey-raw)	 - 从十六进制、base64 或 bech32 解码 ED25519 或 secp256k1 公钥
* [zetacored debug raw-bytes](#zetacored-debug-raw-bytes)	 - 将原始字节输出（例如 [10 21 13 255]）转换为十六进制

## zetacored debug addr

在 hex 和 bech32 之间转换地址

### 概要

在 hex 编码和 bech32 之间转换地址。

示例：
$ zetacored debug addr cosmos1e0jnq2sun3dzjh8p2xq95kk0expwmd7shwjpfg
			

```
zetacored debug addr [address] [flags]
```

### 选项

```
  -h, --help   addr 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug](#zetacored-debug)	 - 用于帮助调试应用程序的工具

## zetacored debug codec

用于帮助调试应用程序编解码器的工具

```
zetacored debug codec [flags]
```

### 选项

```
  -h, --help   codec 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug](#zetacored-debug)	 - 用于帮助调试应用程序的工具
* [zetacored debug codec list-implementations](#zetacored-debug-codec-list-implementations)	 - 列出所提供接口的已注册类型 URL
* [zetacored debug codec list-interfaces](#zetacored-debug-codec-list-interfaces)	 - 列出所有已注册的接口类型 URL

## zetacored debug codec list-implementations

列出为提供的接口注册的类型 URL

### 概要

列出可以使用应用程序编解码器为提供的接口名称使用的已注册类型 URL

```
zetacored debug codec list-implementations [interface] [flags]
```

### 选项

```
  -h, --help   list-implementations 的帮助
```

### 从父命令继承的选项

```
      --home string         用于配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug codec](#zetacored-debug-codec)	 - 用于帮助调试应用程序编解码器的工具

## zetacored debug codec list-interfaces

列出所有已注册的接口类型 URL

### 简介

使用应用程序编解码器列出所有已注册的接口类型 URL

```
zetacored debug codec list-interfaces [flags]
```

### 选项

```
  -h, --help   显示 list-interfaces 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug codec](#zetacored-debug-codec)	 - 用于调试应用程序编解码器的工具

## zetacored debug prefixes

列出 Bech32 中用于人类可读部分 (HRP) 的前缀

### 概要

列出 Bech32 地址中使用的前缀。

```
zetacored debug prefixes [flags]
```

### 示例

```
$ zetacored debug prefixes
```

### 选项

```
  -h, --help   prefixes 命令的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug](#zetacored-debug)	 - 用于帮助调试应用程序的工具

## zetacored debug pubkey

从 proto JSON 解码公钥

### 概要

从 proto JSON 解码公钥并显示其地址。

示例：
$ zetacored debug pubkey '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"AurroA7jvfPd1AadmmOvWM2rJSwipXfRf8yD6pLbA2DJ"}'
			

```
zetacored debug pubkey [pubkey] [flags]
```

### 选项

```
  -h, --help   pubkey 的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug](#zetacored-debug)	 - 用于帮助调试应用程序的工具

## zetacored debug pubkey-raw

从 hex、base64 或 bech32 解码 ED25519 或 secp256k1 公钥

### 概要

从 hex、base64 或 bech32 解码公钥。

```
zetacored debug pubkey-raw [pubkey] -t [{ed25519, secp256k1}] [flags]
```

### 示例

```
zetacored debug pubkey-raw 8FCA9D6D1F80947FD5E9A05309259746F5F72541121766D5F921339DD061174A
zetacored debug pubkey-raw j8qdbR+AlH/V6aBTCSWXRvX3JUESF2bV+SEzndBhF0o=
zetacored debug pubkey-raw cosmospub1zcjduepq3l9f6mglsz28l40f5pfsjfvhgm6lwf2pzgtkd40eyyeem5rpza9q47axrz
```

### 选项

```
  -h, --help          pubkey-raw 命令的帮助信息
  -t, --type string   要解码的公钥类型（其中之一：secp256k1、ed25519） 
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式（json|plain） 
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'） 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug](#zetacored-debug)	 - 用于帮助调试应用程序的工具

## zetacored debug raw-bytes

将原始字节输出（例如 [10 21 13 255]）转换为十六进制

### 简介

将原始字节转换为十六进制。

```
zetacored debug raw-bytes [raw-bytes] [flags]
```

### 示例

```
zetacored debug raw-bytes '[72 101 108 108 111 44 32 112 108 97 121 103 114 111 117 110 100]'
```

### 选项

```
  -h, --help   获取 raw-bytes 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored debug](#zetacored-debug)	 - 用于帮助调试应用程序的工具

## zetacored 文档

为 zetacored 生成 Markdown 格式文档

```
zetacored docs [path] [flags]
```

### 选项

```
  -h, --help          针对 docs 命令的帮助信息
      --path string   文档生成的目标路径
```

### 从父命令继承的选项

```
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored export

将状态导出为 JSON

```
zetacored export [flags]
```

### 选项

```
      --for-zero-height              将状态导出以从高度零开始（执行预处理）
      --height int                   从特定高度导出状态（-1 表示最新高度）（默认 -1）
  -h, --help                         导出命令的帮助
      --home string                  应用程序主目录
      --jail-allowed-addrs strings   逗号分隔的被监禁验证器操作员地址列表，用于解除监禁
      --modules-to-export strings    逗号分隔的要导出的模块列表。如果为空，将导出所有模块
      --output-document string       导出的状态写入给定文件而不是 STDOUT
```

### 从父命令继承的选项

```
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored gentx

生成一个携带自委托的创世交易

### 概要

生成一个创世交易，该交易创建一个带有自委托的验证者，并由给定名称引用的密钥环中的密钥签名。可以可选地提供节点 ID 和共识公钥。如果省略，它们将从 `priv_validator.json` 文件中检索。包含以下默认参数：

	委托金额：           100000000stake
	佣金率：             0.1
	最大佣金率：         0.2
	佣金最大变化率：     0.01
	最小自委托：         1

示例：
```
$ zetacored gentx my-key-name 1000000stake --home=/path/to/home/dir --keyring-backend=os --chain-id=test-chain-1 \
    --moniker="myvalidator" \
    --commission-max-change-rate=0.01 \
    --commission-max-rate=1.0 \
    --commission-rate=0.07 \
    --details="..." \
    --security-contact="..." \
    --website="..."
```

```
zetacored gentx [key_name] [amount] [flags]
```

### 选项

```
  -a, --account-number uint                 签名账户的账户编号（仅限离线模式）
      --amount string                       绑定代币的数量
      --aux                                 生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string               交易广播模式（sync|async）
      --chain-id string                     网络链 ID
      --commission-max-change-rate string   最大佣金变化率百分比（每天）
      --commission-max-rate string          最大佣金率百分比
      --commission-rate string              初始佣金率百分比
      --details string                      验证者的（可选）详细信息
      --dry-run                             忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string                  费用授予者为交易授予费用
      --fee-payer string                    费用支付者代替签名者支付交易费用
      --fees string                         随交易支付的费用；例如：10uatom
      --from string                         用于签名的私钥名称或地址
      --gas string                          每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float                乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string                   用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                       构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                                gentx 命令的帮助信息
      --home string                         应用程序主目录
      --identity string                     （可选）身份签名（例如 UPort 或 Keybase）
      --ip string                           节点的公共 P2P IP
      --keyring-backend string              选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string                  客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                              使用连接的 Ledger 设备
      --min-self-delegation string          验证器要求的最小自委托
      --moniker string                      验证者的（可选）别名
      --node string                          指向此链的 CometBFT rpc 接口的 [host]:[port]
      --node-id string                       节点的 NodeID
      --note string                         为交易添加描述说明（之前为 --memo）
      --offline                             离线模式（不允许任何在线功能）
      --output-document string              将创世交易 JSON 文档写入给定文件而不是默认位置
      --p2p-port uint                       节点的公共 P2P 端口（默认 26656）
      --pubkey string                       验证者的 Protobuf JSON 编码公钥
      --security-contact string             验证者的（可选）安全联系人电子邮件
  -s, --sequence uint                       签名账户的序列号（仅限离线模式）
      --sign-mode string                    选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration           TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint                 已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                          小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                           启用无序交易交付；必须与 --timeout-duration 一起使用
      --website string                      验证者的（可选）网站
  -y, --yes                                 跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored get-pubkey

获取节点账户公钥

```
zetacored get-pubkey [tssKeyName] [password] [flags]
```

### 选项

```
  -h, --help   获取 get-pubkey 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored index-eth-tx

索引历史以太坊交易

### 概要

索引历史以太坊交易，它仅支持两种遍历方向以避免在使用任意区块范围时在索引器数据库中产生间隙：
- backward：从第一个索引区块索引到链上的最早区块，如果索引器数据库为空，则从最新区块开始。
- forward：从最新索引区块索引到链上的最新区块。

当启动节点时，索引器从最新索引区块开始以避免产生间隙。
大多数时候应使用 backward 模式，因此最新索引区块始终保持最新。

```
zetacored index-eth-tx [backward|forward] [flags]
```

### 选项

```
  -h, --help   用于 index-eth-tx 的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored init

初始化私有验证器、P2P、创世及应用配置文件

### 概要

初始化验证器及节点的配置文件。

```
zetacored init [moniker] [flags]
```

### 选项

```
      --chain-id string             创世文件链 ID，若留空则随机生成
      --consensus-key-algo string   用于共识密钥的算法
      --default-denom string        创世文件默认货币单位，若留空则默认值为 'stake'
  -h, --help                        显示 init 命令的帮助信息
      --home string                 节点的主目录
      --initial-height int          指定创世时的初始区块高度（默认为 1）
  -o, --overwrite                   覆盖现有的 genesis.json 文件
      --recover                     提供助记词以恢复现有密钥而非创建新密钥
```

### 从父命令继承的选项

```
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored keys

管理您的应用程序密钥

### 概要

密钥环管理命令。这些密钥可以是 CometBFT 加密库支持的任何格式，并且可以被轻客户端、全节点或任何其他需要使用私钥签名的应用程序使用。

密钥环支持以下后端：

    os          使用操作系统的默认凭据存储。
    file        在应用程序配置目录中使用基于文件的加密密钥库。
                此密钥环每次访问时都会请求密码，这可能在单个命令中多次发生，导致重复的密码提示。
    kwallet     使用 KDE 钱包管理器作为凭据管理应用程序。
    pass        使用 pass 命令行工具来存储和检索密钥。
    test        将密钥不安全地存储到磁盘。它不会提示输入解锁密码，仅应用于测试目的。

kwallet 和 pass 后端依赖于外部工具。有关更多信息，请参阅其各自文档：
    KWallet     https://github.com/KDE/kwallet
    pass        https://www.passwordstore.org/

pass 后端需要 GnuPG：https://gnupg.org/


### 选项

```
  -h, --help                     密钥命令的帮助
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端（os|file|test）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --log_format string    日志格式（json|plain）
      --log_level string     日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color         禁用彩色日志
      --trace                在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）
* [zetacored keys ](#zetacored-keys-)	 - 
* [zetacored keys add](#zetacored-keys-add)	 - 添加加密私钥（新生成或恢复），加密并保存到 [name] 文件
* [zetacored keys delete](#zetacored-keys-delete)	 - 删除给定密钥
* [zetacored keys export](#zetacored-keys-export)	 - 导出私钥
* [zetacored keys import](#zetacored-keys-import)	 - 将私钥导入本地密钥库
* [zetacored keys list](#zetacored-keys-list)	 - 列出所有密钥
* [zetacored keys list-key-types](#zetacored-keys-list-key-types)	 - 列出所有密钥类型
* [zetacored keys migrate](#zetacored-keys-migrate)	 - 将密钥从 amino 序列化格式迁移到 proto 序列化格式
* [zetacored keys mnemonic](#zetacored-keys-mnemonic)	 - 为某些输入熵计算 bip39 助记词
* [zetacored keys parse](#zetacored-keys-parse)	 - 从十六进制解析地址为 bech32 格式，反之亦然
* [zetacored keys rename](#zetacored-keys-rename)	 - 重命名现有密钥
* [zetacored keys show](#zetacored-keys-show)	 - 按名称或地址检索密钥信息
* [zetacored keys unsafe-export-eth-key](#zetacored-keys-unsafe-export-eth-key)	 - **不安全** 导出以太坊私钥
* [zetacored keys unsafe-import-eth-key](#zetacored-keys-unsafe-import-eth-key)	 - **不安全** 将以太坊私钥导入本地密钥库

## zetacored keys

```
zetacored keys  [flags]
```

### 选项

```
  -h, --help   此命令的帮助信息
```

### 从父命令继承的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择钥匙环的后端 (os|file|test)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志记录格式 (json|plain)
      --log_level string         日志记录级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序密钥

## zetacored keys add

添加一个加密的私钥（可以是新生成的或恢复的），对其进行加密，并保存到 [name] 文件

### 概要

派生一个新的私钥并加密到磁盘。
可选地指定一个 BIP39 助记词、一个 BIP39 密码短语以进一步保护助记词，
以及一个 bip32 HD 路径来派生特定账户。密钥将存储在给定的名称下，
并使用给定的密码进行加密。唯一必需的输入是加密密码。

如果使用 `-i` 运行，它将提示用户输入 BIP44 路径、BIP39 助记词和密码短语。
`--recover` 标志允许从种子密码短语恢复密钥。
如果使用 `--dry-run` 运行，将生成（或恢复）一个密钥，但不会存储到
本地密钥库。
使用 `--pubkey` 标志将任意公钥添加到密钥库以构建
多签交易。

使用 `--source` 标志在恢复或交互模式下从文件导入助记词。
示例：

	keys add testing --recover --source ./mnemonic.txt

您可以通过传递存储在钥匙环中的密钥名称列表
和通过 `--multisig-threshold` 所需的最小签名数量来创建和存储多签密钥。除非设置了 `--nosort` 标志，
否则密钥将按地址排序。
示例：

    keys add mymultisig --multisig "keyname1,keyname2,keyname3" --multisig-threshold 2

```
zetacored keys add [name] [flags]
```

### 选项

```
      --account uint32           用于 HD 派生的账户编号（小于等于 2147483647）
      --coin-type uint32         用于 HD 派生的币种类型编号（默认 118）
      --dry-run                  执行操作，但不将密钥添加到本地密钥库
      --hd-path string           手动 HD 路径派生（覆盖 BIP44 配置）
  -h, --help                     关于 add 的帮助信息
      --index uint32             用于 HD 派生的地址索引编号（小于等于 2147483647）
  -i, --interactive              交互式提示用户输入 BIP39 密码短语和助记词
      --key-type string          生成密钥的签名算法类型
      --ledger                   在 Ledger 设备上存储私钥的本地引用
      --multisig strings         存储在钥匙环中的密钥名称列表，用于构建传统的公钥多签密钥
      --multisig-threshold int   N 中需 K 个签名。与 --multisig 一起使用（默认 1）
      --no-backup                不输出种子短语（如果其他人在查看终端）
      --nosort                   传递给 --multisig 的密钥按提供顺序处理
      --pubkey string            以 JSON 格式解析公钥并将密钥信息保存到 [name] 文件
      --pubkey-base64 string     以 base64 格式解析公钥并保存密钥信息
      --recover                  提供种子短语以恢复现有密钥，而不是创建新密钥
      --source string            从文件导入助记词（仅在恢复或交互模式下可用）
```

### 从父命令继承的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择钥匙环的后端（os|file|test）
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式（json|plain）
      --log_level string         日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color             禁用彩色日志
      --output string            输出格式（text|json）
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序密钥

## zetacored keys delete

删除指定的密钥

### 概要

从 Keybase 后端删除密钥。

请注意，删除离线或账本密钥将仅删除本地存储的公钥引用，即存储在账本设备中的私钥无法通过 CLI 删除。

```
zetacored keys delete [name]... [flags]
```

### 选项

```
  -f, --force   无条件删除密钥，不询问密码。已弃用。
  -h, --help    删除命令的帮助信息
  -y, --yes     删除离线或账本密钥引用时跳过确认提示
```

### 从父命令继承的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端 (os|file|test)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您应用程序的密钥

## zetacored keys export

导出私钥

### 概要

从本地密钥环中以 ASCII 装甲加密格式导出一个私钥。

当同时选择 --unarmored-hex 和 --unsafe 标志时，加密私钥材料将以不安全的方式导出，旨在允许用户将密钥导入热钱包。此功能仅适用于高级用户，这些用户确信如何处理私钥工作并完全了解风险。如果您不确定，可能需要进行一些研究并以 ASCII 装甲加密格式导出您的密钥。

```
zetacored keys export [name] [flags]
```

### 选项

```
  -h, --help            导出命令的帮助信息
      --unarmored-hex   导出非装甲十六进制私钥。需要 --unsafe。
      --unsafe          启用不安全操作。此标志必须与所有不安全操作特定选项一起开启。
  -y, --yes             当导出非装甲十六进制私钥时跳过确认提示
```

### 从父命令继承的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端 (os|file|test)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序密钥

## zetacored keys import

将私钥导入到本地密钥库

### 概要

将一个 ASCII 编码的私钥导入到本地密钥库。

```
zetacored keys import [name] [keyfile] [flags]
```

### 选项

```
  -h, --help   关于 import 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string               应用程序主目录
      --keyring-backend string    选择密钥环的后端 (os|file|test)
      --keyring-dir string        客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string         日志格式 (json|plain)
      --log_level string          日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color              禁用彩色日志
      --output string             输出格式 (text|json)
      --trace                     出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您应用程序的密钥

## zetacored keys list

列出所有密钥

### 概要

返回此密钥管理器存储的所有公钥列表，包括其关联的名称和地址。

```
zetacored keys list [flags]
```

### 选项

```
  -h, --help         list 命令的帮助
  -n, --list-names   仅列出名称
```

### 从父命令继承的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端 (os|file|test)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序密钥

## zetacored keys list-key-types

列出所有密钥类型

### 概要

返回所有支持的密钥类型（也称为算法）的列表

```
zetacored keys list-key-types [flags]
```

### 选项

```
  -h, --help   列出 list-key-types 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端 (os|file|test)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序密钥

## zetacored keys migrate

将密钥从 Amino 序列化格式迁移至 Proto 序列化格式

### 概要

将密钥记录从 Amino 迁移至 Protocol Buffers 格式。
对于每个密钥材料条目，该命令会检查是否可以使用 proto 进行反序列化。
如果可以，说明该密钥已完成迁移，因此跳过并继续处理下一个条目。
否则，将尝试使用 Amino 将其反序列化为 LegacyInfo。如果此尝试成功，则将 LegacyInfo 序列化为 Protobuf 序列化格式并覆盖密钥环中的条目。如果发生任何错误，将在 CLI 中输出错误信息，并继续迁移直到密钥环数据库中的所有密钥处理完毕。
更多详细信息请参阅 https://github.com/cosmos/cosmos-sdk/pull/9695。

```
zetacored keys migrate [flags]
```

### 选项

```
  -h, --help   显示 migrate 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string               应用程序主目录
      --keyring-backend string    选择密钥环的后端 (os|file|test)
      --keyring-dir string        客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string         日志格式 (json|plain)
      --log_level string          日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color              禁用彩色日志
      --output string             输出格式 (text|json)
      --trace                     出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序密钥

## zetacored keys mnemonic

计算输入熵的 BIP39 助记词

### 概览

通过读取系统熵来创建 BIP39 助记词（有时称为种子短语）。要使用自己的熵，请使用 `--unsafe-entropy` 选项。

```
zetacored keys mnemonic [flags]
```

### 选项

```
  -h, --help             获取 mnemonic 命令的帮助信息
      --unsafe-entropy   提示用户提供自己的熵，而不是依赖系统熵
  -y, --yes              当检查输入熵长度时跳过确认提示
```

### 继承自父命令的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端 (os|file|test)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理应用程序的密钥

## zetacored keys parse

将地址从十六进制解析为 bech32 格式，反之亦然

### 概要

将密钥地址和指纹从十六进制格式转换为 bech32 cosmos 前缀格式并打印到标准输出，反之亦然。

```
zetacored keys parse [hex-or-bech32-address] [flags]
```

### 选项

```
-h, --help   parse 命令的帮助
```

### 从父命令继承的选项

```
      --home string               应用程序主目录
      --keyring-backend string    选择密钥环的后端 (os|file|test)
      --keyring-dir string        客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string         日志格式 (json|plain)
      --log_level string          日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color              禁用彩色日志
      --output string             输出格式 (text|json)
      --trace                     在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序的密钥

## zetacored keys rename

重命名现有密钥

### 概要

从 Keybase 后端重命名一个密钥。

请注意，重命名离线或 ledger 密钥只会重命名本地存储的公钥引用，即存储在 ledger 设备中的私钥无法通过 CLI 重命名。

```
zetacored keys rename [old_name] [new_name] [flags]
```

### 选项

```
  -h, --help   重命名命令的帮助信息
  -y, --yes    在重命名离线或 ledger 密钥引用时跳过确认提示
```

### 从父命令继承的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择钥匙环的后端 (os|file|test)
      --keyring-dir string       客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您的应用程序密钥

## zetacored keys show

通过名称或地址检索密钥信息

### 概要

显示密钥详情。如果提供多个名称或地址，则会创建一个名为 "multi" 的临时多签密钥，包含所有通过名称提供的密钥并设置多签阈值。

```
zetacored keys show [name_or_address [name_or_address...]] [flags]
```

### 选项

```
  -a, --address                  仅输出地址（不能与 --output 同时使用）
      --bech string              密钥的 Bech32 前缀编码（acc|val|cons）
  -d, --device                   输出硬件钱包设备中的地址（不能与 --pubkey 同时使用）
  -h, --help                     show 命令的帮助信息
      --multisig-threshold int   需要 K/N 个签名（默认值 1）
  -p, --pubkey                   仅输出公钥（不能与 --output 同时使用）
      --qrcode                   显示密钥地址的二维码（如果 -a 或 --address 为 false 则忽略此选项）
```

### 继承自父命令的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环后端（os|file|test）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式（json|plain）
      --log_level string         日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color             禁用彩色日志
      --output string            输出格式（text|json）
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理应用程序的密钥

## zetacored keys unsafe-export-eth-key

**UNSAFE** 导出一个以太坊私钥

### 概览

**UNSAFE** 导出一个未加密的以太坊私钥，用于开发工具

```
zetacored keys unsafe-export-eth-key [name] [flags]
```

### 选项

```
  -h, --help   获取关于 unsafe-export-eth-key 的帮助信息
```

### 从父命令继承的选项

```
      --home string               应用程序主目录
      --keyring-backend string    选择钥匙环的后端 (os|file|test)
      --keyring-dir string        客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --log_format string         日志格式 (json|plain)
      --log_level string          日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color              禁用彩色日志
      --output string             输出格式 (text|json)
      --trace                     出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您应用程序的钥匙

## zetacored keys unsafe-import-eth-key

**不安全** 将以太坊私钥导入到本地密钥库

### 概览

**不安全** 将一个十六进制编码的以太坊私钥导入到本地密钥库。

```
zetacored keys unsafe-import-eth-key [name] [pk] [flags]
```

### 选项

```
  -h, --help   关于 unsafe-import-eth-key 命令的帮助信息
```

### 继承自父命令的选项

```
      --home string              应用程序主目录
      --keyring-backend string   选择密钥环的后端 (os|file|test)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --output string            输出格式 (text|json)
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored keys](#zetacored-keys)	 - 管理您应用程序的密钥

## zetacored parse-genesis-file

解析提供的创世文件，并将所需数据导入到可选提供的创世文件中。

```
zetacored parse-genesis-file [import-genesis-file] [optional-genesis-file] [flags]
```

### 选项

```
  -h, --help     parse-genesis-file 命令的帮助
      --modify   在导入前修改创世文件
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored query

查询子命令

```
zetacored query [flags]
```

### 选项

```
      --chain-id string   网络链 ID
  -h, --help              查询命令的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）
* [zetacored query auth](#zetacored-query-auth)	 - auth 模块的查询命令
* [zetacored query authority](#zetacored-query-authority)	 - authority 模块的查询命令
* [zetacored query authz](#zetacored-query-authz)	 - authz 模块的查询命令
* [zetacored query bank](#zetacored-query-bank)	 - bank 模块的查询命令
* [zetacored query block](#zetacored-query-block)	 - 通过高度、哈希或事件查询已提交的区块
* [zetacored query block-results](#zetacored-query-block-results)	 - 通过高度查询已提交区块的结果
* [zetacored query blocks](#zetacored-query-blocks)	 - 查询匹配一组事件的分页区块
* [zetacored query comet-validator-set](#zetacored-query-comet-validator-set)	 - 获取指定高度的完整 CometBFT 验证器集
* [zetacored query consensus](#zetacored-query-consensus)	 - consensus 模块的查询命令
* [zetacored query crosschain](#zetacored-query-crosschain)	 - crosschain 模块的查询命令
* [zetacored query distribution](#zetacored-query-distribution)	 - distribution 模块的查询命令
* [zetacored query emissions](#zetacored-query-emissions)	 - emissions 模块的查询命令
* [zetacored query evidence](#zetacored-query-evidence)	 - evidence 模块的查询命令
* [zetacored query evm](#zetacored-query-evm)	 - evm 模块的查询命令
* [zetacored query feemarket](#zetacored-query-feemarket)	 - fee market 模块的查询命令
* [zetacored query fungible](#zetacored-query-fungible)	 - fungible 模块的查询命令
* [zetacored query gov](#zetacored-query-gov)	 - gov 模块的查询命令
* [zetacored query group](#zetacored-query-group)	 - group 模块的查询命令
* [zetacored query lightclient](#zetacored-query-lightclient)	 - lightclient 模块的查询命令
* [zetacored query observer](#zetacored-query-observer)	 - observer 模块的查询命令
* [zetacored query params](#zetacored-query-params)	 - params 模块的查询命令
* [zetacored query slashing](#zetacored-query-slashing)	 - slashing 模块的查询命令
* [zetacored query staking](#zetacored-query-staking)	 - staking 模块的查询命令
* [zetacored query tx](#zetacored-query-tx)	 - 通过哈希、"[addr]/[seq]" 组合或逗号分隔的签名查询已提交区块中的交易
* [zetacored query txs](#zetacored-query-txs)	 - 查询匹配一组事件的分页交易
* [zetacored query upgrade](#zetacored-query-upgrade)	 - upgrade 模块的查询命令

## zetacored query auth

认证模块的查询命令

```
zetacored query auth [flags]
```

### 选项

```
  -h, --help   auth 模块的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query auth account](#zetacored-query-auth-account)	 - 按地址查询账户
* [zetacored query auth account-info](#zetacored-query-auth-account-info)	 - 查询所有账户类型通用的账户信息
* [zetacored query auth accounts](#zetacored-query-auth-accounts)	 - 查询所有账户
* [zetacored query auth address-by-acc-num](#zetacored-query-auth-address-by-acc-num)	 - 按账户编号查询账户地址
* [zetacored query auth address-bytes-to-string](#zetacored-query-auth-address-bytes-to-string)	 - 将地址字节转换为字符串
* [zetacored query auth address-string-to-bytes](#zetacored-query-auth-address-string-to-bytes)	 - 将地址字符串转换为字节
* [zetacored query auth bech32-prefix](#zetacored-query-auth-bech32-prefix)	 - 查询链的 bech32 前缀（如果适用）
* [zetacored query auth module-account](#zetacored-query-auth-module-account)	 - 按模块名称查询模块账户信息
* [zetacored query auth module-accounts](#zetacored-query-auth-module-accounts)	 - 查询所有模块账户
* [zetacored query auth params](#zetacored-query-auth-params)	 - 查询当前认证参数

## zetacored query auth account

通过地址查询账户

```
zetacored query auth account [address] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     account 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query auth account-info

查询所有账户类型共有的账户信息。

```
zetacored query auth account-info [address] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     用于 account-info 的帮助
      --keyring-backend string   选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 用于认证模块的查询命令

## zetacored query auth accounts

查询所有账户

```
zetacored query auth accounts [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     accounts 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不对 JSON 输出进行缩进
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query auth address-by-acc-num

通过账户号码查询账户地址

```
zetacored query auth address-by-acc-num [acc-num] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     用于 address-by-acc-num 的帮助
      --id int                   
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query auth address-bytes-to-string

将地址字节转换为字符串

```
zetacored query auth address-bytes-to-string [address-bytes] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     address-bytes-to-string 的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query auth address-string-to-bytes

将地址字符串转换为字节

```
zetacored query auth address-string-to-bytes [address-string] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     address-string-to-bytes 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query auth bech32-prefix

查询链的 bech32 前缀（如果适用）

```
zetacored query auth bech32-prefix [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用指定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     bech32-prefix 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query auth module-account

通过模块名称查询模块账户信息。

```
zetacored query auth module-account [module-name] [flags]
```

### 示例

```
zetacored q auth module-account gov
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     module-account 命令的帮助
      --keyring-backend string   选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 查询认证模块的命令

## zetacored query auth module-accounts

查询所有模块账户

```
zetacored query auth module-accounts [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道进行 gRPC 通信，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                     module-accounts 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query auth params

查询当前的认证参数

```
zetacored query auth params [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     params 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query auth](#zetacored-query-auth)	 - 认证模块的查询命令

## zetacored query authority

权威模块的查询命令

```
zetacored query authority [flags]
```

### 选项

```
  -h, --help   权威模块的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query authority list-authorizations](#zetacored-query-authority-list-authorizations)	 - 列出所有授权
* [zetacored query authority show-authorization](#zetacored-query-authority-show-authorization)	 - 显示给定消息 URL 的授权
* [zetacored query authority show-chain-info](#zetacored-query-authority-show-chain-info)	 - 显示链信息
* [zetacored query authority show-policies](#zetacored-query-authority-show-policies)	 - 显示策略

## zetacored query authority list-authorizations

列出所有授权

```
zetacored query authority list-authorizations [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               list-authorizations 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query authority](#zetacored-query-authority)	 - 授权模块的查询命令

## zetacored query authority show-authorization

显示给定消息 URL 的授权

```
zetacored query authority show-authorization [msg-url] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               show-authorization 命令的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query authority](#zetacored-query-authority)	 - 权威模块的查询命令

## zetacored query authority show-chain-info

显示链信息

```
zetacored query authority show-chain-info [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               显示 show-chain-info 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query authority](#zetacored-query-authority)	 - 权威模块的查询命令

## zetacored query authority show-policies

显示策略

```
zetacored query authority show-policies [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用指定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               显示 show-policies 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query authority](#zetacored-query-authority)	 - 权限模块的查询命令

## zetacored query authz

查询 authz 模块的命令

```
zetacored query authz [flags]
```

### 选项

```
-h, --help   authz 的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query authz grants](#zetacored-query-authz-grants)	 - 查询授予者-被授予者对的授权，并可选择消息类型 URL
* [zetacored query authz grants-by-grantee](#zetacored-query-authz-grants-by-grantee)	 - 查询授予被授予者的授权
* [zetacored query authz grants-by-granter](#zetacored-query-authz-grants-by-granter)	 - 查询由授予者授权的授权

## zetacored query authz grants

查询 granter-grantee 对的授权授予，并可选择指定 msg-type-url

### 概要

查询 granter-grantee 对的授权授予。如果设置了 msg-type-url，则仅选择该消息类型的授权。

```
zetacored query authz grants [granter-addr] [grantee-addr] [msg-type-url] [flags]
```

### 示例

```
zetacored query authz grants cosmos1skj.. cosmos1skjwj.. /cosmos.bank.v1beta1.MsgSend
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     获取 grants 命令的帮助
      --keyring-backend string   选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端 Keyring 目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query authz](#zetacored-query-authz)	 - authz 模块的查询命令

## zetacored query authz grants-by-grantee

查询授予被授权方的授权许可

```
zetacored query authz grants-by-grantee [grantee-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果不设置此项，服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                     grants-by-grantee 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query authz](#zetacored-query-authz)	 - authz 模块的查询命令

## zetacored query authz grants-by-granter

查询由授权者授予的授权许可

```
zetacored query authz grants-by-granter [granter-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                     grants-by-granter 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query authz](#zetacored-query-authz)	 - 查询 authz 模块的命令

## zetacored query bank

银行模块的查询命令

```
zetacored query bank [flags]
```

### 选项

```
  -h, --help   获取 bank 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query bank balance](#zetacored-query-bank-balance)	 - 通过地址和面额查询账户余额
* [zetacored query bank balances](#zetacored-query-bank-balances)	 - 通过地址查询账户余额
* [zetacored query bank denom-metadata](#zetacored-query-bank-denom-metadata)	 - 查询给定硬币面额的客户端元数据
* [zetacored query bank denom-metadata-by-query-string](#zetacored-query-bank-denom-metadata-by-query-string)	 - 执行 DenomMetadataByQueryString RPC 方法
* [zetacored query bank denom-owners](#zetacored-query-bank-denom-owners)	 - 查询拥有特定代币面额的所有账户地址
* [zetacored query bank denom-owners-by-query](#zetacored-query-bank-denom-owners-by-query)	 - 执行 DenomOwnersByQuery RPC 方法
* [zetacored query bank denoms-metadata](#zetacored-query-bank-denoms-metadata)	 - 查询所有已注册硬币面额的客户端元数据
* [zetacored query bank params](#zetacored-query-bank-params)	 - 查询当前银行参数
* [zetacored query bank send-enabled](#zetacored-query-bank-send-enabled)	 - 查询发送启用条目
* [zetacored query bank spendable-balance](#zetacored-query-bank-spendable-balance)	 - 查询单个账户的单个面额可用余额
* [zetacored query bank spendable-balances](#zetacored-query-bank-spendable-balances)	 - 通过地址查询账户可用余额
* [zetacored query bank total-supply](#zetacored-query-bank-total-supply)	 - 查询链上硬币的总供应量
* [zetacored query bank total-supply-of](#zetacored-query-bank-total-supply-of)	 - 查询单个硬币面额的供应量

## zetacored query bank balance

通过地址和面额查询账户余额

```
zetacored query bank balance [address] [denom] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果服务器未使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     余额命令的帮助
      --keyring-backend string   选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank balances

按地址查询账户余额

### 概要

查询账户的总余额或特定面额的余额。

```
zetacored query bank balances [address] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果不指定则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     balances 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
      --resolve-denom            
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank denom-metadata

查询指定币种单位的客户端元数据

```
zetacored query bank denom-metadata [denom] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     denom-metadata 命令帮助
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank denom-metadata-by-query-string

执行 DenomMetadataByQueryString RPC 方法

```
zetacored query bank denom-metadata-by-query-string [flags]
```

### 选项

```
      --denom string              代币名称
      --grpc-addr string          用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道使用 gRPC，若不设置则服务器必须使用 TLS
      --height int                查询特定高度的状态（如果节点正在裁剪状态，可能会出错）
  -h, --help                      denom-metadata-by-query-string 命令的帮助信息
      --keyring-backend string    选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string        客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不缩进 JSON 输出
      --node string               此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string             输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string           网络链 ID
      --home string               配置和数据目录
      --log_format string         日志格式 (json|plain)
      --log_level string          日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color              禁用彩色日志
      --trace                     出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank denom-owners

查询所有拥有特定代币面额的账户地址。

```
zetacored query bank denom-owners [denom] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     denom-owners 的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank denom-owners-by-query

执行 DenomOwnersByQuery RPC 方法

```
zetacored query bank denom-owners-by-query [flags]
```

### 选项

```
      --denom string             
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     denom-owners-by-query 的帮助信息
      --keyring-backend string   选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式（text|json）
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank denoms-metadata

查询所有已注册币种面额的客户端元数据

```
zetacored query bank denoms-metadata [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                     denoms-metadata 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank params

查询当前银行参数。

```
zetacored query bank params [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     params 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank send-enabled

查询已启用的发送条目

### 概要

查询已特别设置的启用发送条目。

要查找一个或更多特定面额，请将它们作为参数提供给此命令。  
要查找所有面额，请不要提供任何参数。

```
zetacored query bank send-enabled [denom1 ...] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     send-enabled 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank spendable-balance

查询单个账户的特定面额代币的可花费余额。

```
zetacored query bank spendable-balance [address] [denom] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     spendable-balance 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank spendable-balances

按地址查询账户可消费余额

```
zetacored query bank spendable-balances [address] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int                查询状态的特定高度（如果节点正在修剪状态，则可能出错）
  -h, --help                      spendable-balances 命令的帮助信息
      --keyring-backend string    选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string        客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不缩进 JSON 输出
      --node string               此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string             输出格式 (text|json)
      --page-count-total          
      --page-key binary           
      --page-limit uint           
      --page-offset uint          
      --page-reverse              
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank total-supply

查询链上代币的总供应量

### 概要

查询链上账户持有的代币总供应量。要查询特定代币面额的总供应量，请使用 `--denom` 标志。

```
zetacored query bank total-supply [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     total-supply 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query bank total-supply-of

查询单个币种面额的总供应量

```
zetacored query bank total-supply-of [denom] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               用于查询状态的特定区块高度（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     获取 total-supply-of 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query bank](#zetacored-query-bank)	 - 银行模块的查询命令

## zetacored query block

通过高度、哈希或事件查询已提交的区块

### 概要

使用 CometBFT RPC 的 `block` 和 `block_by_hash` 方法查询特定的已提交区块

```
zetacored query block --type=[height|hash] [height|hash] [flags]
```

### 示例

```
$ zetacored query block --type=height [height]
$ zetacored query block --type=hash [hash]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         使用特定高度查询状态（若节点正在修剪状态，此操作可能报错）
  -h, --help               block 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口] 
  -o, --output string      输出格式 (text|json) 
      --type string        查询交易时使用的类型，可为 "height" 或 "hash" 
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录 
      --log_format string  日志格式 (json|plain) 
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令

## zetacored query block-results

通过高度查询已提交区块的结果

### 概要

使用 CometBFT RPC 的 `block_results` 方法查询特定已提交区块的结果。

```
zetacored query block-results [height] [flags]
```

### 选项

```
      --grpc-addr string   the gRPC endpoint to use for this chain
      --grpc-insecure      allow gRPC over insecure channels, if not the server must use TLS
      --height int         Use a specific height to query state at (this can error if the node is pruning state)
  -h, --help               help for block-results
      --node string        [host]:[port] to CometBFT RPC interface for this chain 
  -o, --output string      Output format (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令

## zetacored query blocks

查询匹配一组事件的分页区块

### 概要

搜索与给定事件完全匹配的区块，其中结果分页显示。  
事件查询直接传递给 CometBFT 的 RPC BlockSearch 方法，并且必须符合 CometBFT 的查询语法。  
请参考每个模块的文档以获取要查询的完整事件集。  
每个模块在 `xx_events.md` 下记录其相应的事件。

```
zetacored query blocks [flags]
```

### 示例

```
$ zetacored query blocks --query "message.sender='cosmos1...' AND block.height > 7" --page 1 --limit 30 --order_by asc
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               blocks 命令的帮助
      --limit int          每页返回的交易结果数量（默认 100）
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
      --order_by string    排序语义（asc|dsc）
  -o, --output string      输出格式（text|json）
      --page int           查询分页结果的特定页面（默认 1）
      --query string       根据 CometBFT 查询语义的区块事件查询
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令

## zetacored query comet-validator-set

获取指定高度的完整 CometBFT 验证器集

```
zetacored query comet-validator-set [height] [flags]
```

### 选项

```
  -h, --help            comet-validator-set 命令的帮助信息
      --limit int       每页返回的查询结果数量（默认 100）
      --node string     指向此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string   输出格式（text|json）
      --page int        查询分页结果的特定页面（默认 1）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令

## zetacored query consensus

用于查询共识模块的命令

```
zetacored query consensus [flags]
```

### 选项

```
  -h, --help   有关 consensus 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志记录格式 (json|plain)
      --log_level string    日志记录级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query consensus comet](#zetacored-query-consensus-comet)	 - 用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令
* [zetacored query consensus params](#zetacored-query-consensus-params)	 - 查询当前共识参数

## zetacored query consensus comet

用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令

```
zetacored query consensus comet [flags]
```

### 选项

```
  -h, --help   comet 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus](#zetacored-query-consensus) - 共识模块的查询命令
* [zetacored query consensus comet block-by-height](#zetacored-query-consensus-comet-block-by-height) - 按高度查询已提交的区块
* [zetacored query consensus comet block-latest](#zetacored-query-consensus-comet-block-latest) - 查询最新的已提交区块
* [zetacored query consensus comet node-info](#zetacored-query-consensus-comet-node-info) - 查询当前节点信息
* [zetacored query consensus comet syncing](#zetacored-query-consensus-comet-syncing) - 查询节点同步状态
* [zetacored query consensus comet validator-set](#zetacored-query-consensus-comet-validator-set) - 查询最新的验证器集
* [zetacored query consensus comet validator-set-by-height](#zetacored-query-consensus-comet-validator-set-by-height) - 按高度查询验证器集

## zetacored query consensus comet block-by-height

通过高度查询已提交的区块

### 概要

使用 CometBFT RPC `block_by_height` 方法查询特定的已提交区块

```
zetacored query consensus comet block-by-height [height] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     block-by-height 命令的帮助
      --keyring-backend string   选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus comet](#zetacored-query-consensus-comet)	 - 用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令

## zetacored query consensus comet block-latest

查询最新提交的区块

```
zetacored query consensus comet block-latest [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     block-latest 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         用于配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus comet](#zetacored-query-consensus-comet)	 - 用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令

## zetacored query consensus comet node-info

查询当前节点信息

```
zetacored query consensus comet node-info [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     node-info 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus comet](#zetacored-query-consensus-comet)	 - 用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令

## zetacored query consensus comet syncing

查询节点同步状态

```
zetacored query consensus comet syncing [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     获取同步帮助
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus comet](#zetacored-query-consensus-comet)	 - 用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令

## zetacored query consensus comet validator-set

查询最新的验证器集

```
zetacored query consensus comet validator-set [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     validator-set 的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
      --page-count-total
      --page-key binary
      --page-limit uint
      --page-offset uint
      --page-reverse
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus comet](#zetacored-query-consensus-comet)	 - 用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令

## zetacored query consensus comet validator-set-by-height

按高度查询验证器集

```
zetacored query consensus comet validator-set-by-height [height] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     validator-set-by-height 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus comet](#zetacored-query-consensus-comet)	 - 用于 cosmos.base.tendermint.v1beta1.Service 服务的查询命令

## zetacored query consensus params

查询当前共识参数

```
zetacored query consensus params [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     params 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query consensus](#zetacored-query-consensus)	 - 共识模块的查询命令

## zetacored query crosschain

跨链模块的查询命令

```
zetacored query crosschain [flags]
```

### 选项

```
  -h, --help   针对 crosschain 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query) - 查询子命令
* [zetacored query crosschain get-zeta-accounting](#zetacored-query-crosschain-get-zeta-accounting) - 查询 zeta 会计
* [zetacored query crosschain inbound-hash-to-cctx-data](#zetacored-query-crosschain-inbound-hash-to-cctx-data) - 从入站哈希查询 CCTX 数据
* [zetacored query crosschain last-zeta-height](#zetacored-query-crosschain-last-zeta-height) - 查询最后一个 Zeta 高度
* [zetacored query crosschain list-all-inbound-trackers](#zetacored-query-crosschain-list-all-inbound-trackers) - 显示所有入站追踪器
* [zetacored query crosschain list-cctx](#zetacored-query-crosschain-list-cctx) - 列出所有 CCTX
* [zetacored query crosschain list-gas-price](#zetacored-query-crosschain-list-gas-price) - 列出所有 gasPrice
* [zetacored query crosschain list-inbound-hash-to-cctx](#zetacored-query-crosschain-list-inbound-hash-to-cctx) - 列出所有 inboundHashToCctx
* [zetacored query crosschain list-inbound-tracker](#zetacored-query-crosschain-list-inbound-tracker) - 按 chainId 显示入站追踪器列表
* [zetacored query crosschain list-outbound-tracker](#zetacored-query-crosschain-list-outbound-tracker) - 列出所有出站追踪器
* [zetacored query crosschain list-pending-cctx](#zetacored-query-crosschain-list-pending-cctx) - 显示待处理的 CCTX
* [zetacored query crosschain list_pending_cctx_within_rate_limit](#zetacored-query-crosschain-list-pending-cctx-within-rate-limit) - 列出速率限制内的所有待处理 CCTX
* [zetacored query crosschain show-cctx](#zetacored-query-crosschain-show-cctx) - 显示一个 CCTX
* [zetacored query crosschain show-gas-price](#zetacored-query-crosschain-show-gas-price) - 显示一个 gasPrice
* [zetacored query crosschain show-inbound-hash-to-cctx](#zetacored-query-crosschain-show-inbound-hash-to-cctx) - 显示一个 inboundHashToCctx
* [zetacored query crosschain show-inbound-tracker](#zetacored-query-crosschain-show-inbound-tracker) - 按 chainID 和 txHash 显示入站追踪器
* [zetacored query crosschain show-outbound-tracker](#zetacored-query-crosschain-show-outbound-tracker) - 显示一个出站追踪器
* [zetacored query crosschain show-rate-limiter-flags](#zetacored-query-crosschain-show-rate-limiter-flags) - 显示速率限制器标志

## zetacored query crosschain get-zeta-accounting

查询 zeta 会计

```
zetacored query crosschain get-zeta-accounting [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               get-zeta-accounting 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain inbound-hash-to-cctx-data

通过入向哈希查询 CCTX 数据

```
zetacored query crosschain inbound-hash-to-cctx-data [inbound-hash] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过非安全通道进行 gRPC 通信，若不指定则服务器必须使用 TLS
      --height int         查询特定高度的状态（若节点正在修剪状态，此操作可能会报错）
  -h, --help               inbound-hash-to-cctx-data 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain last-zeta-height

查询最新的 Zeta 区块高度

```
zetacored query crosschain last-zeta-height [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               有关 last-zeta-height 的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain list-all-inbound-trackers

显示所有入站追踪器

```
zetacored query crosschain list-all-inbound-trackers [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，如果不指定则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help               列出所有入站追踪器的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 继承自父命令的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain list-cctx

列出所有 CCTX

```
zetacored query crosschain list-cctx [flags]
```

### 选项

```
      --count-total        统计 list-cctx 中的记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               获取 list-cctx 命令的帮助信息
      --limit uint         list-cctx 的查询分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
      --offset uint        list-cctx 的查询分页偏移量
  -o, --output string      输出格式 (text|json)
      --page uint          list-cctx 的查询分页页码。这将设置偏移量为限制的倍数（默认 1）
      --page-key string    list-cctx 的查询分页页面键
      --reverse            按降序排序结果
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain list-gas-price

列出所有 gasPrice

```
zetacored query crosschain list-gas-price [flags]
```

### 选项

```
      --count-total        统计 list-gas-price 中记录的总数以进行查询
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               list-gas-price 的帮助信息
      --limit uint         list-gas-price 的分页限制以进行查询（默认 100）
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
      --offset uint        list-gas-price 的分页偏移以进行查询
  -o, --output string      输出格式 (text|json)
      --page uint          list-gas-price 的分页页码以进行查询。这将偏移设置为限制的倍数（默认 1）
      --page-key string    list-gas-price 的分页页面键以进行查询
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 用于 crosschain 模块的查询命令

## zetacored query crosschain list-inbound-hash-to-cctx

列出所有 inboundHashToCctx

```
zetacored query crosschain list-inbound-hash-to-cctx [flags]
```

### 选项

```
      --count-total        统计要查询的 list-inbound-hash-to-cctx 中的记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               关于 list-inbound-hash-to-cctx 的帮助信息
      --limit uint         要查询的 list-inbound-hash-to-cctx 的分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口的 [主机]:[端口] 
      --offset uint        要查询的 list-inbound-hash-to-cctx 的分页偏移量
  -o, --output string      输出格式（text|json） 
      --page uint          要查询的 list-inbound-hash-to-cctx 的分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string    要查询的 list-inbound-hash-to-cctx 的分页页面键
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录 
      --log_format string  日志格式（json|plain） 
      --log_level string   日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'） 
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 用于 crosschain 模块的查询命令

## zetacored query crosschain list-inbound-tracker

按 chainId 显示入站跟踪器列表

```
zetacored query crosschain list-inbound-tracker [chainId] [flags]
```

### 选项

```
      --count-total        统计 list-inbound-tracker [chainId] 中的记录总数以供查询
      --grpc-addr string  用于此链的 gRPC 端点
      --grpc-insecure     允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int        使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help              list-inbound-tracker 的帮助
      --limit uint        list-inbound-tracker [chainId] 的分页限制以供查询（默认 100）
      --node string       此链的 CometBFT RPC 接口的 [host]:[port] 
      --offset uint       list-inbound-tracker [chainId] 的分页偏移量以供查询
  -o, --output string     输出格式（text|json） 
      --page uint         list-inbound-tracker [chainId] 的分页页码以供查询。这将偏移量设置为限制的倍数（默认 1）
      --page-key string   list-inbound-tracker [chainId] 的分页页面键以供查询
      --reverse           结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式（json|plain） 
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'） 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 用于跨链模块的查询命令

## zetacored query crosschain list-outbound-tracker

列出所有出站追踪器

```
zetacored query crosschain list-outbound-tracker [flags]
```

### 选项

```
      --count-total         统计 list-outbound-tracker 中的记录总数
      --grpc-addr string    用于此链的 gRPC 端点
      --grpc-insecure       允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int          使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                获取 list-outbound-tracker 命令的帮助信息
      --limit uint          list-outbound-tracker 的查询分页限制（默认值：100）
      --node string         此链的 CometBFT RPC 接口 [host]:[port]
      --offset uint         list-outbound-tracker 的查询分页偏移量
  -o, --output string       输出格式（text|json）
      --page uint           list-outbound-tracker 的查询分页页码。这将把偏移量设置为限制的倍数（默认值：1）
      --page-key string     list-outbound-tracker 的查询分页页面键
      --reverse             按降序排序结果
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain list-pending-cctx

显示待处理的 CCTX

```
zetacored query crosschain list-pending-cctx [chain-id] [limit] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道进行 gRPC 通信，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               list-pending-cctx 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 参见

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 用于跨链模块的查询命令

## zetacored query crosschain list_pending_cctx_within_rate_limit

列出所有在速率限制内的待处理 CCTX

```
zetacored query crosschain list_pending_cctx_within_rate_limit [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许在不安全通道上使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               有关 list_pending_cctx_within_rate_limit 的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 用于跨链模块的查询命令

## zetacored query crosschain show-cctx

显示一个 CCTX

```
zetacored query crosschain show-cctx [index] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               show-cctx 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain show-gas-price

显示燃料价格

```
zetacored query crosschain show-gas-price [index] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道进行 gRPC 通信，否则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help               show-gas-price 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain show-inbound-hash-to-cctx

显示一个 inboundHashToCctx

```
zetacored query crosschain show-inbound-hash-to-cctx [inbound-hash] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               显示 show-inbound-hash-to-cctx 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 用于跨链模块的查询命令

## zetacored query crosschain show-inbound-tracker

通过 chainID 和 txHash 显示入站追踪器。

```
zetacored query crosschain show-inbound-tracker [chainID] [txHash] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               显示 show-inbound-tracker 的帮助信息
      --node string        [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain show-outbound-tracker

显示出站追踪器信息

```
zetacored query crosschain show-outbound-tracker [chainId] [nonce] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help               显示 show-outbound-tracker 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 跨链模块的查询命令

## zetacored query crosschain show-rate-limiter-flags

显示速率限制器标志

```
zetacored query crosschain show-rate-limiter-flags [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               帮助信息，用于 show-rate-limiter-flags
      --node string        连接到该链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query crosschain](#zetacored-query-crosschain)	 - 查询跨链模块的命令

## zetacored query distribution

分发模块的查询命令

```
zetacored query distribution [flags]
```

### 选项

```
  -h, --help   获取 distribution 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query distribution commission](#zetacored-query-distribution-commission)	 - 查询分发验证者佣金
* [zetacored query distribution community-pool](#zetacored-query-distribution-community-pool)	 - 查询社区池中的代币数量
* [zetacored query distribution delegator-validators](#zetacored-query-distribution-delegator-validators)	 - 执行 DelegatorValidators RPC 方法
* [zetacored query distribution delegator-withdraw-address](#zetacored-query-distribution-delegator-withdraw-address)	 - 执行 DelegatorWithdrawAddress RPC 方法
* [zetacored query distribution params](#zetacored-query-distribution-params)	 - 查询当前分发参数
* [zetacored query distribution rewards](#zetacored-query-distribution-rewards)	 - 查询所有分发委托者奖励
* [zetacored query distribution rewards-by-validator](#zetacored-query-distribution-rewards-by-validator)	 - 查询来自特定验证者的所有分发委托者
* [zetacored query distribution slashes](#zetacored-query-distribution-slashes)	 - 查询分发验证者罚没记录
* [zetacored query distribution validator-distribution-info](#zetacored-query-distribution-validator-distribution-info)	 - 查询验证者分发信息
* [zetacored query distribution validator-outstanding-rewards](#zetacored-query-distribution-validator-outstanding-rewards)	 - 查询验证者及其所有委托的未提取分发奖励

## zetacored query distribution commission

查询分发给验证者的佣金

```
zetacored query distribution commission [validator] [flags]
```

### 示例

```
$ zetacored query distribution commission [validator-address]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果不设置此项则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     commission 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 继承自父命令的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分发模块的查询命令

## zetacored query distribution community-pool

查询社区池中的代币数量

```
zetacored query distribution community-pool [flags]
```

### 示例

```
$ zetacored query distribution community-pool
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     community-pool 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分发模块的查询命令

## zetacored query distribution delegator-validators

执行 DelegatorValidators RPC 方法

```
zetacored query distribution delegator-validators [flags]
```

### 选项

```
      --delegator-address account address or key name    委托人的账户地址或密钥名称
      --grpc-addr string                                用于此链的 gRPC 端点
      --grpc-insecure                                   允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int                                      使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                                            delegator-validators 命令的帮助信息
      --keyring-backend string                          选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string                              客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                                       不缩进 JSON 输出
      --node string                                     此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string                                   输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分发模块的查询命令

## zetacored query distribution delegator-withdraw-address

执行 DelegatorWithdrawAddress RPC 方法

```
zetacored query distribution delegator-withdraw-address [flags]
```

### 选项

```
      --delegator-address account address or key name   
      --grpc-addr string                                用于此链的 gRPC 端点
      --grpc-insecure                                   允许通过不安全通道使用 gRPC，如果未设置则服务器必须使用 TLS
      --height int                                      使用特定高度查询状态（如果节点正在修剪状态，则可能报错）
  -h, --help                                            delegator-withdraw-address 命令的帮助信息
      --keyring-backend string                          选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string                              客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                                       不缩进 JSON 输出
      --node string                                     此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string                                   输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string                                 网络链 ID
      --home string                                     配置和数据的目录
      --log_format string                               日志格式（json|plain）
      --log_level string                                日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                                    禁用彩色日志
      --trace                                           出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分发模块的查询命令

## zetacored query distribution params

查询当前的分配参数。

```
zetacored query distribution params [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     params 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 参见

* [zetacored query distribution](#zetacored-query-distribution)	 - 分配模块的查询命令

## zetacored query distribution rewards

查询所有分发委托者奖励

### 摘要

查询委托者获得的所有奖励

```
zetacored query distribution rewards [delegator-addr] [flags]
```

### 示例

```
$ zetacored query distribution rewards [delegator-address]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     获取 rewards 命令的帮助
      --keyring-backend string   选择钥匙环的后端（os|file|kwallet|pass|test|memory） 
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port] 
  -o, --output string            输出格式（text|json） 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式（json|plain） 
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'） 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 查询分发模块的命令

## zetacored query distribution rewards-by-validator

查询来自特定验证者的所有分配委托者奖励

```
zetacored query distribution rewards-by-validator [delegator-addr] [validator-addr] [flags]
```

### 示例

```
$ zetacored query distribution rewards [delegator-address] [validator-address]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     rewards-by-validator 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分配模块的查询命令

## zetacored query distribution slashes

查询分发模块的验证者罚没记录

```
zetacored query distribution slashes [validator] [start-height] [end-height] [flags]
```

### 示例

```
$ zetacored query distribution slashes [validator-address] 0 100
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int                查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                      slashes 命令的帮助信息
      --keyring-backend string    选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string        客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不缩进 JSON 输出
      --node string               此链的 CometBFT RPC 接口 [host]:[port] 
  -o, --output string             输出格式 (text|json) 
      --page-count-total          
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分发模块的查询命令

## zetacored query distribution validator-distribution-info

查询验证者分布信息

```
zetacored query distribution validator-distribution-info [validator] [flags]
```

### 示例

```
示例：$ zetacored query distribution validator-distribution-info [validator-address]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     validator-distribution-info 的帮助信息
      --keyring-backend string   选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端 Keyring 目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              连接到该链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分布模块的查询命令

## zetacored query distribution validator-outstanding-rewards

查询分发模块中验证者及其所有委托的未提取（未撤回）奖励

```
zetacored query distribution validator-outstanding-rewards [validator] [flags]
```

### 示例

```
$ zetacored query distribution validator-outstanding-rewards [validator-address]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     validator-outstanding-rewards 命令的帮助信息
      --keyring-backend string   选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query distribution](#zetacored-query-distribution)	 - 分发模块的查询命令

## zetacored query emissions

排放模块的查询命令

```
zetacored query emissions [flags]
```

### 选项

```
  -h, --help   help for emissions
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query emissions list-pool-addresses](#zetacored-query-emissions-list-pool-addresses)	 - 查询 list-pool-addresses
* [zetacored query emissions params](#zetacored-query-emissions-params)	 - 显示模块的参数
* [zetacored query emissions show-available-emissions](#zetacored-query-emissions-show-available-emissions)	 - 查询 show-available-emissions

## zetacored query emissions list-pool-addresses

查询 list-pool-addresses

```
zetacored query emissions list-pool-addresses [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               list-pool-addresses 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query emissions](#zetacored-query-emissions)	 - 用于 emissions 模块的查询命令

## zetacored query emissions params

显示模块的参数

```
zetacored query emissions params [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               params 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query emissions](#zetacored-query-emissions)	 - 用于 emissions 模块的查询命令

## zetacored query emissions show-available-emissions

查询 show-available-emissions

```
zetacored query emissions show-available-emissions [address] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               显示 show-available-emissions 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query emissions](#zetacored-query-emissions)	 - 用于 emissions 模块的查询命令

## zetacored query evidence

证据模块的查询命令

```
zetacored query evidence [flags]
```

### 选项

```
  -h, --help   获取 evidence 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query evidence evidence](#zetacored-query-evidence-evidence)	 - 根据哈希值查询证据
* [zetacored query evidence list](#zetacored-query-evidence-list)	 - 查询所有（分页）已提交的证据

## zetacored query evidence evidence

通过哈希查询证据

```
zetacored query evidence evidence [hash] [flags]
```

### 示例

```
zetacored query evidence evidence DF0C23E8634E480F84B9D5674A7CDC9816466DEC28A3358F73260F68D28D7660
```

### 选项

```
      --evidence-hash binary     
      --grpc-addr string         the gRPC endpoint to use for this chain
      --grpc-insecure            allow gRPC over insecure channels, if not the server must use TLS
      --height int               Use a specific height to query state at (this can error if the node is pruning state)
  -h, --help                     help for evidence
      --keyring-backend string   Select keyring's backend (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       The client Keyring directory; if omitted, the default 'home' directory will be used
      --no-indent                Do not indent JSON output
      --node string              [host]:[port] to CometBFT RPC interface for this chain 
  -o, --output string            Output format (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored query evidence](#zetacored-query-evidence)	 - 证据模块的查询命令

## zetacored query evidence list

查询所有（分页）已提交的证据

```
zetacored query evidence list [flags]
```

### 示例

```
zetacored query evidence list --page=2 --page-limit=50
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道进行 gRPC 通信，否则服务器必须使用 TLS
      --height int                查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                      list 命令的帮助信息
      --keyring-backend string    选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string        客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不缩进 JSON 输出
      --node string               此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string             输出格式 (text|json) 
      --page-count-total          
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evidence](#zetacored-query-evidence)	 - 证据模块的查询命令

## zetacored query evm

用于查询 evm 模块的命令

```
zetacored query evm [flags]
```

### 选项

```
  -h, --help   显示 evm 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query evm 0x-to-bech32](#zetacored-query-evm-0x-to-bech32)	 - 获取给定 0x 地址对应的 bech32 地址
* [zetacored query evm account](#zetacored-query-evm-account)	 - 从地址获取账户信息
* [zetacored query evm balance-bank](#zetacored-query-evm-balance-bank)	 - 获取给定 0x 地址和银行代币的银行余额
* [zetacored query evm balance-erc20](#zetacored-query-evm-balance-erc20)	 - 获取给定 0x 地址和 erc20 地址的 ERC20 余额
* [zetacored query evm bech32-to-0x](#zetacored-query-evm-bech32-to-0x)	 - 获取给定 bech32 地址对应的 0x 地址
* [zetacored query evm code](#zetacored-query-evm-code)	 - 从账户获取代码
* [zetacored query evm config](#zetacored-query-evm-config)	 - 获取 evm 配置
* [zetacored query evm params](#zetacored-query-evm-params)	 - 获取 evm 参数
* [zetacored query evm storage](#zetacored-query-evm-storage)	 - 在指定高度获取账户的存储数据

## zetacored query evm 0x-to-bech32

获取给定 0x 地址的 bech32 地址

### 概要

获取给定 0x 地址的 bech32 地址。

```
zetacored query evm 0x-to-bech32 [flags]
```

### 示例

```
evmd query evm 0x-to-bech32 0x7cB61D4117AE31a12E393a1Cfa3BaC666481D02E
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               0x-to-bech32 的帮助信息
      --node string        [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - 用于 evm 模块的查询命令

## zetacored query evm account

从地址获取账户信息。

### 概要

从地址获取账户信息。如果未提供高度，它将使用上下文中的最新高度。

```
zetacored query evm account ADDRESS [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               account 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string     输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - evm 模块的查询命令

## zetacored query evm balance-bank

获取给定 0x 地址和银行代币单位的银行余额

### 概要

获取给定 0x 地址和银行代币单位的银行余额。

```
zetacored query evm balance-bank [address] [denom] [flags]
```

### 示例

```
evmd query evm balance-bank 0xA2A8B87390F8F2D188242656BFb6852914073D06 atoken
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               balance-bank 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - evm 模块的查询命令

## zetacored query evm balance-erc20

查询指定 0x 地址和 ERC20 地址的 ERC20 余额

### 概要

查询指定 0x 地址和 ERC20 地址的 ERC20 余额。

```
zetacored query evm balance-erc20 [address] [erc20-address] [flags]
```

### 示例

```
evmd query evm balance-erc20 0xA2A8B87390F8F2D188242656BFb6852914073D06 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               balance-erc20 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - 用于 evm 模块的查询命令

## zetacored query evm bech32-to-0x

获取给定 bech32 地址的 0x 地址

### 概要

获取给定 bech32 地址的 0x 地址。

```
zetacored query evm bech32-to-0x [flags]
```

### 示例

```
evmd query evm bech32-to-0x cosmos10jmp6sgh4cc6zt3e8gw05wavvejgr5pwsjskvv
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               bech32-to-0x 的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - 查询 evm 模块的命令

## zetacored query evm code

获取账户代码

### 概要

从账户获取代码。如果未提供高度参数，将使用上下文中的最新高度。

```
zetacored query evm code ADDRESS [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过非安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help               关于 code 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口地址 [host]:[port]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - evm 模块的查询命令

## zetacored query evm config

获取 EVM 配置

### 概要

获取 EVM 配置值。

```
zetacored query evm config [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               针对 config 命令的帮助信息
      --node string        用于此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - 用于 EVM 模块的查询命令

## zetacored query evm params

获取 EVM 参数

### 概要

获取 EVM 参数值。

```
zetacored query evm params [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许在不安全通道上使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               params 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - EVM 模块的查询命令

## zetacored query evm storage

获取账户在给定键和高度下的存储。

### 概要

获取账户在给定键和高度下的存储。如果未提供高度，它将使用上下文中的最新高度。

```
zetacored query evm storage ADDRESS KEY [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               storage 命令的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query evm](#zetacored-query-evm)	 - 查询 evm 模块的命令

## zetacored query feemarket

费用市场模块的查询命令

```
zetacored query feemarket [flags]
```

### 选项

```
  -h, ---help   feemarket 的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query feemarket base-fee](#zetacored-query-feemarket-base-fee)	 - 获取指定区块高度的基础费用金额
* [zetacored query feemarket block-gas](#zetacored-query-feemarket-block-gas)	 - 获取指定区块高度的区块燃气使用量
* [zetacored query feemarket params](#zetacored-query-feemarket-params)	 - 获取费用市场参数

## zetacored query feemarket base-fee

获取指定区块高度的基础费用金额

### 摘要

获取指定区块高度的基础费用金额。
如果未提供高度参数，将使用上下文中的最新区块高度。

```
zetacored query feemarket base-fee [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help               获取 base-fee 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query feemarket](#zetacored-query-feemarket)	 - 费用市场模块的查询命令

## zetacored query feemarket block-gas

获取指定区块高度使用的区块燃料量

### 概要

获取指定区块高度使用的区块燃料量。
如果未提供高度参数，将使用上下文中的最新区块高度

```
zetacored query feemarket block-gas [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点地址
      --grpc-insecure      允许通过非安全通道进行 gRPC 通信，若不设置则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help               获取 block-gas 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口地址 [host]:[port]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的存储目录
      --log_format string  日志格式 (json|plain) 
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color       禁用彩色日志输出
      --trace              出错时打印完整堆栈跟踪信息
```

### 另请参阅

* [zetacored query feemarket](#zetacored-query-feemarket)	 - 费用市场模块的查询命令

## zetacored query feemarket params

获取费用市场参数

### 概要

获取费用市场参数值。

```
zetacored query feemarket params [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               params 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query feemarket](#zetacored-query-feemarket)	 - 费用市场模块的查询命令

## zetacored query fungible

用于 fungible 模块的查询命令

```
zetacored query fungible [flags]
```

### 选项

```
  -h, --help   显示 fungible 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query fungible code-hash](#zetacored-query-fungible-code-hash)	 - 显示账户的代码哈希
* [zetacored query fungible gas-stability-pool-address](#zetacored-query-fungible-gas-stability-pool-address)	 - 查询 gas 稳定池的地址
* [zetacored query fungible gas-stability-pool-balance](#zetacored-query-fungible-gas-stability-pool-balance)	 - 查询指定链的 gas 稳定池余额
* [zetacored query fungible gas-stability-pool-balances](#zetacored-query-fungible-gas-stability-pool-balances)	 - 查询所有 gas 稳定池余额
* [zetacored query fungible list-foreign-coins](#zetacored-query-fungible-list-foreign-coins)	 - 列出所有 ForeignCoins
* [zetacored query fungible show-foreign-coins](#zetacored-query-fungible-show-foreign-coins)	 - 显示 ForeignCoins 信息
* [zetacored query fungible system-contract](#zetacored-query-fungible-system-contract)	 - 查询系统合约

## zetacored query fungible code-hash

显示账户的代码哈希。

```
zetacored query fungible code-hash [address] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               code-hash 命令的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query fungible](#zetacored-query-fungible)	 - 用于可替代模块的查询命令

## zetacored query fungible gas-stability-pool-address

查询 gas 稳定性池地址

```
zetacored query fungible gas-stability-pool-address [flags]
```

### 选项

```
      --count-total        统计要查询的 gas-stability-pool-address 记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，如果不设置此项则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               获取 gas-stability-pool-address 命令的帮助信息
      --limit uint         要查询的 gas-stability-pool-address 的分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
      --offset uint        要查询的 gas-stability-pool-address 的分页偏移量
  -o, --output string      输出格式 (text|json)
      --page uint          要查询的 gas-stability-pool-address 的分页页码。这将把偏移量设置为限制的倍数（默认 1）
      --page-key string    要查询的 gas-stability-pool-address 的分页页面键
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query fungible](#zetacored-query-fungible)	 - 用于 fungible 模块的查询命令

## zetacored query fungible gas-stability-pool-balance

查询链的 Gas 稳定性池余额

```
zetacored query fungible gas-stability-pool-balance [chain-id] [flags]
```

### 选项

```
      --count-total        统计要查询的 gas-stability-pool-balance [chain-id] 中的总记录数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               获取 gas-stability-pool-balance 的帮助信息
      --limit uint         要查询的 gas-stability-pool-balance [chain-id] 的分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
      --offset uint        要查询的 gas-stability-pool-balance [chain-id] 的分页偏移量
  -o, --output string      输出格式（text|json）
      --page uint          要查询的 gas-stability-pool-balance [chain-id] 的分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string    要查询的 gas-stability-pool-balance [chain-id] 的分页页面键
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式（json|plain）
      --log_level string   日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query fungible](#zetacored-query-fungible)	 - 用于可互换模块的查询命令

## zetacored query fungible gas-stability-pool-balances

查询所有 gas 稳定性池余额

```
zetacored query fungible gas-stability-pool-balances [flags]
```

### 选项

```
      --count-total         统计要查询的 gas-stability-pool-balances 记录总数
      --grpc-addr string    用于此链的 gRPC 端点
      --grpc-insecure       允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int          使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                gas-stability-pool-balances 命令的帮助信息
      --limit uint          要查询的 gas-stability-pool-balances 的分页限制（默认 100）
      --node string          此链的 CometBFT RPC 接口的 [主机]:[端口]
      --offset uint         要查询的 gas-stability-pool-balances 的分页偏移量
  -o, --output string       输出格式 (text|json)
      --page uint           要查询的 gas-stability-pool-balances 的分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string     要查询的 gas-stability-pool-balances 的分页页面键
      --reverse             结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query fungible](#zetacored-query-fungible)	 - 用于 fungible 模块的查询命令

## zetacored query fungible list-foreign-coins

列出所有外部代币

```
zetacored query fungible list-foreign-coins [flags]
```

### 选项

```
      --count-total        统计 list-foreign-coins 中的记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               获取 list-foreign-coins 命令的帮助信息
      --limit uint         list-foreign-coins 的查询分页限制（默认值：100）
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
      --offset uint        list-foreign-coins 的查询分页偏移量
  -o, --output string      输出格式（text|json）
      --page uint          list-foreign-coins 的查询分页页码。这将偏移量设置为限制的倍数（默认值：1）
      --page-key string    list-foreign-coins 的查询分页页面键
      --reverse            按降序排序结果
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query fungible](#zetacored-query-fungible)	 - 用于 fungible 模块的查询命令

## zetacored query fungible show-foreign-coins

显示一个 ForeignCoins

```
zetacored query fungible show-foreign-coins [index] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               show-foreign-coins 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query fungible](#zetacored-query-fungible)	 - 用于 fungible 模块的查询命令

## zetacored query fungible system-contract

查询系统合约

```
zetacored query fungible system-contract [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               system-contract 的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query fungible](#zetacored-query-fungible)	 - 用于可替代模块的查询命令

## zetacored query gov

查询治理模块的命令

```
zetacored query gov [flags]
```

### 选项

```
  -h, --help   gov 命令的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query gov constitution](#zetacored-query-gov-constitution)	 - 查询当前链宪法
* [zetacored query gov deposit](#zetacored-query-gov-deposit)	 - 查询存款详情
* [zetacored query gov deposits](#zetacored-query-gov-deposits)	 - 查询提案的存款
* [zetacored query gov params](#zetacored-query-gov-params)	 - 查询治理流程的参数
* [zetacored query gov proposal](#zetacored-query-gov-proposal)	 - 查询单个提案的详情
* [zetacored query gov proposals](#zetacored-query-gov-proposals)	 - 使用可选过滤器查询提案
* [zetacored query gov tally](#zetacored-query-gov-tally)	 - 查询提案投票的计票结果
* [zetacored query gov vote](#zetacored-query-gov-vote)	 - 查询单个投票的详情
* [zetacored query gov votes](#zetacored-query-gov-votes)	 - 查询单个提案的投票

## zetacored query gov constitution

查询当前链的宪法

```
zetacored query gov constitution [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     constitution 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 治理模块的查询命令

## zetacored query gov deposit

查询存款详情

```
zetacored query gov deposit [proposal-id] [depositer-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     获取 deposit 命令的帮助
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 查询 gov 模块的命令

## zetacored query gov deposits

查询提案的抵押金

```
zetacored query gov deposits [proposal-id] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int                查询特定高度的状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                      deposits 命令的帮助信息
      --keyring-backend string    选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string        客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不对 JSON 输出进行缩进
      --node string               此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string             输出格式 (text|json)
      --page-count-total          
      --page-key binary           
      --page-limit uint           
      --page-offset uint          
      --page-reverse              
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 治理模块的查询命令

## zetacored query gov params

查询治理流程的参数

### 概要

查询治理流程的参数。指定特定参数类型（voting|tallying|deposit）以筛选结果。

```
zetacored query gov params [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询状态的特定高度（如果节点正在修剪状态，则可能出错）
  -h, --help                     params 命令的帮助信息
      --keyring-backend string   选择密钥环的后端（os、file、kwallet、pass、test、memory）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace、debug、info、warn、error、fatal、panic、disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 治理模块的查询命令

## zetacored query gov proposal

查询单个提案的详细信息。

```
zetacored query gov proposal [proposal-id] [flags]
```

### 示例

```
zetacored query gov proposal 1
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     提案命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 治理模块的查询命令

## zetacored query gov proposals

使用可选过滤器查询提案

```
zetacored query gov proposals [flags]
```

### 示例

```
zetacored query gov proposals --depositor cosmos1...
zetacored query gov proposals --voter cosmos1...
zetacored query gov proposals --proposal-status (unspecified | deposit-period | voting-period | passed | rejected | failed)
```

### 选项

```
      --depositor account address or key name                                                                        
      --grpc-addr string                                                                                             the gRPC endpoint to use for this chain
      --grpc-insecure                                                                                                allow gRPC over insecure channels, if not the server must use TLS
      --height int                                                                                                   Use a specific height to query state at (this can error if the node is pruning state)
  -h, --help                                                                                                         help for proposals
      --keyring-backend string                                                                                       Select keyring's backend (os|file|kwallet|pass|test|memory) 
      --keyring-dir string                                                                                           The client Keyring directory; if omitted, the default 'home' directory will be used
      --no-indent                                                                                                    Do not indent JSON output
      --node string                                                                                                  [host]:[port] to CometBFT RPC interface for this chain 
  -o, --output string                                                                                                Output format (text|json) 
      --page-count-total                                                                                             
      --page-key binary                                                                                              
      --page-limit uint                                                                                              
      --page-offset uint                                                                                             
      --page-reverse                                                                                                 
      --proposal-status ProposalStatus (unspecified | deposit-period | voting-period | passed | rejected | failed)    (default unspecified)
      --voter account address or key name                                                                            
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 用于 gov 模块的查询命令

## zetacored query gov tally

查询提案投票的统计结果

```
zetacored query gov tally [proposal-id] [flags]
```

### 示例

```
zetacored query gov tally 1
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int                查询特定高度的状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                      tally 命令的帮助信息
      --keyring-backend string    选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string        客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不缩进 JSON 输出
      --node string               此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string             输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string       网络链 ID
      --home string           配置和数据的目录
      --log_format string     日志格式 (json|plain)
      --log_level string      日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color          禁用彩色日志
      --trace                 出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 治理模块的查询命令

## zetacored query gov vote

查询单个投票的详细信息

```
zetacored query gov vote [proposal-id] [voter-addr] [flags]
```

### 示例

```
zetacored query gov vote 1 cosmos1...
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     vote 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 治理模块的查询命令

## zetacored query gov votes

查询单个提案的投票情况

```
zetacored query gov votes [proposal-id] [flags]
```

### 示例

```
zetacored query gov votes 1
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道进行 gRPC 通信，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     votes 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不对 JSON 输出进行缩进
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query gov](#zetacored-query-gov)	 - 治理模块的查询命令

## zetacored query group

群组模块的查询命令

```
zetacored query group [flags]
```

### 选项

```
  -h, --help   群组命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query group group-info](#zetacored-query-group-group-info)	 - 通过群组 ID 查询群组信息
* [zetacored query group group-members](#zetacored-query-group-group-members)	 - 通过群组 ID 查询群组成员
* [zetacored query group group-policies-by-admin](#zetacored-query-group-group-policies-by-admin)	 - 通过管理员账户地址查询群组策略
* [zetacored query group group-policies-by-group](#zetacored-query-group-group-policies-by-group)	 - 通过群组 ID 查询群组策略
* [zetacored query group group-policy-info](#zetacored-query-group-group-policy-info)	 - 通过群组策略账户地址查询群组策略信息
* [zetacored query group groups](#zetacored-query-group-groups)	 - 查询链上所有群组
* [zetacored query group groups-by-admin](#zetacored-query-group-groups-by-admin)	 - 通过管理员账户地址查询群组
* [zetacored query group groups-by-member](#zetacored-query-group-groups-by-member)	 - 通过成员地址查询群组
* [zetacored query group proposal](#zetacored-query-group-proposal)	 - 通过 ID 查询提案
* [zetacored query group proposals-by-group-policy](#zetacored-query-group-proposals-by-group-policy)	 - 通过群组策略账户地址查询提案
* [zetacored query group tally-result](#zetacored-query-group-tally-result)	 - 查询提案的计票结果
* [zetacored query group vote](#zetacored-query-group-vote)	 - 通过提案 ID 和投票者账户地址查询投票
* [zetacored query group votes-by-proposal](#zetacored-query-group-votes-by-proposal)	 - 通过提案 ID 查询投票
* [zetacored query group votes-by-voter](#zetacored-query-group-votes-by-voter)	 - 通过投票者账户地址查询投票

## zetacored query group group-info

通过群组 ID 查询群组信息

```
zetacored query group group-info [group-id] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     获取 group-info 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group group-members

通过组 ID 查询组成员

```
zetacored query group group-members [group-id] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     group-members 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口 
  -o, --output string            输出格式 (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 组模块的查询命令

## zetacored query group group-policies-by-admin

通过管理员账户地址查询群组策略

```
zetacored query group group-policies-by-admin [admin] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     帮助信息，针对 group-policies-by-admin
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group group-policies-by-group

按群组 ID 查询群组策略

```
zetacored query group group-policies-by-group [group-id] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     用于 group-policies-by-group 的帮助
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group group-policy-info

通过群组策略的账户地址查询群组策略信息

```
zetacored query group group-policy-info [group-policy-account] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询状态的指定高度（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                     group-policy-info 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain) 
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group groups

查询链上的所有群组

```
zetacored query group groups [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     groups 命令的帮助
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port] 
  -o, --output string            输出格式 (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group groups-by-admin

按管理员账户地址查询群组

```
zetacored query group groups-by-admin [admin] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许在不安全通道上使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     获取 groups-by-admin 命令的帮助
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group groups-by-member

按成员地址查询群组信息

```
zetacored query group groups-by-member [address] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点地址
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（若节点正在裁剪状态，此操作可能会报错）
  -h, --help                     获取 groups-by-member 命令帮助
      --keyring-backend string   选择钥匙环的后端类型 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；若未指定，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口地址 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         显示总页数
      --page-key binary          分页键值
      --page-limit uint          每页数量限制
      --page-offset uint         页码偏移量
      --page-reverse             反向分页
```

### 继承自父命令的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志输出
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group proposal

按 ID 查询提案

```
zetacored query group proposal [proposal-id] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会报错）
  -h, --help                     proposal 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group proposals-by-group-policy

通过群组策略账户地址查询提案

```
zetacored query group proposals-by-group-policy [group-policy-account] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                     proposals-by-group-policy 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group tally-result

查询提案的投票结果

```
zetacored query group tally-result [proposal-id] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     tally-result 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group vote

通过提案 ID 和投票者账户地址查询投票信息

```
zetacored query group vote [proposal-id] [voter] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询状态的特定高度（如果节点正在修剪状态，则可能出错）
  -h, --help                     vote 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group votes-by-proposal

通过提案 ID 查询投票

```
zetacored query group votes-by-proposal [proposal-id] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     votes-by-proposal 命令的帮助
      --keyring-backend string   选择键环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端键环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 指向此链的 CometBFT RPC 接口 
  -o, --output string            输出格式 (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query group votes-by-voter

按投票者账户地址查询投票

```
zetacored query group votes-by-voter [voter] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     votes-by-voter 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query group](#zetacored-query-group)	 - 群组模块的查询命令

## zetacored query lightclient

lightclient 模块的查询命令

```
zetacored query lightclient [flags]
```

### 选项

```
  -h, --help   lightclient 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query lightclient list-block-header](#zetacored-query-lightclient-list-block-header)	 - 列出所有区块头
* [zetacored query lightclient list-chain-state](#zetacored-query-lightclient-list-chain-state)	 - 列出所有链状态
* [zetacored query lightclient show-block-header](#zetacored-query-lightclient-show-block-header)	 - 根据哈希显示区块头
* [zetacored query lightclient show-chain-state](#zetacored-query-lightclient-show-chain-state)	 - 根据链 ID 显示链状态
* [zetacored query lightclient show-header-enabled-chains](#zetacored-query-lightclient-show-header-enabled-chains)	 - 显示验证标志

## zetacored query lightclient list-block-header

列出所有区块头

```
zetacored query lightclient list-block-header [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               list-block-header 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query lightclient](#zetacored-query-lightclient)	 - lightclient 模块的查询命令

## zetacored query lightclient list-chain-state

列出所有链状态

```
zetacored query lightclient list-chain-state [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               list-chain-state 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络 chain ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              在出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query lightclient](#zetacored-query-lightclient)	 - lightclient 模块的查询命令

## zetacored query lightclient show-block-header

根据区块哈希显示区块头信息

```
zetacored query lightclient show-block-header [block-hash] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点地址
      --grpc-insecure      允许通过非安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         指定要查询状态的特定区块高度（如果节点正在修剪状态，此操作可能会出错）
  -h, --help               显示 show-block-header 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口地址 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query lightclient](#zetacored-query-lightclient)	 - 轻客户端模块的查询命令

## zetacored query lightclient show-chain-state

根据链 ID 显示链状态

```
zetacored query lightclient show-chain-state [chain-id] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               显示 show-chain-state 的帮助信息
      --node string        [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query lightclient](#zetacored-query-lightclient)	 - 用于 lightclient 模块的查询命令

## zetacored query lightclient show-header-enabled-chains

显示验证标志

```
zetacored query lightclient show-header-enabled-chains [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               显示 show-header-enabled-chains 命令的帮助信息
      --node string        [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string      输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query lightclient](#zetacored-query-lightclient)	 - 轻客户端模块的查询命令

## zetacored query observer

observer 模块的查询命令

```
zetacored query observer [flags]
```

### 选项

```
  -h, --help   observer 的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query observer get-historical-tss-address](#zetacored-query-observer-get-historical-tss-address)	 - 通过最终化的 zeta 高度查询 TSS 地址（用于历史 TSS 地址）
* [zetacored query observer get-tss-address](#zetacored-query-observer-get-tss-address)	 - 查询当前 TSS 地址
* [zetacored query observer list-ballots](#zetacored-query-observer-list-ballots)	 - 查询所有 ballots
* [zetacored query observer list-ballots-for-height](#zetacored-query-observer-list-ballots-for-height)	 - 查询 BallotListForHeight
* [zetacored query observer list-blame](#zetacored-query-observer-list-blame)	 - 查询所有责任记录
* [zetacored query observer list-blame-by-msg](#zetacored-query-observer-list-blame-by-msg)	 - 查询所有责任记录
* [zetacored query observer list-chain-nonces](#zetacored-query-observer-list-chain-nonces)	 - 列出所有 chainNonces
* [zetacored query observer list-chain-params](#zetacored-query-observer-list-chain-params)	 - 查询 GetChainParams
* [zetacored query observer list-chains](#zetacored-query-observer-list-chains)	 - 列出所有 SupportedChains
* [zetacored query observer list-node-account](#zetacored-query-observer-list-node-account)	 - 列出所有 NodeAccount
* [zetacored query observer list-observer-set](#zetacored-query-observer-list-observer-set)	 - 查询观察者集合
* [zetacored query observer list-pending-nonces](#zetacored-query-observer-list-pending-nonces)	 - 显示一个 chainNonces
* [zetacored query observer list-tss-funds-migrator](#zetacored-query-observer-list-tss-funds-migrator)	 - 列出所有 TSS 资金迁移器
* [zetacored query observer list-tss-history](#zetacored-query-observer-list-tss-history)	 - 显示 TSS 的历史列表
* [zetacored query observer show-ballot](#zetacored-query-observer-show-ballot)	 - 查询 BallotByIdentifier
* [zetacored query observer show-blame](#zetacored-query-observer-show-blame)	 - 查询 BlameByIdentifier
* [zetacored query observer show-chain-nonces](#zetacored-query-observer-show-chain-nonces)	 - 显示一个 chainNonces
* [zetacored query observer show-chain-params](#zetacored-query-observer-show-chain-params)	 - 查询 GetChainParamsForChain
* [zetacored query observer show-crosschain-flags](#zetacored-query-observer-show-crosschain-flags)	 - 显示跨链标志
* [zetacored query observer show-keygen](#zetacored-query-observer-show-keygen)	 - 显示密钥生成
* [zetacored query observer show-node-account](#zetacored-query-observer-show-node-account)	 - 显示一个 NodeAccount
* [zetacored query observer show-observer-count](#zetacored-query-observer-show-observer-count)	 - 查询观察者数量
* [zetacored query observer show-operational-flags](#zetacored-query-observer-show-operational-flags)	 - 显示操作标志
* [zetacored query observer show-tss](#zetacored-query-observer-show-tss)	 - 显示一个 TSS
* [zetacored query observer show-tss-funds-migrator](#zetacored-query-observer-show-tss-funds-migrator)	 - 显示指定链的 TSS 资金迁移器

## zetacored query observer get-historical-tss-address

通过已确认的 zeta 高度查询历史 TSS 地址（用于历史 TSS 地址）

```
zetacored query observer get-historical-tss-address [finalizedZetaHeight] [bitcoinChainId] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               获取 get-historical-tss-address 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer get-tss-address

查询当前 TSS 地址

```
zetacored query observer get-tss-address [bitcoinChainId]] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               get-tss-address 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-ballots

查询所有投票

```
zetacored query observer list-ballots [flags]
```

### 选项

```
      --count-total        统计 list-ballots 中的记录总数以进行查询
      --grpc-addr string  用于此链的 gRPC 端点
      --grpc-insecure     允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int        使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help              list-ballots 命令的帮助信息
      --limit uint        list-ballots 查询的分页限制（默认 100）
      --node string       此链的 CometBFT RPC 接口的 [主机]:[端口] 
      --offset uint       list-ballots 查询的分页偏移量
  -o, --output string     输出格式（text|json） 
      --page uint         list-ballots 查询的分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string   list-ballots 查询的分页页面键
      --reverse           结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录 
      --log_format string   日志格式（json|plain） 
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'） 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-ballots-for-height

查询指定高度的投票列表

```
zetacored query observer list-ballots-for-height [height] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               list-ballots-for-height 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-blame

查询所有 Blame 记录

```
zetacored query observer list-blame [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               list-blame 命令的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-blame-by-msg

查询所有责备记录

```
zetacored query observer list-blame-by-msg [chainId] [nonce] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               list-blame-by-msg 命令的帮助
      --node string        [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-obobserver)	 - 观察者模块的查询命令

## zetacored query observer list-chain-nonces

列出所有 chainNonces

```
zetacored query observer list-chain-nonces [flags]
```

### 选项

```
      --count-total        统计要查询的 list-chain-nonces 中的记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               有关 list-chain-nonces 的帮助
      --limit uint         要查询的 list-chain-nonces 的分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
      --offset uint        要查询的 list-chain-nonces 的分页偏移量
  -o, --output string      输出格式 (text|json)
      --page uint          要查询的 list-chain-nonces 的分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string    要查询的 list-chain-nonces 的分页页面键
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-chain-params

查询获取链参数

```
zetacored query observer list-chain-params [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help               获取 list-chain-params 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的存储目录
      --log_format string  日志格式 (json|plain) 
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-chains

列出所有支持的链

```
zetacored query observer list-chains [flags]
```

### 选项

```
      --count-total        统计 list-chains 中要查询的记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               关于 list-chains 的帮助信息
      --limit uint         list-chains 的查询分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口的 [主机]:[端口]
      --offset uint        list-chains 的查询分页偏移量
  -o, --output string      输出格式（text|json）
      --page uint          list-chains 的查询分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string    list-chains 的查询分页页面键
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-node-account

列出所有 NodeAccount

```
zetacored query observer list-node-account [flags]
```

### 选项

```
      --count-total        统计 list-node-account 中要查询的记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许在不安全通道上使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               列出 list-node-account 的帮助信息
      --limit uint         list-node-account 要查询的分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
      --offset uint        list-node-account 要查询的分页偏移量
  -o, --output string      输出格式 (text|json)
      --page uint          list-node-account 要查询的分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string    list-node-account 要查询的分页页面键
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-observer-set

查询观察者集合

```
zetacored query observer list-observer-set [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               list-observer-set 的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-pending-nonces

显示链上待处理 nonces

```
zetacored query observer list-pending-nonces [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道进行 gRPC 通信，否则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help               获取 list-pending-nonces 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-tss-funds-migrator

列出所有 TSS 资金迁移器

```
zetacored query observer list-tss-funds-migrator [flags]
```

### 选项

```
      --count-total        统计 list-tss-funds-migrator 中的记录总数以进行查询
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               list-tss-funds-migrator 的帮助信息
      --limit uint         list-tss-funds-migrator 的分页限制以进行查询（默认值 100）
      --node string        [host]:[port] 到此链的 CometBFT RPC 接口
      --offset uint        list-tss-funds-migrator 的分页偏移以进行查询
  -o, --output string      输出格式 (text|json)
      --page uint          list-tss-funds-migrator 的分页页面以进行查询。这将偏移设置为限制的倍数（默认值 1）
      --page-key string    list-tss-funds-migrator 的分页页面键以进行查询
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer list-tss-history

显示 TSS 的历史列表

```
zetacored query observer list-tss-history [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，如果未设置则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               列出 TSS 历史的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 参见

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-ballot

查询 BallotByIdentifier

```
zetacored query observer show-ballot [ballot-identifier] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，如果未设置，服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               显示 show-ballot 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录
      --log_format string  日志格式 (json|plain)
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-blame

查询指定标识符的归责信息

```
zetacored query observer show-blame [blame-identifier] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help               显示 show-blame 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-chain-nonces

显示链随机数

```
zetacored query observer show-chain-nonces [chain-id] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               显示 show-chain-nonces 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-chain-params

查询 GetChainParamsForChain

```
zetacored query observer show-chain-params [chain-id] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               show-chain-params 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-crosschain-flags

显示跨链标志

```
zetacored query observer show-crosschain-flags [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，如果不指定则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help               显示 show-crosschain-flags 命令的帮助信息
      --node string        此链的 CometBFT RPC 接口 [主机]:[端口]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-keygen

显示密钥生成。

```
zetacored query observer show-keygen [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许在不安全通道上使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               show-keygen 命令的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-node-account

显示一个节点账户

```
zetacored query observer show-node-account [operator_address] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help               show-node-account 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-observer-count

查询显示观察者计数

```
zetacored query observer show-observer-count [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               显示 show-observer-count 的帮助信息
      --node string        到此链的 CometBFT RPC 接口的 [host]:[port] 
  -o, --output string      输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string    网络链 ID
      --home string        配置和数据的目录 
      --log_format string  日志格式 (json|plain) 
      --log_level string   日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color       禁用彩色日志
      --trace              出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-operational-flags

显示操作标志

```
zetacored query observer show-operational-flags [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               show-operational-flags 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-tss

显示一个 TSS。

```
zetacored query observer show-tss [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许在不安全通道上使用 gRPC，否则服务器必须使用 TLS
      --height int         使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help               show-tss 的帮助信息
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query observer show-tss-funds-migrator

显示某个链的 TSS 资金迁移器。

```
zetacored query observer show-tss-funds-migrator [chain-id] [flags]
```

### 选项

```
      --count-total        计算在 show-tss-funds-migrator [chain-id] 中查询的记录总数
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，如果未设置则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help               show-tss-funds-migrator 命令的帮助信息
      --limit uint         show-tss-funds-migrator [chain-id] 查询的分页限制（默认 100）
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
      --offset uint        show-tss-funds-migrator [chain-id] 查询的分页偏移量
  -o, --output string      输出格式（text|json）
      --page uint          show-tss-funds-migrator [chain-id] 查询的分页页码。这将偏移量设置为限制的倍数（默认 1）
      --page-key string    show-tss-funds-migrator [chain-id] 查询的分页页面键
      --reverse            结果按降序排序
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query observer](#zetacored-query-observer)	 - 观察者模块的查询命令

## zetacored query params

参数模块的查询命令

```
zetacored query params [flags]
```

### 选项

```
  -h, ---help   params 的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query params subspace](#zetacored-query-params-subspace)	 - 通过 subspace 和 key 查询原始参数
* [zetacored query params subspaces](#zetacored-query-params-subspaces)	 - 查询所有已注册的 subspaces 以及一个 subspace 的所有 keys

## zetacored query params subspace

按子空间和键查询原始参数

```
zetacored query params subspace [subspace] [key] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int                查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                      subspace 命令的帮助信息
      --keyring-backend string    选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string        客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不缩进 JSON 输出
      --node string               此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query params](#zetacored-query-params)	 - 参数模块的查询命令

## zetacored query params subspaces

查询所有已注册的子空间以及某个子空间的所有键

```
zetacored query params subspaces [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     subspaces 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query params](#zetacored-query-params)	 - 用于参数模块的查询命令

## zetacored query slashing

查询惩罚模块的命令

```
zetacored query slashing [flags]
```

### 选项

```
  -h, --help   显示 slashing 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query slashing params](#zetacored-query-slashing-params)	 - 查询当前惩罚参数
* [zetacored query slashing signing-info](#zetacored-query-slashing-signing-info)	 - 查询验证者的签名信息
* [zetacored query slashing signing-infos](#zetacored-query-slashing-signing-infos)	 - 查询所有验证者的签名信息

## zetacored query slashing params

查询当前的 slashing 参数

```
zetacored query slashing params [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     params 命令的帮助信息
      --keyring-backend string   选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query slashing](#zetacored-query-slashing)	 - slashing 模块的查询命令

## zetacored query slashing signing-info

查询验证人的签名信息

### 概要

查询验证人的签名信息，使用公钥（'zetacored comet show-validator'）或验证人共识地址

```
zetacored query slashing signing-info [validator-conspub/address] [flags]
```

### 示例

```
zetacored query slashing signing-info '{"@type":"/cosmos.crypto.ed25519.PubKey","key":"OauFcTKbN5Lx3fJL689cikXBqe+hcp6Y+x0rYUdR9Jk="}'
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     signing-info 命令的帮助信息
      --keyring-backend string   选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式（json|plain）
      --log_level string         日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color             禁用彩色日志
      --trace                    在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query slashing](#zetacored-query-slashing)	 - 惩罚模块的查询命令

## zetacored query slashing signing-infos

查询所有验证者的签名信息

```
zetacored query slashing signing-infos [flags]
```

### 选项

```
      --grpc-addr string         the gRPC endpoint to use for this chain
      --grpc-insecure            allow gRPC over insecure channels, if not the server must use TLS
      --height int               Use a specific height to query state at (this can error if the node is pruning state)
  -h, --help                     help for signing-infos
      --keyring-backend string   Select keyring's backend (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       The client Keyring directory; if omitted, the default 'home' directory will be used
      --no-indent                Do not indent JSON output
      --node string              [host]:[port] to CometBFT RPC interface for this chain 
  -o, --output string            Output format (text|json) 
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored query slashing](#zetacored-query-slashing)	 - 用于惩罚模块的查询命令

## zetacored query staking

质押模块的查询命令

```
zetacored query staking [flags]
```

### 选项

```
  -h, --help   质押相关帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query staking delegation](#zetacored-query-staking-delegation)	 - 基于地址和验证者地址查询委托
* [zetacored query staking delegations](#zetacored-query-staking-delegations)	 - 查询一个委托者进行的所有委托
* [zetacored query staking delegations-to](#zetacored-query-staking-delegations-to)	 - 查询对一个验证者的所有委托
* [zetacored query staking delegator-validator](#zetacored-query-staking-delegator-validator)	 - 查询指定委托者-验证者对中的验证者信息
* [zetacored query staking delegator-validators](#zetacored-query-staking-delegator-validators)	 - 查询指定委托者地址的所有验证者信息
* [zetacored query staking historical-info](#zetacored-query-staking-historical-info)	 - 查询指定高度的历史信息
* [zetacored query staking params](#zetacored-query-staking-params)	 - 查询当前质押参数信息
* [zetacored query staking pool](#zetacored-query-staking-pool)	 - 查询当前质押池数值
* [zetacored query staking redelegation](#zetacored-query-staking-redelegation)	 - 基于委托者及源和目标验证者地址查询重新委托记录
* [zetacored query staking unbonding-delegation](#zetacored-query-staking-unbonding-delegation)	 - 基于委托者和验证者地址查询解绑委托记录
* [zetacored query staking unbonding-delegations](#zetacored-query-staking-unbonding-delegations)	 - 查询一个委托者的所有解绑委托记录
* [zetacored query staking unbonding-delegations-from](#zetacored-query-staking-unbonding-delegations-from)	 - 查询来自一个验证者的所有解绑委托
* [zetacored query staking validator](#zetacored-query-staking-validator)	 - 查询验证者
* [zetacored query staking validators](#zetacored-query-staking-validators)	 - 查询所有验证者

## zetacored query staking delegation

基于地址和验证者地址查询委托

### 概要

查询单个委托者在单个验证者上的委托

```
zetacored query staking delegation [delegator-addr] [validator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     委托命令的帮助
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking delegations

查询某个委托者进行的所有委托

### 概要

查询单个委托者在所有验证人上的委托。

```
zetacored query staking delegations [delegator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure             允许通过不安全通道进行 gRPC 通信，若不设置则服务器必须使用 TLS
      --height int                查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help                      delegations 命令的帮助信息
      --keyring-backend string    选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string        客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                 不缩进 JSON 输出
      --node string               此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string             输出格式 (text|json)
      --page-count-total          
      --page-key binary           
      --page-limit uint           
      --page-offset uint          
      --page-reverse              
```

### 从父命令继承的选项

```
      --chain-id string           网络链 ID
      --home string               配置和数据的目录
      --log_format string         日志格式 (json|plain)
      --log_level string          日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color              禁用彩色日志
      --trace                     出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking delegations-to

查询对单个验证者的所有委托

### 概要

查询对单个验证者的委托。

```
zetacored query staking delegations-to [validator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许在不安全通道上使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     获取 delegations-to 命令的帮助
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking delegator-validator

查询给定委托人和验证者对的验证者信息

```
zetacored query staking delegator-validator [delegator-addr] [validator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     获取 delegator-validator 的帮助
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking delegator-validators

查询指定委托者地址对应的所有验证者信息

```
zetacored query staking delegator-validators [delegator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在裁剪状态，此操作可能会出错）
  -h, --help                     delegator-validators 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking historical-info

查询指定高度的历史信息

```
zetacored query staking historical-info [height] [flags]
```

### 示例

```
$ zetacored query staking historical-info 5
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，如果服务器未使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     帮助信息，用于 historical-info
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 查询质押模块的命令

## zetacored query staking params

查询当前的质押参数信息

### Synopsis

查询设置为质押参数的值。

```
zetacored query staking params [flags]
```

### Options

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     帮助信息，针对 params 命令
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 用于此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### Options inherited from parent commands

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### SEE ALSO

* [zetacored query staking](#zetacored-query-staking)	 - 查询质押模块的命令

## zetacored query staking pool

查询当前质押池的数值

### 概要

查询存储在质押池中的金额数值。

```
zetacored query staking pool [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     pool 命令的帮助信息
      --keyring-backend string   选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking redelegation

基于委托者以及源和目标验证者地址查询重新委托记录

### 概要

查询单个委托者在源验证者和目标验证者之间的重新委托记录。

```
zetacored query staking redelegation [delegator-addr] [src-validator-addr] [dst-validator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               用于查询状态的特定高度（如果节点正在修剪状态，则可能出错）
  -h, --help                     redelegation 命令的帮助信息
      --keyring-backend string   选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式（text|json）
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking unbonding-delegation

基于委托人和验证人地址查询解绑委托记录

### 概要

查询单个委托人在单个验证人上的解绑委托记录。

```
zetacored query staking unbonding-delegation [delegator-addr] [validator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于该链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，此操作可能会报错）
  -h, --help                     unbonding-delegation 命令的帮助信息
      --keyring-backend string   选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              该链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式（text|json）
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据目录
      --log_format string        日志格式（json|plain）
      --log_level string         日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking unbonding-delegations

查询一个委托人的所有解绑委托记录

### 概要

查询单个委托人的解绑委托。

```
zetacored query staking unbonding-delegations [delegator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     解绑委托命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking unbonding-delegations-from

查询来自某个验证人的所有解绑委托

### 概要

查询正在从某个验证人处解绑的委托。

```
zetacored query staking unbonding-delegations-from [validator-addr] [flags]
```

### 示例

```
$ zetacored query staking unbonding-delegations-from [val-addr]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     unbonding-delegations-from 命令的帮助信息
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query staking validator

查询验证器

### 概要

查询单个验证器的详细信息。

```
zetacored query staking validator [validator-addr] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     验证器命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string          网络链 ID
      --home string              配置和数据的目录
      --log_format string        日志格式 (json|plain)
      --log_level string         日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color             禁用彩色日志
      --trace                    在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)     - 质押模块的查询命令

## zetacored query staking validators

查询所有验证器

### 概要

查询网络中所有验证器的详细信息。

```
zetacored query staking validators [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，此操作可能会出错）
  -h, --help                     validators 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [主机]:[端口]
  -o, --output string            输出格式 (text|json)
      --page-count-total         
      --page-key binary          
      --page-limit uint          
      --page-offset uint         
      --page-reverse             
      --status string            
```

### 继承自父命令的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query staking](#zetacored-query-staking)	 - 质押模块的查询命令

## zetacored query tx

通过哈希、`[addr]/[seq]` 组合或逗号分隔的签名在已提交的区块中查询交易

### 概要

示例：
$ zetacored query tx [hash]
$ zetacored query tx --type=acc_seq [addr]/[sequence]
$ zetacored query tx --type=signature [sig1_base64],[sig2_base64...]

```
zetacored query tx --type=[hash|acc_seq|signature] [hash|acc_seq|signature] [flags]
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，如果未设置则服务器必须使用 TLS
      --height int         用于查询状态的特定高度（如果节点正在修剪状态，则可能出错）
  -h, --help               tx 命令的帮助
      --node string        此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string      输出格式 (text|json)
      --type string        查询交易时使用的类型，可以是 "hash"、"acc_seq" 或 "signature" 之一
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](##zetacored-query)	 - 查询子命令

## zetacored query txs

查询匹配一组事件的翻页交易记录

### 简介

搜索与指定事件完全匹配的交易，结果将进行分页处理。事件查询将直接传递给 Tendermint 的 RPC TxSearch 方法，并且必须符合 Tendermint 的查询语法。

请参阅各模块的文档以获取完整的可查询事件集合。每个模块在 `xx_events.md` 文件中记录了其相应的事件。

```
zetacored query txs [flags]
```

### 示例

```
$ zetacored query txs --query "message.sender='cosmos1...' AND message.action='withdraw_delegator_reward' AND tx.height > 7" --page 1 --limit 30
```

### 选项

```
      --grpc-addr string   用于此链的 gRPC 端点
      --grpc-insecure      允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int         查询特定高度的状态（如果节点正在修剪状态，则可能出错）
  -h, --help               关于 txs 命令的帮助信息
      --limit int          每页返回的交易结果数量（默认 100）
      --node string        此链的 CometBFT RPC 接口 [host]:[port]
      --order_by string    排序语义（asc|dsc）
  -o, --output string      输出格式（text|json）
      --page int           查询分页结果中的特定页面（默认 1）
      --query string       根据 Tendermint 查询语义的交易事件查询
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令

## zetacored query upgrade

用于升级模块的查询命令

```
zetacored query upgrade [flags]
```

### 选项

```
-h, --help   升级命令的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络 chain ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query](#zetacored-query)	 - 查询子命令
* [zetacored query upgrade applied](#zetacored-query-upgrade-applied)	 - 查询已完成升级所应用的高度处的区块头
* [zetacored query upgrade authority](#zetacored-query-upgrade-authority)	 - 获取升级授权地址
* [zetacored query upgrade module-versions](#zetacored-query-upgrade-module-versions)	 - 查询模块版本列表
* [zetacored query upgrade plan](#zetacored-query-upgrade-plan)	 - 查询升级计划（如果存在）

## zetacored query upgrade applied

查询已完成升级被应用时的区块头高度

### 概要

如果 upgrade-name 先前在链上执行过，这将返回它被应用时的区块头。这有助于客户端确定在给定区块范围内哪个二进制文件是有效的，以及提供更多上下文来理解过去的迁移。

```
zetacored query upgrade applied [upgrade-name] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，这可能会出错）
  -h, --help                     applied 命令的帮助信息
      --keyring-backend string   选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string       客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口 
  -o, --output string            输出格式 (text|json) 
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query upgrade](#zetacored-query-upgrade)	 - 查询升级模块的命令

## zetacored query upgrade authority

获取升级权限地址

```
zetacored query upgrade authority [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     authority 命令的帮助
      --keyring-backend string   选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端钥匙环目录；如果省略，将使用默认的 home 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口的 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query upgrade](#zetacored-query-upgrade)	 - 升级模块的查询命令

## zetacored query upgrade module-versions

查询模块版本列表

### 概要

获取模块名称及其各自共识版本的列表。在命令后指定特定模块名称将仅返回该模块的信息。

```
zetacored query upgrade module-versions [optional module_name] [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，否则服务器必须使用 TLS
      --height int               使用特定高度查询状态（如果节点正在修剪状态，则可能出错）
  -h, --help                     帮助信息，用于 module-versions
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              [host]:[port] 到此链的 CometBFT RPC 接口
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query upgrade](#zetacored-query-upgrade)	 - 用于升级模块的查询命令

## zetacored query upgrade plan

查询升级计划（如果存在）

### 概要

获取当前已安排的升级计划（如果存在）

```
zetacored query upgrade plan [flags]
```

### 选项

```
      --grpc-addr string         用于此链的 gRPC 端点
      --grpc-insecure            允许通过不安全通道使用 gRPC，若不指定则服务器必须使用 TLS
      --height int               查询特定高度的状态（如果节点正在修剪状态，可能会出错）
  -h, --help                     plan 命令的帮助信息
      --keyring-backend string   选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string       客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --no-indent                不缩进 JSON 输出
      --node string              此链的 CometBFT RPC 接口 [host]:[port]
  -o, --output string            输出格式 (text|json)
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored query upgrade](#zetacored-query-upgrade)	 - 升级模块的查询命令

## zetacored rollback

将 Cosmos SDK 和 CometBFT 状态回滚一个高度

### 概要

状态回滚用于从错误的应用程序状态转换中恢复，当 CometBFT 持久化了一个错误的应用程序哈希并因此无法取得进展时。回滚将高度 n 的状态覆盖为高度 n - 1 的状态。应用程序也会回滚到高度 n - 1。没有区块被移除，因此重启 CometBFT 后，区块 n 中的交易将针对应用程序重新执行。

```
zetacored rollback [flags]
```

### 选项

```
      --hard          移除最后一个区块以及状态
  -h, --help          rollback 命令的帮助
      --home string   应用程序主目录
```

### 从父命令继承的选项

```
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored snapshots

管理本地快照

### 选项

```
  -h, --help   快照帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 参见

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）
* [zetacored snapshots delete](#zetacored-snapshots-delete)	 - 删除本地快照
* [zetacored snapshots dump](#zetacored-snapshots-dump)	 - 将快照转储为便携式归档格式
* [zetacored snapshots export](#zetacored-snapshots-export)	 - 将应用状态导出到快照存储
* [zetacored snapshots list](#zetacored-snapshots-list)	 - 列出本地快照
* [zetacored snapshots load](#zetacored-snapshots-load)	 - 将快照归档文件（.tar.gz）加载到快照存储
* [zetacored snapshots restore](#zetacored-snapshots-restore)	 - 从本地快照恢复应用状态

## zetacored snapshots delete

删除本地快照

```
zetacored snapshots delete [height] [format] [flags]
```

### 选项

```
  -h, --help   删除操作的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored snapshots](#zetacored-snapshots)	 - 管理本地快照

## zetacored snapshots dump

将快照转储为便携式存档格式

```
zetacored snapshots dump [height] [format] [flags]
```

### 选项

```
  -h, --help            help for dump
  -o, --output string   output file
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored snapshots](#zetacored-snapshots)	 - 管理本地快照

## zetacored snapshots export

将应用程序状态导出到快照存储

```
zetacored snapshots export [flags]
```

### 选项

```
      --height int   Height to export, default to latest state height
  -h, --help         help for export
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored snapshots](#zetacored-snapshots)	 - 管理本地快照

## zetacored snapshots list

列出本地快照

```
zetacored snapshots list [flags]
```

### 选项

```
  -h, --help   list 命令的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored snapshots](#zetacored-snapshots)	 - 管理本地快照

## zetacored snapshots load

将快照存档文件 (.tar.gz) 加载到快照存储中

```
zetacored snapshots load [archive-file] [flags]
```

### 选项

```
  -h, --help   显示 load 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored snapshots](#zetacored-snapshots)	 - 管理本地快照

## zetacored snapshots restore

从本地快照恢复应用状态

### 概要

从本地快照恢复应用状态

```
zetacored snapshots restore [height] [format] [flags]
```

### 选项

```
  -h, --help   help for restore
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored snapshots](#zetacored-snapshots)	 - 管理本地快照

## zetacored start

运行全节点

### Synopsis

运行全节点应用程序，可以在进程内或进程外使用 CometBFT。默认情况下，应用程序将在进程内运行 CometBFT。

修剪选项可以通过 `--pruning` 标志提供，或者同时使用 `--pruning-keep-recent`、`pruning-keep-every` 和 `pruning-interval`。

对于 `--pruning`，选项如下：

- default：保留最后 100 个状态，并每 500 个状态保留一个；每 10 个区块间隔进行修剪
- nothing：所有历史状态都将被保存，不会删除任何内容（即归档节点）
- everything：所有已保存的状态都将被删除，仅存储当前状态；每 10 个区块间隔进行修剪
- custom：允许通过 `pruning-keep-recent`、`pruning-keep-every` 和 `pruning-interval` 手动指定修剪选项

节点停止配置以两个标志的形式存在：`--halt-height` 和 `--halt-time`。在 ABCI 提交阶段，节点将检查当前区块高度是否大于或等于停止高度，或者当前区块时间是否大于或等于停止时间。如果是，节点将尝试优雅关闭，并且该区块不会被提交。此外，节点将无法提交后续区块。

为了进行分析和基准测试，可以通过 `--cpu-profile` 标志启用 CPU 分析，该标志接受生成的 pprof 文件的路径。

```
zetacored start [flags]
```

### Options

```
      --abci string                                     指定 ABCI 传输方式 (socket | grpc)
      --address string                                  监听地址
      --api.enable                                      定义是否启用 Cosmos-sdk REST 服务器
      --api.enabled-unsafe-cors                         定义是否启用 CORS（不安全 - 使用时风险自负）
      --app-db-backend string                          应用程序和快照数据库的数据库类型
      --consensus.create_empty_blocks                   设置为 false 以仅在有交易或 AppHash 更改时生成区块（默认 true）
      --consensus.create_empty_blocks_interval string   空块之间的可能间隔
      --consensus.double_sign_check_height int          在加入共识前检查节点共识投票存在的区块数
      --cpu-profile string                              启用 CPU 分析并写入到提供的文件
      --db_backend string                               数据库后端：goleveldb | cleveldb | boltdb | rocksdb | badgerdb
      --db_dir string                                   数据库目录
      --evm.cache-preimage                              启用 EVM 中 SHA3 原像的跟踪（尚未实现）
      --evm.evm-chain-id uint                           EIP-155 兼容的重放保护链 ID（默认 262144）
      --evm.max-tx-gas-wanted uint                      在检查交易模式下，ante 处理程序中返回的每个 eth 交易的所需 gas
      --evm.tracer string                               用于从 EVM 交易执行中收集执行跟踪的 EVM 跟踪器类型 (json|struct|access_list|markdown)
      --genesis_hash bytesHex                           可选创世文件的 SHA-256 哈希
      --grpc-only                                       仅以 gRPC 查询模式启动节点，不带 CometBFT 进程
      --grpc-web.address string                         gRPC-Web 服务器监听地址
      --grpc-web.enable                                 定义是否启用 gRPC-Web 服务器。（注意：gRPC 也必须启用。）
      --grpc.address string                             gRPC 服务器监听地址
      --grpc.enable                                     定义是否启用 gRPC 服务器
      --halt-height uint                                链优雅停止并关闭节点的区块高度
      --halt-time uint                                 链优雅停止并关闭节点的最小区块时间（Unix 秒）
  -h, --help                                            获取 start 命令的帮助
      --home string                                     应用程序主目录
      --inter-block-cache                               启用区块间缓存（默认 true）
      --inv-check-period uint                           每 N 个区块断言注册的不变量
      --json-rpc.address string                         JSON-RPC 服务器监听地址
      --json-rpc.allow-insecure-unlock                  当账户相关 RPC 通过 http 暴露时，允许不安全的账户解锁（默认 true）
      --json-rpc.allow-unprotected-txs                  当全局参数禁用时，允许通过节点的 RPC 提交未受保护（非 EIP155 签名）的交易
      --json-rpc.api strings                            定义应启用的 JSON-RPC 命名空间列表（默认 [eth,net,web3]）
      --json-rpc.block-range-cap eth_getLogs            设置 eth_getLogs 查询允许的最大区块范围（默认 10000）
      --json-rpc.enable                                 定义是否启用 JSON-RPC 服务器
      --json-rpc.enable-indexer                         为 json-rpc 启用自定义交易索引器
      --json-rpc.evm-timeout duration                   设置用于 eth_call 的超时（0=无限）（默认 5s）
      --json-rpc.filter-cap int32                       设置可创建的过滤器总数的全局上限（默认 200）
      --json-rpc.gas-cap uint                           设置在 eth_call/estimateGas 中可使用的 gas 上限，单位是 aatom（0=无限）（默认 25000000）
      --json-rpc.http-idle-timeout duration             设置 json-rpc http 服务器的空闲超时（0=无限）（默认 2m0s）
      --json-rpc.http-timeout duration                  设置 json-rpc http 服务器的读/写超时（0=无限）（默认 30s）
      --json-rpc.logs-cap eth_getLogs                   设置单个 eth_getLogs 查询可返回的最大结果数（默认 10000）
      --json-rpc.max-open-connections int               设置服务器监听器的最大同时连接数
      --json-rpc.txfee-cap float                        设置通过 RPC API 发送的交易费用上限（1 = 默认 1 evmos）（默认 1）
      --json-rpc.ws-address string                      JSON-RPC WS 服务器监听地址
      --metrics                                         定义是否启用 EVM rpc 指标服务器
      --min-retain-blocks uint                          ABCI 提交期间用于修剪 CometBFT 区块的最小区块高度偏移
      --minimum-gas-prices string                       接受交易的最低 gas 价格；交易中的任何费用必须满足此最低要求（例如 20000000000azeta）
      --moniker string                                  节点名称
      --p2p.external-address string                     向对等节点广告的 ip:port 地址，供它们拨号
      --p2p.laddr string                                节点监听地址。（0.0.0.0:0 表示任何接口，任何端口）
      --p2p.persistent_peers string                     逗号分隔的 ID@host:port 持久对等节点
      --p2p.pex                                         启用/禁用对等节点交换（默认 true）
      --p2p.private_peer_ids string                     逗号分隔的私有对等节点 ID
      --p2p.seed_mode                                   启用/禁用种子模式
      --p2p.seeds string                                逗号分隔的 ID@host:port 种子节点
      --p2p.unconditional_peer_ids string               逗号分隔的无条件对等节点 ID
      --priv_validator_laddr string                     用于监听来自外部 priv_validator 进程连接的套接字地址
      --proxy_app string                                代理应用程序地址，或用于本地测试的 'kvstore'、'persistent_kvstore' 或 'noop' 之一
      --pruning string                                  修剪策略 (default|nothing|everything|custom)
      --pruning-interval uint                           从磁盘删除已修剪高度的区块高度间隔（如果修剪不是 'custom'，则忽略）
      --pruning-keep-recent uint                        保留在磁盘上的最近区块高度数（如果修剪不是 'custom'，则忽略）
      --rpc.grpc_laddr string                           GRPC 监听地址（仅限 BroadcastTx）。需要端口
      --rpc.laddr string                                RPC 监听地址。需要端口
      --rpc.pprof_laddr string                          pprof 监听地址 (https://golang.org/pkg/net/http/pprof)
      --rpc.unsafe                                      启用不安全的 rpc 方法
      --skip-config-overwrite                           跳过运行配置覆盖处理程序。仅用于测试目的，跳过使用硬编码的默认超时，而是使用配置文件
      --state-sync.snapshot-interval uint               状态同步快照间隔
      --state-sync.snapshot-keep-recent uint32          保留的状态同步快照数（默认 2）
      --tls.certificate-path string                     服务器 TLS 配置的 cert.pem 文件路径
      --tls.key-path string                             服务器 TLS 配置的 key.pem 文件路径
      --trace                                           在 ABCI 日志中为错误提供完整堆栈跟踪
      --trace-store string                              启用 KVStore 跟踪到输出文件
      --transport string                                传输协议：socket, grpc
      --unsafe-skip-upgrades ints                       跳过一组升级高度以继续使用旧二进制文件
      --with-cometbft                                   在进程内与 CometBFT 嵌入式运行 abci 应用程序（默认 true）
      --x-crisis-skip-assert-invariants                 启动时跳过 x/crisis 不变量检查
```

### Options inherited from parent commands

```
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
```

### SEE ALSO

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored status

查询远程节点状态

```
zetacored status [flags]
```

### 选项

```
  -h, --help            帮助信息
  -n, --node string     要连接的节点
  -o, --output string   输出格式 (text|json)
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored tx

交易子命令

```
zetacored tx [flags]
```

### 选项

```
      --chain-id string   网络链 ID
  -h, --help              tx 命令的帮助
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）
* [zetacored tx auth](#zetacored-tx-auth)	 - auth 模块的交易命令
* [zetacored tx authority](#zetacored-tx-authority)	 - authority 交易子命令
* [zetacored tx authz](#zetacored-tx-authz)	 - 授权交易子命令
* [zetacored tx bank](#zetacored-tx-bank)	 - 银行交易子命令
* [zetacored tx broadcast](#zetacored-tx-broadcast)	 - 广播离线生成的交易
* [zetacored tx consensus](#zetacored-tx-consensus)	 - consensus 模块的交易命令
* [zetacored tx crisis](#zetacored-tx-crisis)	 - crisis 模块的交易命令
* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - crosschain 交易子命令
* [zetacored tx decode](#zetacored-tx-decode)	 - 解码二进制编码的交易字符串
* [zetacored tx distribution](#zetacored-tx-distribution)	 - distribution 交易子命令
* [zetacored tx emissions](#zetacored-tx-emissions)	 - emissions 交易子命令
* [zetacored tx encode](#zetacored-tx-encode)	 - 编码离线生成的交易
* [zetacored tx evidence](#zetacored-tx-evidence)	 - 证据交易子命令
* [zetacored tx evm](#zetacored-tx-evm)	 - evm 子命令
* [zetacored tx feemarket](#zetacored-tx-feemarket)	 - feemarket 模块的交易命令
* [zetacored tx fungible](#zetacored-tx-fungible)	 - fungible 交易子命令
* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令
* [zetacored tx group](#zetacored-tx-group)	 - 组交易子命令
* [zetacored tx lightclient](#zetacored-tx-lightclient)	 - lightclient 交易子命令
* [zetacored tx multi-sign](#zetacored-tx-multi-sign)	 - 为离线生成的交易生成多重签名
* [zetacored tx multisign-batch](#zetacored-tx-multisign-batch)	 - 从批量签名中批量组装多重签名交易
* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令
* [zetacored tx sign](#zetacored-tx-sign)	 - 签名离线生成的交易
* [zetacored tx sign-batch](#zetacored-tx-sign-batch)	 - 签名交易批量文件
* [zetacored tx slashing](#zetacored-tx-slashing)	 - slashing 模块的交易命令
* [zetacored tx staking](#zetacored-tx-staking)	 - 质押交易子命令
* [zetacored tx upgrade](#zetacored-tx-upgrade)	 - 升级交易子命令
* [zetacored tx validate-signatures](#zetacored-tx-validate-signatures)	 - 验证交易签名
* [zetacored tx vesting](#zetacored-tx-vesting)	 - 归属交易子命令

## zetacored tx auth

用于认证模块的交易命令

```
zetacored tx auth [flags]
```

### 选项

```
  -h, --help   获取 auth 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx auth update-params-proposal](#zetacored-tx-auth-update-params-proposal)	 - 提交更新认证模块参数的提案。注意：必须提供完整的参数。

## zetacored tx auth update-params-proposal

提交一个提案以更新认证模块参数。注意：必须提供完整的参数。

```
zetacored tx auth update-params-proposal [params] [flags]
```

### 示例

```
zetacored tx auth update-params-proposal '{ "max_memo_characters": 0, "tx_sig_limit": 0, "tx_size_cost_per_byte": 0, "sig_verify_cost_ed25519": 0, "sig_verify_cost_secp256k1": 0 }'
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成 aux 签名者数据而非发送 tx
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以 tx 模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        update-params-proposal 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止 tx 在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过 tx 广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 参见

* [zetacored tx auth](#zetacored-tx-auth)	 - 认证模块的交易命令

## zetacored tx authority

授权交易子命令

```
zetacored tx authority [flags]
```

### 选项

```
  -h, --help   获取 authority 命令的帮助信息
```

### 继承自父命令的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx authority add-authorization](#zetacored-tx-authority-add-authorization)	 - 添加新授权或更新现有授权的策略。策略类型可以是 0（groupEmergency）、1（groupOperational）、2（groupAdmin）。
* [zetacored tx authority remove-authorization](#zetacored-tx-authority-remove-authorization)	 - 移除现有授权
* [zetacored tx authority remove-chain-info](#zetacored-tx-authority-remove-chain-info)	 - 移除指定链 ID 的链信息
* [zetacored tx authority update-chain-info](#zetacored-tx-authority-update-chain-info)	 - 更新链信息
* [zetacored tx authority update-policies](#zetacored-tx-authority-update-policies)	 - 将策略更新为 JSON 文件中提供的值

## zetacored tx authority add-authorization

添加新的授权或更新现有授权的策略。策略类型可以是 0 代表 groupEmergency，1 代表 groupOperational，2 代表 groupAdmin。

```
zetacored tx authority add-authorization [msg-url] [authorized-policy] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅离线模式）
      --aux                          生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，本地密钥库不可访问）
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 上限；设为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回的估算值的调整系数；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                         add-authorization 命令的帮助信息
      --keyring-backend string       选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加说明的注释（之前为 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，并且区块时间已超过提交时间加 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                   小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                    启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                          跳过交易广播提示确认
```

### 继承自父命令的选项

```
      --home string                  配置和数据的目录
      --log_format string            日志格式 (json|plain)
      --log_level string             日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                 禁用彩色日志
      --trace                        在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx authority](#zetacored-tx-authority)	 - 授权交易子命令

## zetacored tx authority remove-authorization

移除现有的授权

```
zetacored tx authority remove-authorization [msg-url] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        remove-authorization 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx authority](#zetacored-tx-authority)	 - 授权交易子命令

## zetacored tx authority remove-chain-info

移除指定链 ID 的链信息

```
zetacored tx authority remove-chain-info [chain-id] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        remove-chain-info 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（原 --memo 选项）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx authority](#zetacored-tx-authority)	 - 权限交易子命令

## zetacored tx authority update-chain-info

更新链信息

```
zetacored tx authority update-chain-info [chain-info-json-file] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                           生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string         交易广播模式 (sync|async)
      --chain-id string               网络链 ID
      --dry-run                       忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，本地密钥库不可访问）
      --fee-granter string            费用资助者为交易支付费用
      --fee-payer string              费用支付者代替签名者支付交易费用
      --fees string                   随交易支付的费用；例如：10uatom
      --from string                   用于签名的私钥名称或地址
      --gas string                    每笔交易的 gas 上限；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。(默认 200000)
      --gas-adjustment float          乘以交易模拟返回估算值的调整因子；如果手动设置了 gas 上限，则忽略此标志 (默认 1)
      --gas-prices string             用于确定交易费用的 Gas 价格（十进制格式，例如 0.1uatom）
      --generate-only                 构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                          update-chain-info 命令的帮助信息
      --keyring-backend string        选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string            客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                        使用已连接的 Ledger 设备
      --node string                   该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                   为交易添加描述说明的注释（之前为 --memo）
      --offline                       离线模式（不允许任何在线功能）
  -o, --output string                 输出格式 (text|json)
  -s, --sequence uint                 签名账户的序列号（仅限离线模式）
      --sign-mode string              选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration     TimeoutDuration 是交易在内存池中被视为有效的时长。交易的乱序 nonce 将被设置为交易创建时间加上传递的 duration 值。如果交易仍在内存池中，并且区块时间已超过提交时间加上 TimeoutTimestamp，则该交易将被拒绝。
      --timeout-height uint           已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                    小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                     启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                           跳过交易广播提示确认
```

### 继承自父命令的选项

```
      --home string                   配置和数据的目录
      --log_format string             日志格式 (json|plain)
      --log_level string              日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                  禁用彩色日志
      --trace                         出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx authority](#zetacored-tx-authority)	 - 授权交易子命令

## zetacored tx authority update-policies

使用 JSON 文件中的值更新策略。

```
zetacored tx authority update-policies [policies-json-file] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置一个有效的代币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        与交易模拟返回的估计值相乘的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        update-policies 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置一个区块超时高度以防止交易超过某个高度被提交
      --tip string                  Tip 是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx authority](#zetacored-tx-authority)	 - 权威交易子命令

## zetacored tx authz

授权交易子命令

### 概要

授权和撤销代表您的地址执行交易的访问权限

```
zetacored tx authz [flags]
```

### 选项

```
  -h, --help   authz 命令的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx authz exec](#zetacored-tx-authz-exec)	 - 代表授权者账户执行交易
* [zetacored tx authz grant](#zetacored-tx-authz-grant)	 - 向地址授予授权
* [zetacored tx authz revoke](#zetacored-tx-authz-revoke)	 - 撤销授权

## zetacored tx authz exec

代表授权人账户执行交易

### 概要

代表授权人账户执行交易：
示例：
 $ zetacored tx authz exec tx.json --from grantee
 $ zetacored tx bank send [granter] [recipient] --from [granter] --chain-id [chain-id] --generate-only > tx.json && zetacored tx authz exec tx.json --from grantee

```
zetacored tx authz exec [tx-json-file] --from [grantee] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          为交易授予手续费的授权方
      --fee-payer string            代替签名者支付交易手续费的支付方
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 以自动计算充足 gas。注意："auto" 选项不一定报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的 Gas 价格（十进制格式）（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        exec 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加说明的备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时长。交易的无序随机数将被设置为交易创建时间 + 传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将在目标链上转移给手续费支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx authz](#zetacored-tx-authz)	 - 授权交易子命令

## zetacored tx authz grant

授予地址授权

### 概要

创建一个新的授权授予，允许一个地址代表您执行交易：

示例：
 $ zetacored tx authz grant cosmos1skjw.. send --spend-limit=1000stake --from=cosmos1skl..
 $ zetacored tx authz grant cosmos1skjw.. generic --msg-type=/cosmos.gov.v1.MsgVote --from=cosmos1sk..

```
zetacored tx authz grant [grantee] [authorization_type="send"|"generic"|"delegate"|"unbond"|"redelegate"] --from [granter] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户号（仅离线模式）
      --allow-list strings           允许的地址列表，授权接收者可以发送资金，以逗号分隔
      --allowed-validators strings   允许的验证者地址，以逗号分隔
      --aux                          生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string        交易广播模式（sync|async）
      --chain-id string              网络链 ID
      --deny-validators strings      拒绝的验证者地址，以逗号分隔
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --expiration int               过期时间作为 Unix 时间戳。设置为零（0）表示无过期。默认值为 0。
      --fee-granter string           费用授予者为交易授予费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float         乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string            Gas 价格，以十进制格式确定交易费用（例如 0.1uatom）
      --generate-only                构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                         获取 grant 命令的帮助
      --keyring-backend string       选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string           客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用连接的 Ledger 设备
      --msg-type string              为其创建 GenericAuthorization 的 Msg 方法名称
      --node string                  连接到该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加描述的注释（之前是 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式（text|json）
  -s, --sequence uint                签名账户的序列号（仅离线模式）
      --sign-mode string             选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --spend-limit string           发送授权的支出限制，允许支出的币种数组
      --timeout-duration duration    超时持续时间，交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint          已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                   小费金额，将转移到目标链上的费用支付者。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                    启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### SEE ALSO

* [zetacored tx authz](#zetacored-tx-authz)	 - 授权交易子命令

## zetacored tx authz revoke

撤销授权

### 概要

撤销从授权者到被授权者的授权：
示例：
 $ zetacored tx authz revoke cosmos1skj.. /cosmos.bank.v1beta1.MsgSend --from=cosmos1skj..

```
zetacored tx authz revoke [grantee] [msg-type-url] --from=[granter] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式的 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        revoke 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx authz](#zetacored-tx-authz)	 - 授权交易子命令

## zetacored tx bank

银行交易子命令

```
zetacored tx bank [flags]
```

### 选项

```
  -h, --help   获取 bank 命令的帮助信息
```

### 继承自父命令的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx bank multi-send](#zetacored-tx-bank-multi-send)	 - 将资金从一个账户发送到两个或更多账户。
* [zetacored tx bank send](#zetacored-tx-bank-send)	 - 将资金从一个账户发送到另一个账户。
* [zetacored tx bank set-send-enabled-proposal](#zetacored-tx-bank-set-send-enabled-proposal)	 - 提交提案以设置/更新/删除发送启用条目
* [zetacored tx bank update-params-proposal](#zetacored-tx-bank-update-params-proposal)	 - 提交提案以更新银行模块参数。注意：必须提供完整的参数。

## zetacored tx bank multi-send

从一个账户向两个或多个账户发送资金。

### 概要

从一个账户向两个或多个账户发送资金。
默认情况下，将 [amount] 发送到列表中的每个地址。
使用 `--split` 标志时，[amount] 会在地址之间平均分配。
注意，`--from` 标志被忽略，因为它隐含在 [from_key_or_address] 中，并且地址之间用空格分隔。
当使用 `--dry-run` 时，不能使用密钥名称，只能使用 bech32 地址。

```
zetacored tx bank multi-send [from_key_or_address] [to_address_1 to_address_2 ...] [amount] [flags]
```

### 示例

```
zetacored tx bank multi-send cosmos1... cosmos1... cosmos1... cosmos1... 10stake
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        multi-send 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --split                       将等分的代币金额发送到每个地址
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  Tip 是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx bank](#zetacored-tx-bank)	 - 银行交易子命令

## zetacored tx bank send

从一个账户发送资金到另一个账户。

### 概要

从一个账户发送资金到另一个账户。
注意，`--from` 标志被忽略，因为它隐含在 `[from_key_or_address]` 中。
当使用 `--dry-run` 时，不能使用密钥名称，只能使用 bech32 地址。

```
zetacored tx bank send [from_key_or_address] [to_address] [amount] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 `--gas` 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 `auto` 以自动计算足够的 gas。注意：`auto` 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 `fees` 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式的 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        send 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 `home` 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 `[host]:[port]`
      --note string                 为交易添加描述说明（之前是 `--memo`）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 `--timeout-duration`。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 `--aux` 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 `--timeout-duration` 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx bank](zetacored-tx-bank)	 - 银行交易子命令

## zetacored tx bank set-send-enabled-proposal

提交一个提案来设置/更新/删除发送启用条目

```
zetacored tx bank set-send-enabled-proposal [send_enabled] [flags]
```

### 示例

```
zetacored tx bank set-send-enabled-proposal '{"denom":"stake","enabled":true}'
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的燃气限制；设置为 "auto" 以自动计算充足燃气。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置燃气限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式燃气价格（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        set-send-enabled-proposal 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
      --use-default-for strings     对给定代币使用默认值（删除发送启用条目）
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx bank](#zetacored-tx-bank)	 - 银行交易子命令

## zetacored tx bank update-params-proposal

提交更新银行模块参数的提案。注意：必须提供完整的参数。

```
zetacored tx bank update-params-proposal [params] [flags]
```

### 示例

```
zetacored tx bank update-params-proposal '{ "default_send_enabled": true }'
```

### 选项

```
  -a, --account-number uint         签名账户的账号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 自动计算充足 gas。注意："auto" 选项不一定报告准确结果。设置有效的代币值来调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        用于乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 上限则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        update-params-proposal 命令的帮助信息
      --keyring-backend string      选择密钥库的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥库目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加说明的备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx bank](#zetacored-tx-bank)	 - 银行交易子命令

## zetacored tx broadcast

广播离线生成的交易

### 摘要

广播使用 `--generate-only` 标志创建并使用 `sign` 命令签名的交易。从 `[file_path]` 读取交易并将其广播到节点。如果你在输入文件名位置提供了破折号 `-` 参数，则该命令将从标准输入读取。

$ zetacored tx broadcast ./mytxn.json

```
zetacored tx broadcast [file_path] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                           生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string         交易广播模式 (sync|async)
      --chain-id string               网络链 ID
      --dry-run                       忽略 `--gas` 标志并执行交易模拟，但不广播它（启用时，无法访问本地 Keybase）
      --fee-granter string            费用授予者为交易支付费用
      --fee-payer string              费用支付者为交易支付费用，而不是从签名者处扣除
      --fees string                   随交易一同支付的费用；例如：10uatom
      --from string                   用于签名的私钥的名称或地址
      --gas string                    每笔交易设置的 Gas 上限；设置为 "auto" 以自动计算足够的 Gas。注意："auto" 选项并不总是报告准确的结果。设置一个有效的代币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float          乘以交易模拟返回的估算值的调整因子；如果手动设置了 Gas 上限，则忽略此标志（默认值 1）
      --gas-prices string             用于确定交易费用的十进制格式的 Gas 价格（例如 0.1uatom）
      --generate-only                 构建未签名的交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                          broadcast 命令的帮助信息
      --keyring-backend string        选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string            客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                        使用已连接的 Ledger 设备
      --node string                   此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                   为交易添加描述说明的注释（以前是 --memo）
      --offline                       离线模式（不允许任何在线功能）
  -o, --output string                 输出格式 (text|json)
  -s, --sequence uint                 签名账户的序列号（仅限离线模式）
      --sign-mode string              选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration     超时持续时间是交易在内存池中被视为有效的时间段。交易的"无序随机数"将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则该交易将被拒绝。
      --timeout-height uint           已弃用：请改用 `--timeout-duration`。设置一个区块超时高度以防止交易在超过某个高度后被提交
      --tip string                    小费是将转移到目标链上费用支付者的金额。此标志仅在与 `--aux` 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                     启用无序交易交付；必须与 `--timeout-duration` 结合使用
  -y, --yes                           跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                   配置和数据的目录
      --log_format string             日志格式 (json|plain)
      --log_level string              日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color                  禁用彩色日志
      --trace                         出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令

## zetacored tx consensus

共识模块的交易命令

```
zetacored tx consensus [flags]
```

### 选项

```
  -h, --help   consensus 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx consensus update-params-proposal](#zetacored-tx-consensus-update-params-proposal)	 - 提交更新共识模块参数的提案。注意：必须提供完整的参数。

## zetacored tx consensus update-params-proposal

提交一个提案以更新共识模块参数。注意：必须提供完整的参数。

```
zetacored tx consensus update-params-proposal [params] [flags]
```

### 示例

```
zetacored tx consensus update-params-proposal '{ params }'
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式的 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        update-params-proposal 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx consensus](#zetacored-tx-consensus)	 - 共识模块的交易命令

## zetacored tx crisis

危机模块的交易命令

```
zetacored tx crisis [flags]
```

### 选项

```
  -h, --help   危机命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx crisis invariant-broken](#zetacored-tx-crisis-invariant-broken)	 - 提交不变量被破坏的证明

## zetacored tx crisis invariant-broken

提交不变量被破坏的证明

```
zetacored tx crisis invariant-broken [module-name] [invariant-route] --from mykey [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式的 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        invariant-broken 的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时间段。交易的未排序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，并且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crisis](#zetacored-tx-crisis)	 - 危机模块的交易命令

## zetacored tx crosschain

跨链交易子命令

```
zetacored tx crosschain [flags]
```

### 选项

```
  -h, --help   crosschain 命令的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx crosschain abort-stuck-cctx](#zetacored-tx-crosschain-abort-stuck-cctx)	 - 中止一个卡住的 CCTX
* [zetacored tx crosschain add-inbound-tracker](#zetacored-tx-crosschain-add-inbound-tracker)	 - 添加一个入站追踪器
			使用 0:Zeta,1:Gas,2:ERC20
* [zetacored tx crosschain add-outbound-tracker](#zetacored-tx-crosschain-add-outbound-tracker)	 - 添加一个出站追踪器
* [zetacored tx crosschain migrate-tss-funds](#zetacored-tx-crosschain-migrate-tss-funds)	 - 将 TSS 资金迁移到最新的 TSS 地址
* [zetacored tx crosschain refund-aborted](#zetacored-tx-crosschain-refund-aborted)	 - 退款一个已中止的交易，退款地址是可选的，如果未提供，退款将发送到 cctx 的发送者/交易来源。
* [zetacored tx crosschain remove-inbound-tracker](#zetacored-tx-crosschain-remove-inbound-tracker)	 - 移除一个入站追踪器
* [zetacored tx crosschain remove-outbound-tracker](#zetacored-tx-crosschain-remove-outbound-tracker)	 - 移除一个出站追踪器
* [zetacored tx crosschain update-tss-address](#zetacored-tx-crosschain-update-tss-address)	 - 创建一个新的 TSSVoter
* [zetacored tx crosschain vote-gas-price](#zetacored-tx-crosschain-vote-gas-price)	 - 广播消息以投票 gas 价格
* [zetacored tx crosschain vote-inbound](#zetacored-tx-crosschain-vote-inbound)	 - 广播消息以投票入站交易
* [zetacored tx crosschain vote-outbound](#zetacored-tx-crosschain-vote-outbound)	 - 广播消息以投票出站交易
* [zetacored tx crosschain whitelist-erc20](#zetacored-tx-crosschain-whitelist-erc20)	 - 将新的 erc20 代币添加到白名单

## zetacored tx crosschain abort-stuck-cctx

中止一个卡住的 CCTX

```
zetacored tx crosschain abort-stuck-cctx [index] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           以十进制格式表示的 gas 价格，用于确定交易费（例如 0.1uatom）
      --generate-only               构建未签名的交易并写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        关于 abort-stuck-cctx 的帮助
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain add-inbound-tracker

添加一个入站追踪器。使用 0:Zeta,1:Gas,2:ERC20

```
zetacored tx crosschain add-inbound-tracker [chain-id] [tx-hash] [coin-type] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        add-inbound-tracker 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain add-outbound-tracker

添加一个出站追踪器

```
zetacored tx crosschain add-outbound-tracker [chain] [nonce] [tx-hash] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值：200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值：1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如：0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        add-outbound-tracker 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [主机]:[端口]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则被忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain migrate-tss-funds

迁移 TSS 资金到最新的 TSS 地址

```
zetacored tx crosschain migrate-tss-funds [chainID] [amount] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者为交易支付费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        调整因子，用于乘以交易模拟返回的估计值；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           以十进制格式的 Gas 价格来确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名的交易并将其写入 STDOUT（启用时，仅当提供密钥名称时才访问本地 Keybase）
  -h, --help                        migrate-tss-funds 的帮助
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 指向此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置一个区块超时高度以防止交易超过某个高度被提交
      --tip string                  Tip 是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略它。
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain refund-aborted

退还已中止的交易，退款地址为可选参数；如果未提供，退款将发送至 cctx 的发送者/交易发起方。

```
zetacored tx crosschain refund-aborted [cctx-index] [refund-address] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 可自动计算充足 gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估算值的调整系数；如果手动设置 gas 上限则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        refund-aborted 命令帮助信息
      --keyring-backend string      选择密钥环后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加说明的注释（原 --memo 参数）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   交易在内存池中被视为有效的超时时长。交易的无序随机数将被设置为交易创建时间加上传入的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过特定高度后被打包
      --tip string                  将在目标链上转移给费用支付者的小费金额。此标志仅在与 --aux 联用时有效，如果目标链未启用 TipDecorator 则会被忽略
      --unordered                   启用无序交易传输；必须与 --timeout-duration 联用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain remove-inbound-tracker

移除一个入站追踪器

```
zetacored tx crosschain remove-inbound-tracker [chain-id] [tx-hash] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        remove-inbound-tracker 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时长。交易的无序 nonce 将被设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain remove-outbound-tracker

移除一个出站追踪器

```
zetacored tx crosschain remove-outbound-tracker [chain] [nonce] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式的 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        remove-outbound-tracker 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain update-tss-address

创建一个新的 TSSVoter

```
zetacored tx crosschain update-tss-address [pubkey] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           以十进制格式表示的 Gas 价格，用于确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        update-tss-address 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain vote-gas-price

广播消息以投票决定燃料价格

```
zetacored tx crosschain vote-gas-price [chain] [price] [priorityFee] [blockNumber] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的燃料限制；设为 "auto" 以自动计算充足燃料。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回估算值的调整系数；如果手动设置了燃料限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式燃料价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        vote-gas-price 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 指向此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的时长。交易的乱序 nonce 将被设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则会被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain vote-inbound

广播消息以投票一个 inbound

```
zetacored tx crosschain vote-inbound [sender] [senderChainID] [txOrigin] [receiver] [receiverChainID] [amount] [message] [inboundHash] [inBlockHeight] [coinType] [asset] [eventIndex] [protocolContractVersion] [isArbitraryCall] [confirmationMode] [inboundStatus] [flags]
```

### 示例

```
zetacored tx crosschain vote-inbound 0xfa233D806C8EB69548F3c4bC0ABb46FaD4e2EB26 8453 "" 0xfa233D806C8EB69548F3c4bC0ABb46FaD4e2EB26 7000 1000000 "" 0x66b59ad844404e91faa9587a3061e2f7af36f7a7a1a0afaca3a2efd811bc9463 26170791 Gas 0x0000000000000000000000000000000000000000 587 V2 FALSE SAFE SUCCESS
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        vote-inbound 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain vote-outbound

广播消息以投票一个出站交易

```
zetacored tx crosschain vote-outbound [sendHash] [outboundHash] [outBlockHeight] [outGasUsed] [outEffectiveGasPrice] [outEffectiveGasLimit] [valueReceived] [Status] [chain] [outTXNonce] [coinType] [confirmationMode] [flags]
```

### 示例

```
zetacored tx crosschain vote-outbound 0x12044bec3b050fb28996630e9f2e9cc8d6cf9ef0e911e73348ade46c7ba3417a 0x4f29f9199b10189c8d02b83568aba4cb23984f11adf23e7e5d2eb037ca309497 67773716 65646 30011221226 100000 297254 0 137 13812 ERC20 SAFE
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式的 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        vote-outbound 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 参见

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx crosschain whitelist-erc20

将新的 ERC20 代币添加到白名单

```
zetacored tx crosschain whitelist-erc20 [erc20Address] [chainID] [name] [symbol] [decimals] [gasLimit] [liquidityCap] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不进行广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 可自动计算充足的 gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估算值的调整系数；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        whitelist-erc20 命令的帮助信息
      --keyring-backend string      选择密钥库的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥库目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明的备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度之后提交交易
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 继承自父命令的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx crosschain](#zetacored-tx-crosschain)	 - 跨链交易子命令

## zetacored tx decode

解码一个二进制编码的交易字符串

```
zetacored tx decode [protobuf-byte-string] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 Gas 限制；设置为 "auto" 以自动计算充足的 Gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 Gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        decode 命令的帮助信息
  -x, --hex                         将输入视为十六进制而非 base64
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令

## zetacored tx distribution

分发交易子命令

```
zetacored tx distribution [flags]
```

### 选项

```
  -h, --help   distribution 的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx distribution community-pool-spend-proposal](#zetacored-tx-distribution-community-pool-spend-proposal)	 - 提交一个从社区池支出的提案
* [zetacored tx distribution fund-community-pool](#zetacored-tx-distribution-fund-community-pool)	 - 使用指定金额资助社区池
* [zetacored tx distribution fund-validator-rewards-pool](#zetacored-tx-distribution-fund-validator-rewards-pool)	 - 使用指定金额资助验证者奖励池
* [zetacored tx distribution set-withdraw-addr](#zetacored-tx-distribution-set-withdraw-addr)	 - 更改与地址关联的奖励的默认提款地址
* [zetacored tx distribution update-params-proposal](#zetacored-tx-distribution-update-params-proposal)	 - 提交一个更新分发模块参数的提案。注意：必须提供所有参数。
* [zetacored tx distribution withdraw-all-rewards](#zetacored-tx-distribution-withdraw-all-rewards)	 - 提取委托人的所有委托奖励
* [zetacored tx distribution withdraw-rewards](#zetacored-tx-distribution-withdraw-rewards)	 - 从给定的委托地址提取奖励，如果给定的委托地址是验证者操作员，则可以选择提取验证者佣金
* [zetacored tx distribution withdraw-validator-commission](#zetacored-tx-distribution-withdraw-validator-commission)	 - 从验证者地址提取佣金（必须是验证者操作员）

## zetacored tx distribution community-pool-spend-proposal

提交一个从社区池支出的提案。

```
zetacored tx distribution community-pool-spend-proposal [recipient] [amount] [flags]
```

### 示例

```
$ zetacored tx distribution community-pool-spend-proposal [recipient] 100uatom
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        community-pool-spend-proposal 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分发交易子命令

## zetacored tx distribution fund-community-pool

使用指定金额为社区池注资

### 概要

使用指定金额为社区池注资

示例：
$ zetacored tx distribution fund-community-pool 100uatom --from mykey

```
zetacored tx distribution fund-community-pool [amount] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        fund-community-pool 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分发交易子命令

## zetacored tx distribution fund-validator-rewards-pool

使用指定金额向验证者奖励池注资

```
zetacored tx distribution fund-validator-rewards-pool [val_addr] [amount] [flags]
```

### 示例

```
zetacored tx distribution fund-validator-rewards-pool cosmosvaloper1x20lytyf6zkcrv5edpkfkn8sz578qg5sqfyqnp 100uatom --from mykey
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                           生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string         交易广播模式 (sync|async)
      --chain-id string               网络链 ID
      --dry-run                       忽略 --gas 标志并执行交易模拟，但不广播（启用后无法访问本地密钥库）
      --fee-granter string            费用授予者为交易支付费用
      --fee-payer string              费用支付者代替签名者支付交易费用
      --fees string                   随交易支付的费用；例如：10uatom
      --from string                   用于签名的私钥名称或地址
      --gas string                    每笔交易的 gas 限制；设为 "auto" 可自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float          乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string             用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                 构建未签名交易并将其输出到 STDOUT（启用后，仅在提供密钥名称时访问本地密钥库）
  -h, --help                          fund-validator-rewards-pool 命令的帮助信息
      --keyring-backend string        选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string            客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                        使用已连接的 Ledger 设备
      --node string                   该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                   为交易添加描述说明的注释（原先是 --memo）
      --offline                       离线模式（不允许任何在线功能）
  -o, --output string                 输出格式 (text|json)
  -s, --sequence uint                 签名账户的序列号（仅限离线模式）
      --sign-mode string              选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration     TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则该交易将被拒绝。
      --timeout-height uint           已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                    小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                     启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                           跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                   配置和数据的目录
      --log_format string             日志格式 (json|plain)
      --log_level string              日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                  禁用彩色日志
      --trace                         出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分发交易子命令

## zetacored tx distribution set-withdraw-addr

更改与地址关联的奖励的默认提现地址。

### 概要

设置与委托者地址关联的奖励的提现地址。

示例：
$ zetacored tx distribution set-withdraw-addr zeta1gghjut3ccd8ay0zduzj64hwre2fxs9ld75ru9p --from mykey

```
zetacored tx distribution set-withdraw-addr [withdraw-addr] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        set-withdraw-addr 命令的帮助信息
      --keyring-backend string      选择密钥环后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述备注（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分发交易子命令

## zetacored tx distribution update-params-proposal

提交更新分配模块参数的提案。注意：必须提供完整的参数。

```
zetacored tx distribution update-params-proposal [params] [flags]
```

### 示例

```
zetacored tx distribution update-params-proposal '{ "community_tax": "20000", "base_proposer_reward": "0", "bonus_proposer_reward": "0", "withdraw_addr_enabled": true }'
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用后，本地 Keybase 不可访问）
      --fee-granter string          费用资助者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 Gas 限制；设为 "auto" 以自动计算充足的 Gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整系数；如果手动设置了 Gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的 Gas 价格（十进制格式，例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用后，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        update-params-proposal 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加说明的注释（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时间段。交易的无序随机数将设置为交易创建时间加上传递的 duration 值。如果交易仍在内存池中，并且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在超过某个高度后提交交易
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分配交易子命令

## zetacored tx distribution withdraw-all-rewards

提取委托者的所有委托奖励

### 概要

提取单个委托者的所有奖励。  
注意，如果您将此命令与 `--broadcast-mode=sync` 或 `--broadcast-mode=async` 一起使用，`max-msgs` 标志将自动设置为 0。

示例：  
`$ zetacored tx distribution withdraw-all-rewards --from mykey`

```
zetacored tx distribution withdraw-all-rewards [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        withdraw-all-rewards 命令的帮助信息
      --keyring-backend string      选择密钥库的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥库目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --max-msgs int                限制每笔交易的消息数量（0 表示无限制）
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（原 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分发交易子命令

## zetacored tx distribution withdraw-rewards

从给定的委托地址提取奖励，如果给定的委托地址是验证者操作员，则可以选择提取验证者佣金。

### 概要

从给定的委托地址提取奖励，如果给定的委托地址是验证者操作员，则可以选择提取验证者佣金。

示例：
$ zetacored tx distribution withdraw-rewards zetavaloper1gghjut3ccd8ay0zduzj64hwre2fxs9ldmqhffj --from mykey
$ zetacored tx distribution withdraw-rewards zetavaloper1gghjut3ccd8ay0zduzj64hwre2fxs9ldmqhffj --from mykey --commission

```
zetacored tx distribution withdraw-rewards [validator-addr] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --commission                  除了奖励外，还提取验证者的佣金
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        withdraw-rewards 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分发交易子命令

## zetacored tx distribution withdraw-validator-commission

从一个验证者地址提取佣金（必须是验证者操作者）

```
zetacored tx distribution withdraw-validator-commission [validator-addr] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync | async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 `--gas` 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 `auto` 以自动计算足够的 gas。注意：`auto` 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 `fees` 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        withdraw-validator-commission 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os | file | kwallet | pass | test | memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 `home` 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text | json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct | amino-json | direct-aux | textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json | plain）
      --log_level string            日志级别（trace | debug | info | warn | error | fatal | panic | disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx distribution](#zetacored-tx-distribution)	 - 分发交易子命令

## zetacored tx emissions

排放交易子命令

```
zetacored tx emissions [flags]
```

### 选项

```
  -h, --help   help for emissions
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx emissions withdraw-emission](#zetacored-tx-emissions-withdraw-emission)	 - 创建一个新的 withdrawEmission

## zetacored tx emissions withdraw-emission

创建新的 withdrawEmission

```
zetacored tx emissions withdraw-emission [amount] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 以自动计算充足 gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        withdraw-emission 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  此链的 CometBFT rpc 接口的 [主机]:[端口]
      --note string                 为交易添加描述说明（原 --memo 参数）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时间段。交易的无序随机数将被设置为交易创建时间加上传递的 duration 值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx emissions](#zetacored-tx-emissions)	 - 排放交易子命令

## zetacored tx encode

编码离线生成的交易

### 概要

编码使用 `--generate-only` 标志创建或使用 `sign` 命令签名的交易。  
从 `[file]` 读取交易，将其序列化为 Protobuf 线路协议，并以 base64 格式输出。  
如果您提供破折号 (-) 参数代替输入文件名，则命令从标准输入读取。

```
zetacored tx encode [file] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        encode 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令

## zetacored tx evidence

证据交易子命令

```
zetacored tx evidence [flags]
```

### 选项

```
  -h, --help   evidence 子命令的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志记录格式 (json|plain)
      --log_level string    日志记录级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令

## zetacored tx evm

evm 子命令

```
zetacored tx evm [flags]
```

### 选项

```
  -h, --help   evm 的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx evm raw](#zetacored-tx-evm-raw)	 - 从原始 ethereum 交易构建 cosmos 交易
* [zetacored tx evm send](#zetacored-tx-evm-send)	 - 将资金从一个账户发送到另一个账户。

## zetacored tx evm raw

从原始以太坊交易构建 Cosmos 交易

```
zetacored tx evm raw TX_HEX [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        针对交易模拟返回的估算值相乘的调整系数；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        raw 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明的备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被认为有效的时间。交易的乱序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx evm](#zetacored-tx-evm)	 - evm 子命令

## zetacored tx evm send

从一个账户向另一个账户发送资金。

### 概要

从一个账户向另一个账户发送资金。可以使用 0x 地址和 bech32 地址。
请注意，`--from` 标志会被忽略，因为它已隐含在 [from_key_or_address] 中。
当使用 `--dry-run` 时，不能使用密钥名称，只能使用 0x 或 bech32 地址。

```
zetacored tx evm send [from_key_or_address] [to_address] [amount] [flags]
```

### 示例

```
evmd tx evm send 0x7cB61D4117AE31a12E393a1Cfa3BaC666481D02E 0xA2A8B87390F8F2D188242656BFb6852914073D06 10utoken
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                          生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不广播（启用后，无法访问本地密钥库）
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 限制；设为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回的估算值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名交易并将其写入 STDOUT（启用后，仅在提供密钥名称时访问本地密钥库）
  -h, --help                         获取 send 命令的帮助
      --keyring-backend string       选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加描述的备注（之前是 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅限离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，并且区块时间已超过提交时间加 TimeoutTimestamp，则该交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                   Tip 是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                    启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx evm](#zetacored-tx-evm)	 - evm 子命令

## zetacored tx feemarket

费用市场模块的交易命令

```
zetacored tx feemarket [flags]
```

### 选项

```
  -h, --help   获取 feemarket 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx feemarket update-params](#zetacored-tx-feemarket-update-params)	 - 执行 UpdateParams RPC 方法

## zetacored tx feemarket update-params

执行 UpdateParams RPC 方法

```
zetacored tx feemarket update-params [flags]
```

### 选项

```
  -a, --account-number uint                            签名账户的账户编号（仅离线模式可用）
      --aux                                            生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string                          交易广播模式 (sync|async) 
      --chain-id string                                网络链 ID
      --dry-run                                        忽略 --gas 标志并执行交易模拟，但不进行广播（启用时无法访问本地 Keybase）
      --fee-granter string                             费用资助者为交易支付费用
      --fee-payer string                               费用支付者代替签名者支付交易费用
      --fees string                                    随交易支付的费用；例如：10uatom
      --from string                                    用于签名的私钥名称或地址
      --gas string                                     每笔交易的 gas 限制；设为 "auto" 可自动计算充足 gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float                           用于乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 限制，则此标志将被忽略（默认值 1）
      --gas-prices string                              用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                                  构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时才访问本地 Keybase）
  -h, --help                                           update-params 命令的帮助信息
      --keyring-backend string                         选择钥匙环的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string                             客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                                         使用已连接的 Ledger 设备
      --node string                                    此链的 CometBFT rpc 接口 [host]:[port] 
      --note string                                    为交易添加说明的备注（之前为 --memo）
      --offline                                        离线模式（不允许任何在线功能）
  -o, --output string                                  输出格式 (text|json) 
      --params cosmos.evm.feemarket.v1.Params (json)   
  -s, --sequence uint                                  签名账户的序列号（仅离线模式可用）
      --sign-mode string                               选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration                      TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，则交易将被拒绝。
      --timeout-height uint                            已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                                     小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则会被忽略
      --unordered                                      启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                                            跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx feemarket](#zetacored-tx-feemarket)	 - feemarket 模块的交易命令

## zetacored tx fungible

同质化代币交易子命令

```
zetacored tx fungible [flags]
```

### 选项

```
  -h, --help   同质化命令的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx fungible deploy-fungible-coin-zrc-4](#zetacored-tx-fungible-deploy-fungible-coin-zrc-4)	 - 广播消息 DeployFungibleCoinZRC20
* [zetacored tx fungible deploy-system-contracts](#zetacored-tx-fungible-deploy-system-contracts)	 - 广播消息 SystemContracts
* [zetacored tx fungible pause-zrc20](#zetacored-tx-fungible-pause-zrc20)	 - 广播消息 PauseZRC20
* [zetacored tx fungible remove-foreign-coin](#zetacored-tx-fungible-remove-foreign-coin)	 - 广播消息 RemoveForeignCoin
* [zetacored tx fungible unpause-zrc20](#zetacored-tx-fungible-unpause-zrc20)	 - 广播消息 UnpauseZRC20
* [zetacored tx fungible update-contract-bytecode](#zetacored-tx-fungible-update-contract-bytecode)	 - 广播消息 UpdateContractBytecode
* [zetacored tx fungible update-gateway-contract](#zetacored-tx-fungible-update-gateway-contract)	 - 广播消息 UpdateGatewayContract 以更新网关合约地址
* [zetacored tx fungible update-system-contract](#zetacored-tx-fungible-update-system-contract)	 - 广播消息 UpdateSystemContract
* [zetacored tx fungible update-zrc20-liquidity-cap](#zetacored-tx-fungible-update-zrc20-liquidity-cap)	 - 广播消息 UpdateZRC20LiquidityCap
* [zetacored tx fungible update-zrc20-withdraw-fee](#zetacored-tx-fungible-update-zrc20-withdraw-fee)	 - 广播消息 UpdateZRC20WithdrawFee

## zetacored tx fungible deploy-fungible-coin-zrc-4

广播消息 DeployFungibleCoinZRC20

```
zetacored tx fungible deploy-fungible-coin-zrc-4 [erc-20] [foreign-chain] [decimals] [name] [symbol] [coin-type] [gas-limit] [liquidity-cap] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                          生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不进行广播（启用后无法访问本地 Keybase）
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 Gas 限制；设为 "auto" 可自动计算充足 Gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回估算值的调整系数；如果手动设置了 Gas 限制，则忽略此标志（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                         deploy-fungible-coin-zrc-4 命令帮助信息
      --keyring-backend string       选择密钥环后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口 [host]:[port]
      --note string                  为交易添加描述说明（之前为 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅限离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    超时时长是交易在内存池中被视为有效的时长。交易的无序 nonce 将被设置为交易创建时间加上传入的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                   小费是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则会被忽略
      --unordered                    启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                  配置和数据目录
      --log_format string            日志格式 (json|plain)
      --log_level string             日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                 禁用彩色日志
      --trace                        在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 可互换代币交易子命令

## zetacored tx fungible deploy-system-contracts

广播消息 SystemContracts

```
zetacored tx fungible deploy-system-contracts [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的 Gas 价格（十进制格式，例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        获取 deploy-system-contracts 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 可替代代币交易子命令

## zetacored tx fungible pause-zrc20

广播消息 PauseZRC20

```
zetacored tx fungible pause-zrc20 [contractAddress1, contractAddress2, ...] [flags]
```

### 示例

```
zetacored tx fungible pause-zrc20 "0xece40cbB54d65282c4623f141c4a8a0bE7D6AdEc, 0xece40cbB54d65282c4623f141c4a8a0bEjgksncf" 
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        pause-zrc20 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 同质化交易子命令

## zetacored tx fungible remove-foreign-coin

广播消息 RemoveForeignCoin

```
zetacored tx fungible remove-foreign-coin [name] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不进行广播（启用后，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估算值的调整因子；如果手动设置了 gas 限制，则此标志将被忽略（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其输出到 STDOUT（启用后，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        remove-foreign-coin 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的未排序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，并且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则将被忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 可替代代币交易子命令

## zetacored tx fungible unpause-zrc20

广播 UnpauseZRC20 消息

```
zetacored tx fungible unpause-zrc20 [contractAddress1, contractAddress2, ...] [flags]
```

### 示例

```
zetacored tx fungible unpause-zrc20 "0xece40cbB54d65282c4623f141c4a8a0bE7D6AdEc, 0xece40cbB54d65282c4623f141c4a8a0bEjgksncf" 
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，无法访问本地 Keybase）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的 Gas 价格（十进制格式，例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        unpause-zrc20 命令帮助
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  指向此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（以前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度之后被提交
      --tip string                  小费是将要在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 可互换代币交易子命令

## zetacored tx fungible update-contract-bytecode

广播消息 UpdateContractBytecode

```
zetacored tx fungible update-contract-bytecode [contract-address] [new-code-hash] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async) 
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者为交易支付费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  设置每笔交易的 gas 限制；设置为 `auto` 以自动计算足够的 gas。注意：`auto` 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 `fees` 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的 Gas 价格，以十进制格式（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        update-contract-bytecode 的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 `home` 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port] 
      --note string                 为交易添加描述说明（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json) 
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录 
      --log_format string   日志格式 (json|plain) 
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - fungible 交易子命令

## zetacored tx fungible update-gateway-contract

广播 UpdateGatewayContract 消息以更新网关合约地址

```
zetacored tx fungible update-gateway-contract [contract-address] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账号编号（仅限离线模式）
      --aux                          生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不进行广播（启用时无法访问本地 Keybase）
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 限制；设为 "auto" 可自动计算充足 gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回的估算值的调整系数；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                         update-gateway-contract 命令帮助
      --keyring-backend string       选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加说明的备注（之前为 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅限离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                   小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                    启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 可互换代币交易子命令

## zetacored tx fungible update-system-contract

广播消息 UpdateSystemContract

```
zetacored tx fungible update-system-contract [contract-address]  [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的燃气限制；设置为 "auto" 以自动计算充足燃气。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估计值的调整因子；如果手动设置燃气限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式燃气价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        update-system-contract 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述备注（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 可替代代币交易子命令

## zetacored tx fungible update-zrc20-liquidity-cap

广播消息 UpdateZRC20LiquidityCap

```
zetacored tx fungible update-zrc20-liquidity-cap [zrc20] [liquidity-cap] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 上限；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        update-zrc20-liquidity-cap 命令帮助
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易超过特定高度后被提交
      --tip string                  小费是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则被忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### SEE ALSO

* [zetacored tx fungible](#zetacored-tx-fungible)	 - fungible transactions subcommands

## zetacored tx fungible update-zrc20-withdraw-fee

广播消息 UpdateZRC20WithdrawFee

```
zetacored tx fungible update-zrc20-withdraw-fee [contractAddress] [newWithdrawFee] [newGasLimit] [flags]
```

### 选项

```
  -a, --account-number uint         The account number of the signing account (offline mode only)
      --aux                         Generate aux signer data instead of sending a tx
  -b, --broadcast-mode string       Transaction broadcasting mode (sync|async) 
      --chain-id string             The network chain ID
      --dry-run                     ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible)
      --fee-granter string          Fee granter grants fees for the transaction
      --fee-payer string            Fee payer pays fees for the transaction instead of deducting from the signer
      --fees string                 Fees to pay along with transaction; eg: 10uatom
      --from string                 Name or address of private key with which to sign
      --gas string                  gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically. Note: "auto" option doesn't always report accurate results. Set a valid coin value to adjust the result. Can be used instead of "fees". (default 200000)
      --gas-adjustment float        adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored  (default 1)
      --gas-prices string           Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom)
      --generate-only               Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name)
  -h, --help                        help for update-zrc20-withdraw-fee
      --keyring-backend string      Select keyring's backend (os|file|kwallet|pass|test|memory) 
      --keyring-dir string          The client Keyring directory; if omitted, the default 'home' directory will be used
      --ledger                      Use a connected Ledger device
      --node string                 [host]:[port] to CometBFT rpc interface for this chain 
      --note string                 Note to add a description to the transaction (previously --memo)
      --offline                     Offline mode (does not allow any online functionality)
  -o, --output string               Output format (text|json) 
  -s, --sequence uint               The sequence number of the signing account (offline mode only)
      --sign-mode string            Choose sign mode (direct|amino-json|direct-aux|textual), this is an advanced feature
      --timeout-duration duration   TimeoutDuration is the duration the transaction will be considered valid in the mempool. The transaction's unordered nonce will be set to the time of transaction creation + the duration value passed. If the transaction is still in the mempool, and the block time has passed the time of submission + TimeoutTimestamp, the transaction will be rejected.
      --timeout-height uint         DEPRECATED: Please use --timeout-duration instead. Set a block timeout height to prevent the tx from being committed past a certain height
      --tip string                  Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator
      --unordered                   Enable unordered transaction delivery; must be used in conjunction with --timeout-duration
  -y, --yes                         Skip tx broadcasting prompt confirmation
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored tx fungible](#zetacored-tx-fungible)	 - 可互换交易子命令

## zetacored tx gov

治理交易子命令

```
zetacored tx gov [flags]
```

### 选项

```
  -h, --help   gov 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx gov cancel-proposal](#zetacored-tx-gov-cancel-proposal)	 - 在投票期结束前取消治理提案。必须由提案创建者签名。
* [zetacored tx gov deposit](#zetacored-tx-gov-deposit)	 - 为活跃提案存入代币
* [zetacored tx gov draft-proposal](#zetacored-tx-gov-draft-proposal)	 - 生成提案草案 json 文件。生成的提案 json 仅包含一条消息（框架）。
* [zetacored tx gov submit-legacy-proposal](#zetacored-tx-gov-submit-legacy-proposal)	 - 提交传统提案及初始质押
* [zetacored tx gov submit-proposal](#zetacored-tx-gov-submit-proposal)	 - 提交提案及相关消息、元数据和质押
* [zetacored tx gov vote](#zetacored-tx-gov-vote)	 - 对活跃提案投票，选项：yes/no/no_with_veto/abstain
* [zetacored tx gov weighted-vote](#zetacored-tx-gov-weighted-vote)	 - 对活跃提案投票，选项：yes/no/no_with_veto/abstain

## zetacored tx gov cancel-proposal

在投票期结束前取消治理提案。必须由提案创建者签名。

```
zetacored tx gov cancel-proposal [proposal-id] [flags]
```

### 示例

```
$ zetacored tx gov cancel-proposal 1 --from mykey
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async) 
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用后，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  设置每笔交易的 gas 上限；设为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估算值的调整系数；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名的交易并将其写入 STDOUT（启用后，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        cancel-proposal 命令的帮助信息
      --keyring-backend string      选择钥匙圈的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string          客户端钥匙圈目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  此链的 CometBFT rpc 接口的 [host]:[port] 
      --note string                 为交易添加描述说明的注释（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json) 
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时长。交易的无序随机数将被设置为交易创建时间 + 传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则该交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain) 
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令

## zetacored tx gov deposit

为活跃提案质押代币

### 概要

为活跃提案提交质押。您可以通过运行 `zetacored query gov proposals` 来查找提案 ID。

示例：
$ zetacored tx gov deposit 1 10stake --from mykey

```
zetacored tx gov deposit [proposal-id] [deposit] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的燃气限制；设为 "auto" 自动计算充足燃气。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回估算值的调整系数；如果手动设置燃气限制则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的燃气价格（十进制格式，例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        deposit 命令帮助
      --keyring-backend string      选择密钥库后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥库目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加说明的备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令

## zetacored tx gov draft-proposal

生成一个草案提案 JSON 文件。生成的提案 JSON 仅包含一条消息（框架）。

```
zetacored tx gov draft-proposal [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        draft-proposal 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [主机]:[端口]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --skip-metadata               跳过元数据提示
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令

## zetacored tx gov submit-legacy-proposal

提交一个旧版提案及其初始存款

### 概要

提交一个旧版提案及其初始存款。
提案标题、描述、类型和存款可以直接提供或通过提案 JSON 文件提供。

示例：
$ zetacored tx gov submit-legacy-proposal --proposal="path/to/proposal.json" --from mykey

其中 proposal.json 包含：

{
  "title": "Test Proposal",
  "description": "My awesome proposal",
  "type": "Text",
  "deposit": "10test"
}

等效于：

$ zetacored tx gov submit-legacy-proposal --title="Test Proposal" --description="My awesome proposal" --type="Text" --deposit="10test" --from mykey

```
zetacored tx gov submit-legacy-proposal [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --deposit string              提案存款
      --description string          提案描述
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时才访问本地密钥库）
  -h, --help                        submit-legacy-proposal 命令的帮助
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
      --proposal string             提案文件路径（如果给出此路径，则忽略其他提案标志）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --title string                提案标题
      --type string                 提案类型
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令

## zetacored tx gov submit-proposal

提交一个提案，包括一些消息、元数据和存款

### 概要

提交一个提案，包括一些消息、元数据和存款。  
它们应该在一个 JSON 文件中定义。

示例：  
```bash
$ zetacored tx gov submit-proposal path/to/proposal.json
```

其中 `proposal.json` 包含：

```json
{
  // proto-JSON 编码的 sdk.Msgs 数组
  "messages": [
    {
      "@type": "/cosmos.bank.v1beta1.MsgSend",
      "from_address": "cosmos1...",
      "to_address": "cosmos1...",
      "amount":[{"denom": "stake","amount": "10"}]
    }
  ],
  // 元数据可以是 base64 编码、原始文本、字符串化 JSON 或指向 JSON 的 IPFS 链接
  // 参见下面的元数据示例
  "metadata": "4pIMOgIGx1vZGU=",
  "deposit": "10stake",
  "title": "My proposal",
  "summary": "A short summary of my proposal",
  "expedited": false
}
```

元数据示例：  
```json
{
	"title": "",
	"authors": [""],
	"summary": "",
	"details": "", 
	"proposal_forum_url": "",
	"vote_option_context": "",
}
```

```
zetacored tx gov submit-proposal [path/to/proposal.json] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的 Gas 价格（十进制格式，例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        submit-proposal 命令的帮助信息
      --keyring-backend string      选择密钥库的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥库目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时间段。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 参见

* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令

## zetacored tx gov vote

为活跃提案投票，选项：yes/no/no_with_veto/abstain

### 概要

为活跃提案提交投票。您可以通过运行 `zetacored query gov proposals` 来查找提案 ID。

示例：
$ zetacored tx gov vote 1 yes --from mykey

```
zetacored tx gov vote [proposal-id] [option] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        vote 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --metadata string             指定投票的元数据
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的时间。交易的乱序 nonce 将被设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令

## zetacored tx gov weighted-vote

对活跃提案进行投票，选项：yes/no/no_with_veto/abstain

### 概要

提交对活跃提案的投票。您可以通过运行 `zetacored query gov proposals` 来查找提案 ID。

示例：
$ zetacored tx gov weighted-vote 1 yes=0.6,no=0.3,abstain=0.05,no_with_veto=0.05 --from mykey

```
zetacored tx gov weighted-vote [proposal-id] [weighted-options] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者为交易支付费用，而非从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        weighted-vote 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --metadata string             指定加权投票的元数据
      --node string                 该链的 CometBFT rpc 接口的 [主机]:[端口]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时间段。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx gov](#zetacored-tx-gov)	 - 治理交易子命令

## zetacored tx group

群组交易子命令

```
zetacored tx group [flags]
```

### 选项

```
  -h, --help   获取 group 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx group create-group](#zetacored-tx-group-create-group)	 - 创建一个群组，该群组是具有关联权重和管理员账户的成员账户的聚合
* [zetacored tx group create-group-policy](#zetacored-tx-group-create-group-policy)	 - 创建一个群组策略，该策略是与群组和决策策略关联的账户。注意，`--from` 标志会被忽略，因为它从 [admin] 隐含得出
* [zetacored tx group create-group-with-policy](#zetacored-tx-group-create-group-with-policy)	 - 创建带有策略的群组，该群组是具有关联权重、管理员账户和决策策略的成员账户的聚合
* [zetacored tx group draft-proposal](#zetacored-tx-group-draft-proposal)	 - 生成一个提案草稿 json 文件。生成的提案 json 仅包含一条消息（框架）
* [zetacored tx group exec](#zetacored-tx-group-exec)	 - 执行提案
* [zetacored tx group leave-group](#zetacored-tx-group-leave-group)	 - 从群组中移除成员
* [zetacored tx group submit-proposal](#zetacored-tx-group-submit-proposal)	 - 提交新提案
* [zetacored tx group update-group-admin](#zetacored-tx-group-update-group-admin)	 - 更新群组管理员
* [zetacored tx group update-group-members](#zetacored-tx-group-update-group-members)	 - 更新群组成员。将成员的权重设置为 "0" 可将其删除
* [zetacored tx group update-group-metadata](#zetacored-tx-group-update-group-metadata)	 - 更新群组的元数据
* [zetacored tx group update-group-policy-admin](#zetacored-tx-group-update-group-policy-admin)	 - 更新群组策略管理员
* [zetacored tx group update-group-policy-decision-policy](#zetacored-tx-group-update-group-policy-decision-policy)	 - 更新群组策略的决策策略
* [zetacored tx group update-group-policy-metadata](#zetacored-tx-group-update-group-policy-metadata)	 - 更新群组策略元数据
* [zetacored tx group vote](#zetacored-tx-group-vote)	 - 对提案进行投票
* [zetacored tx group withdraw-proposal](#zetacored-tx-group-withdraw-proposal)	 - 撤回已提交的提案

## zetacored tx group create-group

创建一个群组，该群组是成员账户的聚合，具有关联的权重和一个管理员账户。

### 概要

创建一个群组，该群组是成员账户的聚合，具有关联的权重和一个管理员账户。  
注意，`--from` 标志被忽略，因为它从 [admin] 隐含。成员账户可以通过一个包含成员数组的 members JSON 文件提供。

```
zetacored tx group create-group [admin] [metadata] [members-json-file] [flags]
```

### 示例

```
zetacored tx group create-group [admin] [metadata] [members-json-file]

其中 members.json 包含：

{
	"members": [
		{
			"address": "addr1",
			"weight": "1",
			"metadata": "some metadata"
		},
		{
			"address": "addr2",
			"weight": "1",
			"metadata": "some metadata"
		}
	]
}
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（当启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替从签名者扣除费用支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式的 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名的交易并将其写入 STDOUT（当启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        create-group 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置一个区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则被忽略。
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group create-group-policy

创建一个群组策略，该策略是与群组和决策策略关联的账户。注意，`--from` 标志被忽略，因为它从 [admin] 隐含。

```
zetacored tx group create-group-policy [admin] [group-id] [metadata] [decision-policy-json-file] [flags]
```

### 示例

```
zetacored tx group create-group-policy [admin] [group-id] [metadata] policy.json
```

其中 policy.json 包含：

```json
{
    "@type": "/cosmos.group.v1.ThresholdDecisionPolicy",
    "threshold": "1",
    "windows": {
        "voting_period": "120h",
        "min_execution_period": "0s"
    }
}
```

在这里，当需要时我们可以使用百分比决策策略，其中 0 < percentage <= 1：

```json
{
    "@type": "/cosmos.group.v1.PercentageDecisionPolicy",
    "percentage": "0.5",
    "windows": {
        "voting_period": "120h",
        "min_execution_period": "0s"
    }
}
```

### 选项

```
  -a, --account-number uint         签名账户的账户号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        create-group-policy 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### SEE ALSO

* [zetacored tx group](#zetacored-tx-group)	 - Group transaction subcommands

## zetacored tx group create-group-with-policy

创建一个带有策略的群组，该策略是成员账户及其关联权重的聚合，包括一个管理员账户和决策策略。

### 概要

创建一个带有策略的群组，该策略是成员账户及其关联权重的聚合，包括一个管理员账户和决策策略。注意，`--from` 标志被忽略，因为它从 [admin] 隐含。
成员账户可以通过一个包含成员数组的 members JSON 文件提供。
如果 group-policy-as-admin 标志设置为 true，则新创建的群组和群组策略的管理员被设置为群组策略地址本身。

```
zetacored tx group create-group-with-policy [admin] [group-metadata] [group-policy-metadata] [members-json-file] [decision-policy-json-file] [flags]
```

### 示例

```

zetacored tx group create-group-with-policy [admin] [group-metadata] [group-policy-metadata] members.json policy.json

其中 members.json 包含：

{
	"members": [
		{
			"address": "addr1",
			"weight": "1",
			"metadata": "some metadata"
		},
		{
			"address": "addr2",
			"weight": "1",
			"metadata": "some metadata"
		}
	]
}

且 policy.json 包含：

{
    "@type": "/cosmos.group.v1.ThresholdDecisionPolicy",
    "threshold": "1",
    "windows": {
        "voting_period": "120h",
        "min_execution_period": "0s"
    }
}

```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
      --group-policy-as-admin       当为 true 时，将新创建的群组和群组策略的管理员设置为群组策略地址本身
  -h, --help                        create-group-with-policy 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时长。交易的无序随机数将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group draft-proposal

生成一个草案提案 JSON 文件。生成的提案 JSON 仅包含一个消息（框架）。

```
zetacored tx group draft-proposal [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        针对交易模拟返回的估计值乘上的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的 Gas 价格，以十进制格式（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        draft-proposal 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --skip-metadata               跳过元数据提示
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 组交易子命令

## zetacored tx group exec

执行提案

```
zetacored tx group exec [proposal-id] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                          生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，本地密钥库不可访问）
      --fee-granter string           费用资助者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 上限；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回估算值的调整因子；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                         exec 命令的帮助信息
      --keyring-backend string       选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加描述说明的注释（之前为 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅限离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的时间段。交易的乱序 nonce 将被设置为交易创建时间加上传递的 duration 值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度之后提交交易
      --tip string                   小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                    启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                  配置和数据的目录
      --log_format string            日志格式 (json|plain)
      --log_level string             日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                 禁用彩色日志
      --trace                        出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group leave-group

从群组中移除成员

### 概要

从群组中移除成员

参数：
		   group-id: 群组的唯一标识符
		   member-address: 群组成员的账户地址
		   注意，`--from` 标志被忽略，因为它从 [member-address] 隐含
		

```
zetacored tx group leave-group [member-address] [group-id] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async) 
      --chain-id string             网络链 ID
      --dry-run                     忽略 `--gas` 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          为交易授予费用的费用授予者
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        leave-group 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port] 
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json) 
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain) 
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group submit-proposal

提交新提案

### 概要

提交一个新提案。
参数：
			msg_tx_json_file：包含在提案被接受时将执行的消息的 JSON 文件路径。

```
zetacored tx group submit-proposal [proposal_json_file] [flags]
```

### 示例

```

zetacored tx group submit-proposal path/to/proposal.json
	
	其中 proposal.json 包含：

{
	"group_policy_address": "cosmos1...",
	// proto-JSON 编码的 sdk.Msgs 数组
	"messages": [
	{
		"@type": "/cosmos.bank.v1beta1.MsgSend",
		"from_address": "cosmos1...",
		"to_address": "cosmos1...",
		"amount":[{"denom": "stake","amount": "10"}]
	}
	],
	// 元数据可以是 base64 编码、原始文本、字符串化 JSON 或指向 JSON 的 IPFS 链接
	// 参见下面的元数据示例
	"metadata": "4pIMOgIGx1vZGU=", // base64 编码的元数据
	"title": "My proposal",
	"summary": "This is a proposal to send 10 stake to cosmos1...",
	"proposers": ["cosmos1...", "cosmos1..."],
}

元数据示例： 
{
	"title": "",
	"authors": [""],
	"summary": "",
	"details": "", 
	"proposal_forum_url": "",
	"vote_option_context": "",
} 

```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --exec string                 设置为 1 或 'try' 以在创建提案后立即尝试执行（提案者签名被视为赞成票）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的燃气限制；设置为 "auto" 以自动计算充足燃气。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置燃气限制，则忽略此标志（默认 1）
      --gas-prices string           十进制格式的燃气价格，用于确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        submit-proposal 命令帮助
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 参见

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group update-group-admin

更新群组的管理员

```
zetacored tx group update-group-admin [admin] [group-id] [new-admin] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync｜async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        针对交易模拟返回的估算值相乘的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        update-group-admin 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os｜file｜kwallet｜pass｜test｜memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text｜json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct｜amino-json｜direct-aux｜textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的乱序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json｜plain）
      --log_level string            日志级别（trace｜debug｜info｜warn｜error｜fatal｜panic｜disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 参见

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group update-group-members

更新群组成员。将成员的权重设置为 "0" 即可删除该成员。

```
zetacored tx group update-group-members [admin] [group-id] [members-json-file] [flags]
```

### 示例

```

zetacored tx group update-group-members [admin] [group-id] [members-json-file]

其中 members.json 文件包含：

{
	"members": [
		{
			"address": "addr1",
			"weight": "1",
			"metadata": "some new metadata"
		},
		{
			"address": "addr2",
			"weight": "0",
			"metadata": "some metadata"
		}
	]
}

将成员的权重设置为 "0" 即可删除该成员。

```

### 选项

```
  -a, --account-number uint          签名账户的账号（仅离线模式）
      --aux                          生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不广播（启用后，本地 Keybase 不可访问）
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确的结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float         乘以交易模拟返回的估算值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string            Gas 价格（十进制格式），用于确定交易费用（例如 0.1uatom）
      --generate-only                构建未签名的交易并将其写入 STDOUT（启用后，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                         update-group-members 命令的帮助信息
      --keyring-backend string       选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加描述的备注（之前是 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，并且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度之后提交交易
      --tip string                   小费是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                    启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                  配置和数据的目录
      --log_format string            日志格式 (json|plain)
      --log_level string             日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                 禁用彩色日志
      --trace                        出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group update-group-metadata

更新群组元数据

```
zetacored tx group update-group-metadata [admin] [group-id] [metadata] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 可自动计算充足 gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值来调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        update-group-metadata 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 指向该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加说明的注释（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则会被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group update-group-policy-admin

更新群组策略管理员

```
zetacored tx group update-group-policy-admin [admin] [group-policy-account] [new-admin] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络 chain ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        gas 估算的调整因子，与交易模拟返回的估算值相乘；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的 Gas 价格，以十进制格式表示（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时才访问本地 Keybase）
  -h, --help                        update-group-policy-admin 的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 指向此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在 mempool 中被视为有效的持续时间。交易的 unordered nonce 将设置为交易创建时间 + 传递的持续时间值。如果交易仍在 mempool 中，且区块时间已超过提交时间 + TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易超过某个高度后被提交
      --tip string                  Tip 是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 参见

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group update-group-policy-decision-policy

更新群组策略的决策策略

```
zetacored tx group update-group-policy-decision-policy [admin] [group-policy-account] [decision-policy-json-file] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        update-group-policy-decision-policy 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group update-group-policy-metadata

更新群组策略元数据

```
zetacored tx group update-group-policy-metadata [admin] [group-policy-account] [new-metadata] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        update-group-policy-metadata 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 指向此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加说明的注释（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时长。交易的乱序 nonce 将被设置为交易创建时间加上传递的 duration 值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group vote

对提案进行投票

### 概要

对提案进行投票。

参数：
			proposal-id: 提案的唯一 ID
			voter: 投票者账户地址
			vote-option: 投票者的选择
				VOTE_OPTION_UNSPECIFIED: 无操作
				VOTE_OPTION_NO: 反对
				VOTE_OPTION_YES: 赞成
				VOTE_OPTION_ABSTAIN: 弃权
				VOTE_OPTION_NO_WITH_VETO: 反对并否决
			metadata: 投票的元数据

```
zetacored tx group vote [proposal-id] [voter] [vote-option] [metadata] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账号编号（仅离线模式）
      --aux                          生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async) 
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不广播（启用后，无法访问本地 Keybase）
      --exec string                  设置为 1 以在投票后立即尝试执行提案
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 限制；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回的预估值的调整系数；如果手动设置了 gas 限制，则此标志被忽略（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名的交易并将其写入 STDOUT（启用后，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                         vote 命令的帮助信息
      --keyring-backend string       选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string           客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  此链的 CometBFT rpc 接口的 [host]:[port] 
      --note string                  为交易添加说明的注释（之前为 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json) 
  -s, --sequence uint                签名账户的序列号（仅离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的时间长度。交易的无序 nonce 将被设置为交易创建时间加上传递的 duration 值。如果交易仍在内存池中，并且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                   小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                    启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                  配置和数据的目录
      --log_format string            日志格式 (json|plain) 
      --log_level string             日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color                 禁用彩色日志
      --trace                        出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 群组交易子命令

## zetacored tx group withdraw-proposal

撤回已提交的提案

### 概要

撤回已提交的提案。

参数：
			proposal-id: 提案的唯一 ID。
			group-policy-admin-or-proposer: 组策略的管理员或提案的提议者之一。
			注意：--from 标志将在此处被忽略。

```
zetacored tx group withdraw-proposal [proposal-id] [group-policy-admin-or-proposer] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        withdraw-proposal 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述备注（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx group](#zetacored-tx-group)	 - 组交易子命令

## zetacored tx lightclient

lightclient 交易子命令

```
zetacored tx lightclient [flags]
```

### 选项

```
  -h, --help   lightclient 的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx lightclient disable-header-verification](#zetacored-tx-lightclient-disable-header-verification)	 - 禁用以逗号分隔的链列表的头部验证
* [zetacored tx lightclient enable-header-verification](#zetacored-tx-lightclient-enable-header-verification)	 - 启用以逗号分隔的链列表的验证

## zetacored tx lightclient disable-header-verification

禁用以逗号分隔的链 ID 列表的头部验证

### 概要

提供一个以逗号分隔的链 ID 列表，以禁用指定链 ID 的区块头部验证。

   示例：
                    要禁用链 ID 1 和 56 的验证标志
					zetacored tx lightclient disable-header-verification "1,56"
				

```
zetacored tx lightclient disable-header-verification [list of chain-id] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           以十进制格式表示的 Gas 价格，用于确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        disable-header-verification 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx lightclient](#zetacored-tx-lightclient)	 - lightclient 交易子命令

## zetacored tx lightclient enable-header-verification

为以逗号分隔的链列表启用验证功能

### 概要

提供一个以逗号分隔的链 ID 列表，为指定的链 ID 启用区块头验证。

  				示例：
                    要为链 ID 1 和 56 启用验证标志
					zetacored tx lightclient enable-header-verification "1,56"
				

```
zetacored tx lightclient enable-header-verification [链ID列表] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                          生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不广播（启用时，无法访问本地 Keybase）
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易设置的 gas 上限；设为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回的估算值的调整因子；如果手动设置了 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                         enable-header-verification 命令的帮助信息
      --keyring-backend string       选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加描述说明（以前是 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅限离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止在超过某个高度后提交交易
      --tip string                   小费是将要在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                    启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                  配置和数据的目录
      --log_format string            日志格式 (json|plain)
      --log_level string             日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color                 禁用彩色日志
      --trace                        在出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx lightclient](#zetacored-tx-lightclient)	 - lightclient 交易子命令

## zetacored tx multi-sign

为离线生成的交易生成多重签名

### 概要

对使用 `--generate-only` 标志创建的、需要多重签名的交易进行签名。

从一个或多个 `[signature]` 文件中读取一个或多个签名，生成符合多重签名密钥 `[name]` 的多重签名，并将密钥名称附加到从 `[file]` 读取的交易中。

示例：
```bash
$ zetacored tx multisign transaction.json k1k2k3 k1sig.json k2sig.json k3sig.json
```

如果 `--signature-only` 标志启用，则仅输出生成签名的 JSON 表示。

如果 `--offline` 标志启用，客户端将不会连接外部节点。不会执行账户编号或序列号查询，因此您必须手动设置这些参数。

如果 `--skip-signature-verification` 标志启用，该命令将不会验证提供的签名文件中的签名。这在多重签名账户是嵌套多重签名场景中的签名者时非常有用。

当前多重签名实现默认为 `amino-json` 签名模式。不支持 `SIGN_MODE_DIRECT` 签名模式。

```bash
zetacored tx multi-sign [file] [name] [[signature]...] [flags]
```

### 选项

```
  -a, --account-number uint           签名账户的账户编号（仅离线模式）
      --aux                           生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string         交易广播模式 (sync|async)
      --chain-id string               网络链 ID
      --dry-run                       忽略 `--gas` 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string            费用授予者为交易授予费用
      --fee-payer string              费用支付者代替签名者支付交易费用
      --fees string                   随交易支付的费用；例如：10uatom
      --from string                   用于签名的私钥名称或地址
      --gas string                    每笔交易的 gas 上限；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float          乘以交易模拟返回估算值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string             用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                 构建未签名交易并写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                          multi-sign 命令帮助
      --keyring-backend string        选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string            客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                        使用已连接的 Ledger 设备
      --node string                   该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                   为交易添加描述备注（先前为 --memo）
      --offline                       离线模式（不允许任何在线功能）
      --output-document string        文档将写入给定文件而非 STDOUT
  -s, --sequence uint                 签名账户的序列号（仅离线模式）
      --sign-mode string              选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --signature-only                仅打印生成的签名，然后退出
      --skip-signature-verification   跳过签名验证
      --timeout-duration duration     超时持续时间是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + 超时时间戳，交易将被拒绝。
      --timeout-height uint           已弃用：请改用 `--timeout-duration`。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                    小费是将转移到目标链上费用支付者的金额。此标志仅在与 `--aux` 一起使用时有效，如果目标链未启用 TipDecorator，则被忽略。
      --unordered                     启用无序交易交付；必须与 `--timeout-duration` 结合使用
  -y, --yes                           跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](##zetacored-tx)	 - 交易子命令

## zetacored tx multisign-batch

从批量签名中批量组装多重签名交易

### 概要

组装由批量签名命令生成的一批多重签名交易。

从一个或多个 [signature] 文件中读取一个或多个签名，生成符合多重签名密钥 [name] 的多重签名，并将密钥名称附加到从 [file] 读取的交易中。

示例：
$ zetacored tx multisign-batch transactions.json multisigk1k2k3 k1sigs.json k2sigs.json k3sig.json

当前多重签名实现默认为 amino-json 签名模式。不支持 SIGN_MODE_DIRECT 签名模式。

```
zetacored tx multisign-batch [file] [name] [[signature-file]...] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        multisign-batch 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --multisig string             交易代表签名的多重签名账户地址
      --no-auto-increment           禁用序列号自动递增
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述备注（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
      --output-document string      文档将写入给定文件而非 STDOUT
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令

## zetacored tx observer

observer 交易子命令

```
zetacored tx observer [flags]
```

### 选项

```
  -h, --help   observer 的帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx observer add-observer](#zetacored-tx-observer-add-observer)	 - 广播消息 add-observer
* [zetacored tx observer disable-cctx](#zetacored-tx-observer-disable-cctx)	 - 禁用 CCTX 的入站和出站
* [zetacored tx observer disable-fast-confirmation](#zetacored-tx-observer-disable-fast-confirmation)	 - 禁用给定链 ID 的快速确认
* [zetacored tx observer enable-cctx](#zetacored-tx-observer-enable-cctx)	 - 启用 CCTX 的入站和出站
* [zetacored tx observer encode](#zetacored-tx-observer-encode)	 - 将 JSON 字符串编码为十六进制
* [zetacored tx observer remove-chain-params](#zetacored-tx-observer-remove-chain-params)	 - 广播消息以移除链参数
* [zetacored tx observer reset-chain-nonces](#zetacored-tx-observer-reset-chain-nonces)	 - 广播消息以重置链 nonces
* [zetacored tx observer update-chain-params](#zetacored-tx-observer-update-chain-params)	 - 广播消息 updateChainParams
* [zetacored tx observer update-gas-price-increase-flags](#zetacored-tx-observer-update-gas-price-increase-flags)	 - 更新 gas 价格增加标志
* [zetacored tx observer update-keygen](#zetacored-tx-observer-update-keygen)	 - 通过组提案更新 keygen 块的命令
* [zetacored tx observer update-observer](#zetacored-tx-observer-update-observer)	 - 广播消息 add-observer
* [zetacored tx observer update-operational-flags](#zetacored-tx-observer-update-operational-flags)	 - 广播消息 UpdateOperationalFlags
* [zetacored tx observer vote-blame](#zetacored-tx-observer-vote-blame)	 - 广播消息 vote-blame
* [zetacored tx observer vote-tss](#zetacored-tx-observer-vote-tss)	 - 投票创建新的 TSS

## zetacored tx observer add-observer

广播添加观察者消息

```
zetacored tx observer add-observer [observer-address] [zetaclient-grantee-pubkey] [add_node_account_only] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用资助者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        add-observer 命令帮助
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - 观察者交易子命令

## zetacored tx observer disable-cctx

禁用 CCTX 的入站和出站

```
zetacored tx observer disable-cctx [disable-inbound] [disable-outbound] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 上限；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估计值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        disable-cctx 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将被设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - 观察者交易子命令

## zetacored tx observer disable-fast-confirmation

禁用对给定链 ID 的快速确认。

```
zetacored tx observer disable-fast-confirmation [chain-id] [flags]
```

### 示例

```
zetacored tx observer disable-fast-confirmation 1
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（同步|异步）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以 tx 模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式的 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        disable-fast-confirmation 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [主机]:[端口]
      --note string                 为交易添加描述说明（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止 tx 在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 参见

* [zetacored tx observer](#zetacored-tx-observer)	 - 观察者交易子命令

## zetacored tx observer enable-cctx

启用 CCTX 的入站和出站

```
zetacored tx observer enable-cctx [enable-inbound] [enable-outbound] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        enable-cctx 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的时长。交易的无序 nonce 将设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令

## zetacored tx observer encode

将 JSON 字符串编码为十六进制。

```
zetacored tx observer encode [file.json] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        encode 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时长。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 参见

* [zetacored tx observer](#zetacored-tx-observer)	 - 观察者交易子命令

## zetacored tx observer remove-chain-params

广播消息以移除链参数

```
zetacored tx observer remove-chain-params [chain-id] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值：200000）
      --gas-adjustment float        针对交易模拟返回的估算值乘上的调整系数；若手动设置 gas 上限则忽略此标志（默认值：1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如：0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        remove-chain-params 的帮助信息
      --keyring-backend string      选择密钥环后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；若省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述备注（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的时长值。若交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 同时使用时有效，若目标链未启用 TipDecorator 则被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 同时使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - 观察者交易子命令

## zetacored tx observer reset-chain-nonces

广播消息以重置链随机数

```
zetacored tx observer reset-chain-nonces [chain-id] [chain-nonce-low] [chain-nonce-high] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估算值的调整因子；如果手动设置了 gas 上限，则此标志被忽略（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        reset-chain-nonces 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加说明的注释（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将要在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令

## zetacored tx observer update-chain-params

广播消息 updateChainParams

```
zetacored tx observer update-chain-params [chain-id] [client-params.json] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           以十进制格式表示的 Gas 价格，用于确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        update-chain-params 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令

## zetacored tx observer update-gas-price-increase-flags

更新 gas 价格增长标志

```
zetacored tx observer update-gas-price-increase-flags [epochLength] [retryInterval] [gasPriceIncreasePercent] [gasPriceIncreaseMax] [maxPendingCctxs] [retryIntervalBTC] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async) 
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估算值的调整系数；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        update-gas-price-increase-flags 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port] 
      --note string                 为交易添加描述的注释（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json) 
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain) 
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令

## zetacored tx observer update-keygen

通过群组提案更新 keygen 块的命令

```
zetacored tx observer update-keygen [block] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        update-keygen 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令

## zetacored tx observer update-observer

广播消息 update-observer

```
zetacored tx observer update-observer [old-observer-address] [new-observer-address] [update-reason] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账号（仅离线模式）
      --aux                          生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不进行广播（启用时无法访问本地 Keybase）
      --fee-granter string           费用授予者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 限制；设为 "auto" 以自动计算充足 gas。注意："auto" 选项不一定能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float         用于乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                         update-observer 命令的帮助信息
      --keyring-backend string       选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --node string                  此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加描述说明（之前为 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
  -s, --sequence uint                签名账户的序列号（仅离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的时间段。交易的无序 nonce 将被设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                   小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则会被忽略
      --unordered                    启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                  配置和数据的目录
      --log_format string            日志格式 (json|plain)
      --log_level string             日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                 禁用彩色日志
      --trace                        出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令

## zetacored tx observer update-operational-flags

广播消息 UpdateOperationalFlags

```
zetacored tx observer update-operational-flags [flags]
```

### 选项

```
  -a, --account-number uint                 签名账户的账户编号（仅限离线模式）
      --aux                                 生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string               交易广播模式（sync|async）
      --chain-id string                     网络链 ID
      --dry-run                             忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string                  费用授予者为交易授予费用
      --fee-payer string                    费用支付者代替签名者支付交易费用
      --fees string                         随交易支付的费用；例如：10uatom
      --file string                         包含 OperationalFlags 的 JSON 文件路径
      --from string                         用于签名的私钥名称或地址
      --gas string                          每笔交易设置的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float                乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string                   用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                       构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                                获取 update-operational-flags 的帮助信息
      --keyring-backend string              选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string                  客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                              使用已连接的 Ledger 设备
      --node string                         该链的 CometBFT rpc 接口的 [主机]:[端口]
      --note string                         为交易添加描述说明（之前为 --memo）
      --offline                             离线模式（不允许任何在线功能）
  -o, --output string                       输出格式（text|json）
      --restart-height int                  协调 zetaclient 重启的高度
  -s, --sequence uint                       签名账户的序列号（仅限离线模式）
      --sign-mode string                    选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --signer-block-time-offset duration   从 zetacore 区块时间开始的偏移量以启动签名
      --timeout-duration duration           TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint                 已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                          小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                           启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                                 跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - 观察者交易子命令

## zetacored tx observer vote-blame

广播消息 vote-blame

```
zetacored tx observer vote-blame [chain-id] [index] [failure-reason] [node-list] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅 offline 模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        vote-blame 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述备注（之前为 --memo）
      --offline                     offline 模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅 offline 模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后提交
      --tip string                  Tip 是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则被忽略。
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx observer](#zetacored-tx-observer)	 - observer 交易子命令

## zetacored tx observer vote-tss

为新 TSS 创建投票

```
zetacored tx observer vote-tss [pubkey] [keygen-block] [status] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者为交易支付费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        调整因子，乘以交易模拟返回的估计值；如果手动设置 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           以十进制格式的 Gas 价格来确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时才访问本地 Keybase）
  -h, --help                        vote-tss 命令的帮助
      --keyring-backend string      选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的乱序随机数将设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                  Tip 是将要转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用乱序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### SEE ALSO

* [zetacored tx observer](#zetacored-tx-observer)	 - 观察者交易子命令

## zetacored tx sign

对离线生成的事务进行签名

### 概要

对使用 `--generate-only` 标志创建的事务进行签名。  
它将从 `[file]` 读取事务，对其进行签名，并打印其 JSON 编码。

如果设置了 `--signature-only` 标志，它将仅输出签名部分。

`--offline` 标志确保客户端不会连接到全节点。  
因此，不会执行账户和序列号查询，并且需要手动设置这些参数。注意，无效值将导致事务失败。

`--multisig=[multisig_key]` 标志代表多签账户密钥生成签名。  
它隐含了 `--signature-only`。完整的多签事务最终可以通过 `multisign` 命令生成。

```
zetacored tx sign [file] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                          生成辅助签名者数据而不是发送事务
  -b, --broadcast-mode string       事务广播模式（sync|async）
      --chain-id string              网络链 ID
      --dry-run                      忽略 `--gas` 标志并执行事务模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string           费用授予者为事务授予费用
      --fee-payer string             费用支付者代替签名者支付事务费用
      --fees string                  随事务支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每事务设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float         乘以事务模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则此标志被忽略（默认值 1）
      --gas-prices string            用于确定事务费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名事务并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                         sign 命令的帮助信息
      --keyring-backend string       选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string           客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                        使用已连接的 Ledger 设备
      --multisig string              代表其进行事务签名的多签账户的地址或密钥名称
      --node string                   连接到该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                   为事务添加描述说明（之前为 --memo）
      --offline                       离线模式（不允许任何在线功能）
  -o, --output string                输出格式（text|json）
      --output-document string       文档将写入给定文件而不是 STDOUT
      --overwrite                     用新签名覆盖现有签名。如果禁用，新签名将被追加
  -s, --sequence uint                签名账户的序列号（仅离线模式）
      --sign-mode string             选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --signature-only               仅打印签名
      --timeout-duration duration    TimeoutDuration 是事务在内存池中被视为有效的持续时间。事务的无序 nonce 将被设置为事务创建时间加上传递的持续时间值。如果事务仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则事务将被拒绝。
      --timeout-height uint          已弃用：请改用 `--timeout-duration`。设置区块超时高度以防止事务在特定高度后被提交
      --tip string                    Tip 是将转移到目标链上费用支付者的金额。此标志仅在与 `--aux` 一起使用时有效，如果目标链未启用 TipDecorator，则此标志被忽略
      --unordered                     启用无序事务传递；必须与 `--timeout-duration` 结合使用
  -y, --yes                          跳过事务广播提示确认
```

### 从父命令继承的选项

```
      --home string                  配置和数据的目录
      --log_format string            日志格式（json|plain）
      --log_level string             日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                 禁用彩色日志
      --trace                        在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 事务子命令

## zetacored tx sign-batch

签署交易批处理文件

### 概要

签署使用 `--generate-only` 生成的交易批处理文件。
该命令处理来自一个文件（每行一个 `StdTx`）或多个文件的交易列表。
然后生成已签名的交易或签名，并打印它们的 JSON 编码，以 `\n` 分隔。
随着签名的生成，该命令会相应更新账户和序列号。

如果设置了 `--signature-only` 标志，它将仅输出签名部分。

`--offline` 标志确保客户端不会连接到全节点。
因此，不会执行账户和序列号查询，并且需要手动设置这些参数。注意，无效值将导致交易失败。序列号将为每个签名的交易自动递增。

当 `offline=false` 时，如果使用 `--account-number` 或 `--sequence` 标志，它们将被忽略并被默认标志值覆盖。

`--multisig=[multisig_key]` 标志代表多签账户密钥生成签名。它隐含 `--signature-only`。

```
zetacored tx sign-batch [file] ([file2]...) [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --append                      合并所有消息并生成单个已签名的交易以进行广播。
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async) 
      --chain-id string             网络链 ID
      --dry-run                     忽略 `--gas` 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名的交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        sign-batch 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory) 
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --multisig string             代表其签署交易的多签账户的地址或密钥名称
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port] 
      --note string                 为交易添加描述的备注（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json) 
      --output-document string      文档将写入给定文件而不是 STDOUT
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --signature-only              仅打印生成的签名，然后退出
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录 
      --log_format string           日志格式 (json|plain) 
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]') 
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令

## zetacored tx slashing

用于 slashing 模块的交易命令

```
zetacored tx slashing [flags]
```

### 选项

```
  -h, --help   help for slashing
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx slashing unjail](#zetacored-tx-slashing-unjail)	 - 解禁被监禁的验证者
* [zetacored tx slashing update-params-proposal](#zetacored-tx-slashing-update-params-proposal)	 - 提交一个提案以更新 slashing 模块参数。注意：必须提供全部参数。

## zetacored tx slashing unjail

解除一个被监禁验证人的监禁状态

```
zetacored tx slashing unjail [flags]
```

### 示例

```
zetacored tx slashing unjail --from [validator]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                           生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string         交易广播模式 (sync|async)
      --chain-id string               网络链 ID
      --dry-run                       忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string            费用授予者为交易支付费用
      --fee-payer string              费用支付者代替签名者支付交易费用
      --fees string                   随交易支付的费用；例如：10uatom
      --from string                   用于签名的私钥名称或地址
      --gas string                    每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float          乘以交易模拟返回的估算值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string             用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                 构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                          unjail 命令的帮助信息
      --keyring-backend string        选择密钥库的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string            客户端密钥库目录；如果省略，将使用默认的 'home' 目录
      --ledger                        使用已连接的 Ledger 设备
      --node string                   该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                   为交易添加描述说明（之前为 --memo）
      --offline                       离线模式（不允许任何在线功能）
  -o, --output string                 输出格式 (text|json)
  -s, --sequence uint                 签名账户的序列号（仅限离线模式）
      --sign-mode string              选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration     TimeoutDuration 是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间 + 传递的时长值。如果交易仍在内存池中，并且区块时间已超过提交时间 + TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint           已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                    小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                     启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                           跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                   配置和数据的目录
      --log_format string             日志格式 (json|plain)
      --log_level string              日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                  禁用彩色日志
      --trace                         在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx slashing](#zetacored-tx-slashing)	 - 惩罚模块的交易命令

## zetacored tx slashing update-params-proposal

提交一个提案来更新 slashing 模块参数。注意：必须提供完整的参数。

### 概要

提交一个提案来更新 slashing 模块参数。注意：必须提供完整的参数。
通过运行 `zetacored query slashing params --output json` 查看需要填写的字段。

```
zetacored tx slashing update-params-proposal [params] [flags]
```

### 示例

```
zetacored tx slashing update-params-proposal '{ "signed_blocks_window": "100", ... }'
```

### 选项

```
  -a, --account-number uint         签名账户的账户号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        update-params-proposal 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx slashing](#zetacored-tx-slashing)	 - slashing 模块的交易命令

## zetacored tx staking

质押交易子命令

```
zetacored tx staking [flags]
```

### 选项

```
  -h, --help   获取 staking 相关帮助
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx staking cancel-unbond](#zetacored-tx-staking-cancel-unbond)	 - 取消解除绑定的委托并重新委托给验证者
* [zetacored tx staking create-validator](#zetacored-tx-staking-create-validator)	 - 创建新的验证者并使用自委托进行初始化
* [zetacored tx staking delegate](#zetacored-tx-staking-delegate)	 - 将流动代币委托给验证者
* [zetacored tx staking edit-validator](#zetacored-tx-staking-edit-validator)	 - 编辑现有的验证者账户
* [zetacored tx staking redelegate](#zetacored-tx-staking-redelegate)	 - 将非流动代币从一个验证者重新委托给另一个验证者
* [zetacored tx staking unbond](#zetacored-tx-staking-unbond)	 - 从验证者解除份额绑定

## zetacored tx staking cancel-unbond

取消解绑委托并重新委托给验证者

### 摘要

取消解绑委托并重新委托给验证者。

示例：
```bash
$ zetacored tx staking cancel-unbond zetavaloper1gghjut3ccd8ay0zduzj64hwre2fxs9ldmqhffj 100stake 2 --from mykey
```

```
zetacored tx staking cancel-unbond [validator-addr] [amount] [creation-height] [flags]
```

### 示例

```bash
$ zetacored tx staking cancel-unbond zetavaloper1gghjut3ccd8ay0zduzj64hwre2fxs9ldmqhffj 100stake 2 --from mykey
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 自动计算充足 gas。注意："auto" 选项不一定报告准确结果。设置有效的代币值来调整结果。可替代 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整系数；如果手动设置 gas 限制则忽略此标志（默认 1）
      --gas-prices string           以十进制格式表示的 gas 价格，用于确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        cancel-unbond 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加说明的备注（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时间段。交易的无序随机数将设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止在特定高度后提交交易
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则被忽略
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx staking](#zetacored-tx-staking)	 - 质押交易子命令

## zetacored tx staking create-validator

创建一个新的验证者，并使用自委托对其进行初始化。

### 概要

通过提交一个包含新验证者详细信息的 JSON 文件，创建一个使用自委托初始化的新验证者。

```
zetacored tx staking create-validator [path/to/validator.json] [flags]
```

### 示例

```
$ zetacored tx staking create-validator path/to/validator.json --from keyname

其中 validator.json 包含：

{
	"pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"oWg2ISpLF405Jcm2vXV+2v4fnjodh6aafuIdeoW+rUw="},
	"amount": "1000000stake",
	"moniker": "myvalidator",
	"identity": "optional identity signature (ex. UPort or Keybase)",
	"website": "validator's (optional) website",
	"security": "validator's (optional) security contact email",
	"details": "validator's (optional) details",
	"commission-rate": "0.1",
	"commission-max-rate": "0.2",
	"commission-max-change-rate": "0.01",
	"min-self-delegation": "1"
}

我们可以使用 `zetacored tendermint show-validator` 获取公钥。
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的燃气限制；设置为 "auto" 以自动计算足够的燃气。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置燃气限制，则忽略此标志（默认 1）
      --gas-prices string           以十进制格式的燃气价格，用于确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        create-validator 命令的帮助信息
      --ip string                   节点的公共 IP。仅当与 --generate-only 结合使用时生效
      --keyring-backend string      选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --node-id string              节点的 ID
      --note string                 为交易添加描述备注（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请使用 --timeout-duration 代替。设置区块超时高度以防止交易在特定高度后提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx staking](#zetacored-tx-staking)	 - 质押交易子命令

## zetacored tx staking delegate

将流动代币委托给验证者

### 概要

从您的钱包中将一定数量的流动代币委托给验证者。

示例：
$ zetacored tx staking delegate cosmosvalopers1l2rsakp388kuv9k8qzq6lrm9taddae7fpx59wm 1000stake --from mykey

```
zetacored tx staking delegate [validator-addr] [amount] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           以十进制格式表示的 gas 价格，用于确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        delegate 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx staking](#zetacored-tx-staking)	 - 质押交易子命令

## zetacored tx staking edit-validator

编辑现有的验证人账户

```
zetacored tx staking edit-validator [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                           生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string        交易广播模式 (sync|async)
      --chain-id string              网络链 ID
      --commission-rate string       新的佣金率百分比
      --details string               验证人的（可选）详细信息
      --dry-run                      忽略 --gas 标志并执行交易模拟，但不进行广播（启用时，本地密钥库不可访问）
      --fee-granter string           费用资助者为交易支付费用
      --fee-payer string             费用支付者代替签名者支付交易费用
      --fees string                  随交易支付的费用；例如：10uatom
      --from string                  用于签名的私钥名称或地址
      --gas string                   每笔交易的 gas 上限；设为 "auto" 以自动计算充足的 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值：200000）
      --gas-adjustment float         乘以交易模拟返回估算值的调整系数；如果手动设置了 gas 上限，则忽略此标志（默认值：1）
      --gas-prices string            用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                构建未签名的交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                         edit-validator 命令的帮助信息
      --identity string              （可选的）身份签名（例如 UPort 或 Keybase）
      --keyring-backend string       选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string           客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                       使用已连接的 Ledger 设备
      --min-self-delegation string   验证人要求的最低自委托数量
      --new-moniker string           验证人名称
      --node string                  此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                  为交易添加描述的备注（之前是 --memo）
      --offline                      离线模式（不允许任何在线功能）
  -o, --output string                输出格式 (text|json)
      --security-contact string      验证人的（可选）安全联系邮箱
  -s, --sequence uint                签名账户的序列号（仅限离线模式）
      --sign-mode string             选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration    TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将被设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，并且区块时间已超过提交时间加上 TimeoutTimestamp，则该交易将被拒绝。
      --timeout-height uint          已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                   小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，并且如果目标链未启用 TipDecorator，则会被忽略
      --unordered                    启用无序交易交付；必须与 --timeout-duration 结合使用
      --website string               验证人的（可选）网站
  -y, --yes                          跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx staking](#zetacored-tx-staking)	 - 质押交易子命令

## zetacored tx staking redelegate

将非流动性代币从一个验证人重新委托到另一个验证人

### 概要

将一定数量的非流动性质押代币从一个验证人重新委托到另一个验证人。

示例：
```bash
$ zetacored tx staking redelegate cosmosvalopers1gghjut3ccd8ay0zduzj64hwre2fxs9ldmqhffj cosmosvalopers1l2rsakp388kuv9k8qzq6lrm9taddae7fpx59wm 100stake --from mykey
```

```
zetacored tx staking redelegate [src-validator-addr] [dst-validator-addr] [amount] [flags]
```

### 选项

```
  -a, --account-number uint          签名账户的账户编号（仅限离线模式）
      --aux                           生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string         交易广播模式 (sync|async)
      --chain-id string               网络链 ID
      --dry-run                       忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string            费用授予者为交易支付费用
      --fee-payer string              费用支付者代替签名者支付交易费用
      --fees string                   随交易支付的费用；例如：10uatom
      --from string                   用于签名的私钥名称或地址
      --gas string                    每笔交易的 gas 限制；设为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的币值来调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float          乘以交易模拟返回的估算值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string             用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only                 构建未签名的交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                          redelegate 命令的帮助信息
      --keyring-backend string        选择 keyring 的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string            客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                        使用已连接的 Ledger 设备
      --node string                   该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                   为交易添加描述说明（之前为 --memo）
      --offline                       离线模式（不允许任何在线功能）
  -o, --output string                 输出格式 (text|json)
  -s, --sequence uint                 签名账户的序列号（仅限离线模式）
      --sign-mode string              选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration     TimeoutDuration 是交易在内存池中被视为有效的时长。交易的未排序随机数将被设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint           已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在超过某个高度后被提交
      --tip string                    Tip 是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则会被忽略
      --unordered                     启用无序交易传递；必须与 --timeout-duration 结合使用
  -y, --yes                           跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                   配置和数据的目录
      --log_format string             日志格式 (json|plain)
      --log_level string              日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                  禁用彩色日志
      --trace                         在出错时打印完整的堆栈跟踪
```

### 另请参阅

* [zetacored tx staking](#zetacored-tx-staking)	 - 质押交易子命令

## zetacored tx staking unbond

从验证者解绑份额

### 简介

从验证者解绑一定数量的已绑定份额。

示例：
$ zetacored tx staking unbond zetavaloper1gghjut3ccd8ay0zduzj64hwre2fxs9ldmqhffj 100stake --from mykey

```
zetacored tx staking unbond [validator-addr] [amount] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的燃气限制；设置为 "auto" 以自动计算足够的燃气。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可以代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置燃气限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的燃气价格（十进制格式，例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        unbond 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，这是一个高级功能
      --timeout-duration duration   超时时长是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在某个高度之后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx staking](#zetacored-tx-staking)	 - 质押交易子命令

## zetacored tx upgrade

升级交易子命令

### 选项

```
  -h, --help   help for upgrade
```

### 从父命令继承的选项

```
      --chain-id string     The network chain ID
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx upgrade cancel-software-upgrade](#zetacored-tx-upgrade-cancel-software-upgrade)	 - 取消当前软件升级提案
* [zetacored tx upgrade cancel-upgrade-proposal](#zetacored-tx-upgrade-cancel-upgrade-proposal)	 - 提交一个提案以取消计划的链升级。
* [zetacored tx upgrade software-upgrade](#zetacored-tx-upgrade-software-upgrade)	 - 提交一个软件升级提案

## zetacored tx upgrade cancel-software-upgrade

取消当前的软件升级提案

### 概要

取消软件升级提案以及初始存款。

```
zetacored tx upgrade cancel-software-upgrade [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --authority string            升级模块权限地址（默认为治理模块）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --deposit string              包含在治理提案中的存款
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者为交易支付费用，而非从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        cancel-software-upgrade 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --metadata string             包含在治理提案中的元数据
      --node string                  此链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加说明的备注（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --summary string              包含在治理提案中的摘要
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --title string                治理提案的标题
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx upgrade](#zetacored-tx-upgrade)	 - 升级交易子命令

## zetacored tx upgrade cancel-upgrade-proposal

提交一个提案以取消计划中的链升级。

```
zetacored tx upgrade cancel-upgrade-proposal [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播它（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者为交易支付费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算足够的 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值来调整结果。可以代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           以十进制格式的 Gas 价格来确定交易费用（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        取消升级提案的帮助
      --keyring-backend string      选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述的注释（之前是 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），这是一个高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将被设置为交易创建时间 + 传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间 + TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易超过某个高度被提交
      --tip string                  Tip 是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略它
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式（json|plain）
      --log_level string    日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx upgrade](#zetacored-tx-upgrade)	 - 升级交易子命令

## zetacored tx upgrade software-upgrade

提交一个软件升级提案

### 概要

提交一个软件升级以及初始存款。
请为升级指定一个唯一的名称和生效高度。
您可以包含信息以引用二进制下载链接，格式需兼容：https://docs.cosmos.network/main/tooling/cosmovisor

```
zetacored tx upgrade software-upgrade [name] (--upgrade-height [height]) (--upgrade-info [info]) [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --authority string            升级模块权限的地址（默认为 gov）
      --aux                         生成辅助签名者数据而不是发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --daemon-name string          正在升级的可执行文件名称（用于升级信息验证）。默认为 DAEMON_NAME 环境变量（如果设置），否则为此可执行文件
      --deposit string              包含在治理提案中的存款
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者支付交易费用，而不是从签名者扣除
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易设置的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回的估计值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并将其写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        software-upgrade 命令的帮助信息
      --keyring-backend string      选择钥匙环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端钥匙环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --metadata string             包含在治理提案中的元数据
      --no-checksum-required        跳过升级信息中二进制文件的校验和要求
      --no-validate                 跳过升级信息的验证（危险！）
      --node string                 此链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --summary string              包含在治理提案中的摘要
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --title string                放在治理提案上的标题
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
      --upgrade-height int          升级必须发生的高度
      --upgrade-info string         升级计划的信息，例如新版本下载 URL 等
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx upgrade](#zetacored-tx-upgrade)	 - 升级交易子命令

## zetacored tx validate-signatures

验证交易签名

### 概要

打印必须签署交易的地址、已经签署的地址，并确保签名顺序正确。

该命令将检查所有必需的签名者是否已签署交易、签名是否按正确顺序收集，以及签名在给定交易上是否有效。如果同时设置了 `--offline` 标志，则不会执行交易上的签名验证，因为这需要与全节点进行 RPC 通信。

```
zetacored tx validate-signatures [file] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式 (sync|async)
      --chain-id string             网络链 ID
      --dry-run                     忽略 `--gas` 标志并执行交易模拟，但不广播（启用时，本地密钥库不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 自动计算充足 gas。注意："auto" 选项并不总能报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 上限，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅在提供密钥名称时访问本地密钥库）
  -h, --help                        validate-signatures 命令的帮助信息
      --keyring-backend string      选择密钥环的后端 (os|file|kwallet|pass|test|memory)
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式 (text|json)
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式 (direct|amino-json|direct-aux|textual)，此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的时长值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将转移到目标链上费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator 则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 结合使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式 (json|plain)
      --log_level string            日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令

## zetacored tx vesting

归属交易子命令

```
zetacored tx vesting [flags]
```

### 选项

```
  -h, --help   获取 vesting 命令的帮助信息
```

### 从父命令继承的选项

```
      --chain-id string     网络链 ID
      --home string         配置和数据的存储目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx](#zetacored-tx)	 - 交易子命令
* [zetacored tx vesting create-periodic-vesting-account](#zetacored-tx-vesting-create-periodic-vesting-account)	 - 创建一个新的归属账户，并使用代币分配进行资金注入。
* [zetacored tx vesting create-permanent-locked-account](#zetacored-tx-vesting-create-permanent-locked-account)	 - 创建一个新的永久锁定账户，并使用代币分配进行资金注入。
* [zetacored tx vesting create-vesting-account](#zetacored-tx-vesting-create-vesting-account)	 - 创建一个新的归属账户，并使用代币分配进行资金注入。

## zetacored tx vesting create-periodic-vesting-account

创建一个新的归属账户，由代币分配提供资金。

### 概要

一系列代币和以秒为单位的周期长度。周期是顺序的，即一个周期的持续时间仅在前一个周期结束时开始。第一个周期的持续时间在账户创建时开始。例如，以下的 `periods.json` 文件显示了 20 个 "test" 代币，每隔 30 天归属一次。
		其中 `periods.json` 包含：

		一个代币字符串数组和代币归属的 Unix 纪元时间
{ "start_time": 1625204910,
"periods":[
 {
  "coins": "10test",
  "length_seconds":2592000 // 30 天
 },
 {
	"coins": "10test",
	"length_seconds":2592000 // 30 天
 },
]
	}
		

```
zetacored tx vesting create-periodic-vesting-account [to_address] [periods_json_file] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易授予费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认值 200000）
      --gas-adjustment float        用于乘以交易模拟返回的估计值的调整因子；如果手动设置了 gas 限制，则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅在提供密钥名称时访问本地 Keybase）
  -h, --help                        create-periodic-vesting-account 命令的帮助信息
      --keyring-backend string      选择密钥环的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端密钥环目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（先前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加上超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 一起使用时有效，如果目标链未启用 TipDecorator，则忽略此标志
      --unordered                   启用无序交易传递；必须与 --timeout-duration 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx vesting](#zetacored-tx-vesting)	 - 归属交易子命令

## zetacored tx vesting create-permanent-locked-account

创建一个由代币分配资助的新永久锁定账户。

### 概要

创建一个由永久锁定代币分配资助的新账户。这些代币可用于质押但不可转让。质押奖励将作为流动和可转让的代币累积。

```
zetacored tx vesting create-permanent-locked-account [to_address] [amount] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync｜async）
      --chain-id string             网络链 ID
      --dry-run                     忽略 --gas 标志并执行交易模拟，但不广播（启用时无法访问本地密钥库）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 上限；设为 "auto" 自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可替代 "fees" 使用。（默认值 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整系数；若手动设置 gas 上限则忽略此标志（默认值 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并输出到 STDOUT（启用时，仅当提供密钥名称时访问本地密钥库）
  -h, --help                        create-permanent-locked-account 命令的帮助信息
      --keyring-backend string      选择密钥环后端（os｜file｜kwallet｜pass｜test｜memory）
      --keyring-dir string          客户端密钥环目录；若省略，将使用默认的 'home' 目录
      --ledger                      使用已连接的 Ledger 设备
      --node string                 该链的 CometBFT rpc 接口 [host]:[port]
      --note string                 为交易添加描述说明（原 --memo 选项）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text｜json）
  -s, --sequence uint               签名账户的序列号（仅离线模式）
      --sign-mode string            选择签名模式（direct｜amino-json｜direct-aux｜textual），此为高级功能
      --timeout-duration duration   超时持续时间是交易在内存池中被视为有效的时长。交易的无序随机数将设置为交易创建时间加上传递的持续时间值。若交易仍在内存池中，且区块时间已超过提交时间加超时时间戳，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 --timeout-duration。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  小费是将在目标链上转移给费用支付者的金额。此标志仅在与 --aux 同时使用时有效，若目标链未启用 TipDecorator 则忽略
      --unordered                   启用无序交易交付；必须与 --timeout-duration 同时使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据目录
      --log_format string           日志格式（json｜plain）
      --log_level string            日志级别（trace｜debug｜info｜warn｜error｜fatal｜panic｜disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx vesting](#zetacored-tx-vesting)	 - 归属交易子命令

## zetacored tx vesting create-vesting-account

创建一个由代币分配资助的新归属账户。

### 概要

创建一个由代币分配资助的新归属账户。该账户可以是延迟或连续归属账户，这由 `--delayed` 标志决定。所有创建的归属账户的起始时间将设置为提交区块的时间。必须提供 `end_time` 作为 UNIX 纪元时间戳。

```
zetacored tx vesting create-vesting-account [to_address] [amount] [end_time] [flags]
```

### 选项

```
  -a, --account-number uint         签名账户的账户编号（仅限离线模式）
      --aux                         生成辅助签名者数据而非发送交易
  -b, --broadcast-mode string       交易广播模式（sync|async）
      --chain-id string             网络链 ID
      --delayed                     如果为 true，则创建延迟归属账户
      --dry-run                     忽略 `--gas` 标志并执行交易模拟，但不广播（启用时，本地 Keybase 不可访问）
      --fee-granter string          费用授予者为交易支付费用
      --fee-payer string            费用支付者代替签名者支付交易费用
      --fees string                 随交易支付的费用；例如：10uatom
      --from string                 用于签名的私钥名称或地址
      --gas string                  每笔交易的 gas 限制；设置为 "auto" 以自动计算充足 gas。注意："auto" 选项并不总是报告准确结果。设置有效的代币值以调整结果。可代替 "fees" 使用。（默认 200000）
      --gas-adjustment float        乘以交易模拟返回估算值的调整因子；如果手动设置 gas 限制，则忽略此标志（默认 1）
      --gas-prices string           用于确定交易费用的十进制格式 Gas 价格（例如 0.1uatom）
      --generate-only               构建未签名交易并写入 STDOUT（启用时，仅当提供密钥名称时访问本地 Keybase）
  -h, --help                        create-vesting-account 命令的帮助信息
      --keyring-backend string      选择 keyring 的后端（os|file|kwallet|pass|test|memory）
      --keyring-dir string          客户端 Keyring 目录；如果省略，将使用默认的 'home' 目录
      --ledger                      使用连接的 Ledger 设备
      --node string                  该链的 CometBFT rpc 接口的 [host]:[port]
      --note string                 为交易添加描述说明（之前为 --memo）
      --offline                     离线模式（不允许任何在线功能）
  -o, --output string               输出格式（text|json）
  -s, --sequence uint               签名账户的序列号（仅限离线模式）
      --sign-mode string            选择签名模式（direct|amino-json|direct-aux|textual），此为高级功能
      --timeout-duration duration   TimeoutDuration 是交易在内存池中被视为有效的持续时间。交易的无序 nonce 将设置为交易创建时间加上传递的持续时间值。如果交易仍在内存池中，且区块时间已超过提交时间加 TimeoutTimestamp，则交易将被拒绝。
      --timeout-height uint         已弃用：请改用 `--timeout-duration`。设置区块超时高度以防止交易在特定高度后被提交
      --tip string                  Tip 是将转移到目标链上费用支付者的金额。此标志仅在与 `--aux` 一起使用时有效，如果目标链未启用 TipDecorator，则忽略
      --unordered                   启用无序交易传递；必须与 `--timeout-duration` 一起使用
  -y, --yes                         跳过交易广播提示确认
```

### 从父命令继承的选项

```
      --home string                 配置和数据的目录
      --log_format string           日志格式（json|plain）
      --log_level string            日志级别（trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]'）
      --log_no_color                禁用彩色日志
      --trace                       在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored tx vesting](#zetacored-tx-vesting)	 - 归属交易子命令

## zetacored upgrade-handler-version

打印默认的升级处理程序版本

```
zetacored upgrade-handler-version [flags]
```

### 选项

```
  -h, --help   upgrade-handler-version 命令的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据的目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               在错误时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored validate

验证位于默认位置或作为参数传递的位置的创世文件

```
zetacored validate [file] [flags]
```

### 选项

```
  -h, --help   关于 validate 的帮助信息
```

### 从父命令继承的选项

```
      --home string         配置和数据目录
      --log_format string   日志格式 (json|plain)
      --log_level string    日志级别 (trace|debug|info|warn|error|fatal|panic|disabled 或 '*:[level],[key]:[level]')
      --log_no_color        禁用彩色日志
      --trace               出错时打印完整堆栈跟踪
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）

## zetacored 版本

打印应用程序二进制版本信息

```
zetacored version [flags]
```

### 选项

```
  -h, --help            help for version
      --long            Print long version information
  -o, --output string   Output format (text|json) 
```

### 从父命令继承的选项

```
      --home string         directory for config and data 
      --log_format string   The logging format (json|plain) 
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic|disabled or '*:[level],[key]:[level]') 
      --log_no_color        Disable colored logs
      --trace               print out full stack trace on errors
```

### 另请参阅

* [zetacored](#zetacored)	 - Zetacore 守护进程（服务器）