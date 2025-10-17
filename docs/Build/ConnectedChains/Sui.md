\## Sui



从 Sui 调用通用应用并存入代币



\### Sui 网关



要从 Sui 链与通用应用交互，需使用 Sui 网关。


关于使用 Sui 网关的分步示例，请参见 [Sui 教程](https://www.zetachain.com/docs/developers/tutorials/sui/)。



Sui 网关支持：



\- 向 ZetaChain 上的通用应用或账户存入原生 SUI 及其他代币

\- 存入代币并调用通用应用



\#### 存入代币



要向 ZetaChain 上的外部拥有账户（EOA）或通用合约存入代币，可使用 `deposit` 函数：



```rust

public entry fun deposit<T>(

&nbsp;   gateway: \&mut Gateway,

&nbsp;   coins: Coin<T>,

&nbsp;   receiver: String,

&nbsp;   ctx: \&mut TxContext,

)

```



`deposit` 函数接受任何已列入白名单的代币类型 `T`（包括原生 SUI），这些代币将被发送到 ZetaChain 上指定的接收方。



`receiver` 参数应为有效的 EVM 格式地址（以 `0x` 为前缀的十六进制字符串），代表 ZetaChain 上的外部拥有账户（EOA）或通用应用地址。即使接收方是通用应用合约，`deposit` 函数也不会触发合约调用。如果需要存入代币并调用通用应用，请改用 `deposit\_and\_call` 函数。



存款处理完成后，接收方将在 ZetaChain 上收到存入代币对应的 ZRC-20 版本。



\#### 存入代币并调用通用应用



要存入代币并调用通用应用合约，可使用 `deposit\_and\_call` 函数：



```rust

public entry fun deposit\_and\_call<T>(

&nbsp;   gateway: \&mut Gateway,

&nbsp;   coins: Coin<T>,

&nbsp;   receiver: String,

&nbsp;   payload: vector<u8>,

&nbsp;   ctx: \&mut TxContext,

)

```



`receiver` 必须是 ZetaChain 上通用应用合约的地址。`payload` 参数将被传递到通用应用合约的 `onCall` 函数。



&nbsp;payload 的最大大小为 1024 字节。如果 payload 超过此限制，交易将失败。



\#### 管理函数



Sui 网关包含多个需要特殊权限对象的管理函数：



\- `whitelist<T>` - 启用新代币类型的存款功能（需要 `WhitelistCap` 权限）

\- `withdraw<T>` - 当代币从 ZetaChain 提取到 Sui 时，由 TSS 地址调用。此函数需要特殊的权限对象（`WithdrawCap`），该对象仅由 TSS 节点持有。`nonce` 参数通过确保每次提取仅被处理一次来防止重放攻击。

\- `unwhitelist<T>` - 禁用代币类型的存款功能（需要 `AdminCap` 权限）

\- `pause` - 暂时禁用所有存款（需要 `AdminCap` 权限）

\- `unpause` - 重新启用存款（需要 `AdminCap` 权限）

\- `issue\_withdraw\_and\_whitelist\_cap` - 轮换 TSS 权限（需要 `AdminCap` 权限）



\#### 事件



网关会 emit 多个可监控的事件：



\- `DepositEvent` - 存入代币时 emit

\- `DepositAndCallEvent` - 存入代币并进行合约调用时 emit

\- `WithdrawEvent` - 提取代币时 emit

\- `NonceIncreaseEvent` - 提取 nonce 增加时 emit



\#### 视图函数



网关提供多个只读函数：



\- `nonce()` - 返回当前提取 nonce

\- `vault\_balance<T>()` - 返回网关中特定代币类型的余额

\- `is\_whitelisted<T>()` - 检查代币类型是否已启用存款功能

\- `is\_paused()` - 检查存款当前是否已暂停

