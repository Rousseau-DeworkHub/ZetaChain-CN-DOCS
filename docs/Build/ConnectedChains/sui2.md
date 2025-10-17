```markdown
# Sui

通过 Sui 链与通用应用程序交互并存入代币。

## Sui 网关

要从 Sui 链与通用应用程序交互，请使用 Sui 网关。

关于使用 Sui 网关的分步示例，请参阅 [Sui 教程](/)。

Sui 网关支持：

- 将原生 SUI 和其他代币存入 ZetaChain 上的通用应用程序或账户
- 存入代币并调用通用应用程序

## 存入代币

要将代币存入 ZetaChain 上的 EOA 或通用合约，请使用 `deposit` 函数：

```move
public entry fun deposit<T>(
    gateway: &mut Gateway,
    coins: Coin<T>,
    receiver: String,
    ctx: &mut TxContext,
)
```

`deposit` 函数接受任何已列入白名单的代币类型 `T`（包括原生 SUI），这些代币将被发送到 ZetaChain 上指定的接收者。

`receiver` 参数应是一个有效的 EVM 风格地址（以 `0x` 为前缀的十六进制字符串），代表 ZetaChain 上的外部拥有账户（EOA）或通用应用程序地址。即使接收者是通用应用程序合约，`deposit` 函数也不会触发合约调用。如果您想存入并调用通用应用程序，请改用 `deposit_and_call` 函数。

存款处理完成后，接收者将在 ZetaChain 上收到所存入代币的 ZRC-20 版本。

## 存入代币并调用通用应用程序

要存入代币并调用通用应用程序合约，请使用 `deposit_and_call` 函数：

```move
public entry fun deposit_and_call<T>(
    gateway: &mut Gateway,
    coins: Coin<T>,
    receiver: String,
    payload: vector<u8>,
    ctx: &mut TxContext,
)
```

`receiver` 必须是 ZetaChain 上通用应用程序合约的地址。`payload` 参数将传递给通用应用程序合约的 `onCall` 函数。

有效负载的最大大小为 1024 字节。如果有效负载超过此限制，交易将失败。

## 管理功能

Sui 网关包含几个需要特殊能力对象的管理功能：

- `whitelist<T>` - 启用新代币类型的存款（需要 `WhitelistCap`）
- `withdraw<T>` - 当代币从 ZetaChain 提现回 Sui 时，由 TSS 地址调用。此函数需要一个特殊的能力对象（`WithdrawCap`），该对象仅由 TSS 节点持有。`nonce` 参数通过确保每次提现都被精确处理一次来防止重放攻击。
- `unwhitelist<T>` - 禁用某个代币类型的存款（需要 `AdminCap`）
- `pause` - 暂时禁用所有存款（需要 `AdminCap`）
- `unpause` - 重新启用存款（需要 `AdminCap`）
- `issue_withdraw_and_whitelist_cap` - 轮换 TSS 能力（需要 `AdminCap`）

## 事件

网关会发出几个可以被监听的事件：

- `DepositEvent` - 存入代币时发出
- `DepositAndCallEvent` - 存入代币并进行合约调用时发出
- `WithdrawEvent` - 提现代币时发出
- `NonceIncreaseEvent` - 提现 nonce 增加时发出

## 视图函数

网关提供了几个只读函数：

- `nonce()` - 返回当前的提现 nonce
- `vault_balance<T>()` - 返回网关中特定代币类型的余额
- `is_whitelisted<T>()` - 检查某个代币类型是否已启用存款
- `is_paused()` - 检查存款当前是否暂停
```