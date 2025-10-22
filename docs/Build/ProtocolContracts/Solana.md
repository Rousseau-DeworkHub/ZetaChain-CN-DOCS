# Solana

|标题|描述|
|:-|:-|
|Solana|Solana 协议合约库文档|

*# 箱文档

**版本：** 0.1.0

**格式版本：** 41

# 模块 `gateway`

## 模块

## 模块 `program`

表示程序的模块。

```rust
pub mod program { /* ... */ }
```

### 类型

#### 结构体 `Gateway`

表示程序的结构体。

```rust
pub struct Gateway;
```

##### 实现

###### Trait 实现

- **Freeze**
- **Send**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    原样返回参数。

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Unpin**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **RefUnwindSafe**
- **Sync**
- **UnwindSafe**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **Same**
- **Clone**
  - ```rust
    fn clone(self: &Self) -> Gateway { /* ... */ }
    ```

- **CloneToUninit**
  - ```rust
    unsafe fn clone_to_uninit(self: &Self, dst: *mut u8) { /* ... */ }
    ```

- **IntoEither**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Id**
  - ```rust
    fn id() -> Pubkey { /* ... */ }
    ```

- **ToOwned**
  - ```rust
    fn to_owned(self: &Self) -> T { /* ... */ }
    ```

  - ```rust
    fn clone_into(self: &Self, target: &mut T) { /* ... */ }
    ```

## 模块 `gateway`

```rust
pub mod gateway { /* ... */ }
```

### 函数

#### 函数 `initialize`

初始化网关 PDA。

参数：

* `ctx` - 指令上下文。
* `tss_address` - 以太坊 TSS 地址（20 字节）。
* `chain_id` - 与 PDA 关联的链 ID。

```rust
pub fn initialize(ctx: Context<''_, ''_, ''_, ''_, Initialize<''_>>, tss_address: [u8; 20], chain_id: u64) -> Result<()> { /* ... */ }
```

#### 函数 `increment_nonce`

递增 nonce，在出站失败时由 TSS 使用。

参数：

* `ctx` - 指令上下文。
* `amount` - 原始出站中的金额。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn increment_nonce(ctx: Context<''_, ''_, ''_, ''_, IncrementNonce<''_>>, amount: u64, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `execute`

提取金额到目标程序 PDA，并在目标程序上调用 on_call。

参数：

* `ctx` - 指令上下文。
* `amount` - 要转移的 SOL 金额。
* `sender` - 发送者地址。
* `data` - 传递给目标程序的任意数据。
* `signature` - 消息的签名。
* `recovery_id` - 签名的恢复 ID。
* `message_hash` - 消息的哈希。
* `nonce` - 消息的 nonce。

```rust
pub fn execute(ctx: Context<''_, ''_, ''_, ''_, Execute<''_>>, amount: u64, sender: [u8; 20], data: Vec<u8>, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `execute_revert`

提取金额到目标程序 PDA，并在目标程序上调用 on_revert。

参数：

* `ctx` - 指令上下文。
* `amount` - 要提取的 SOL 金额。
* `sender` - 来自 ZEVM 的发送者。
* `data` - 传递给目标程序的数据。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn execute_revert(ctx: Context<''_, ''_, ''_, ''_, Execute<''_>>, amount: u64, sender: Pubkey, data: Vec<u8>, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `execute_spl_token`

提取 SPL 代币金额到目标程序 PDA，并在目标程序上调用 on_call。

参数：

* `ctx` - 指令上下文。
* `decimals` - 用于精度的代币小数位数。
* `amount` - 要提取的代币金额。
* `sender` - 来自 ZEVM 的发送者。
* `data` - 传递给目标程序的数据。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn execute_spl_token(ctx: Context<''_, ''_, ''_, ''_, ExecuteSPLToken<''_>>, decimals: u8, amount: u64, sender: [u8; 20], data: Vec<u8>, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `execute_spl_token_revert`

提取 SPL 代币金额到目标程序 PDA，并在目标程序上调用 on_revert。

参数：

* `ctx` - 指令上下文。
* `decimals` - 用于精度的代币小数位数。
* `amount` - 要提取的代币金额。
* `sender` - 来自 ZEVM 的发送者。
* `data` - 传递给目标程序的数据。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn execute_spl_token_revert(ctx: Context<''_, ''_, ''_, ''_, ExecuteSPLToken<''_>>, decimals: u8, amount: u64, sender: Pubkey, data: Vec<u8>, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `set_deposit_paused`

暂停或取消暂停存款。调用者是 PDA 中存储的权限。

参数：

* `ctx` - 指令上下文。
* `deposit_paused` - 用于暂停或取消暂停存款的布尔标志。

```rust
pub fn set_deposit_paused(ctx: Context<''_, ''_, ''_, ''_, UpdatePaused<''_>>, deposit_paused: bool) -> Result<()> { /* ... */ }
```

#### 函数 `update_tss`

更新 TSS 地址。调用者是 PDA 中存储的权限。

参数：

* `ctx` - 指令上下文。
* `tss_address` - 新的以太坊 TSS 地址（20 字节）。

```rust
pub fn update_tss(ctx: Context<''_, ''_, ''_, ''_, UpdateTss<''_>>, tss_address: [u8; 20]) -> Result<()> { /* ... */ }
```

#### 函数 `update_authority`

更新 PDA 权限。调用者是 PDA 中存储的权限。

参数：

* `ctx` - 指令上下文。
* `new_authority_address` - 新权限的公钥。

```rust
pub fn update_authority(ctx: Context<''_, ''_, ''_, ''_, UpdateAuthority<''_>>, new_authority_address: Pubkey) -> Result<()> { /* ... */ }
```

#### 函数 `reset_nonce`

重置 PDA nonce。调用者是 PDA 中存储的权限。

参数：

* `ctx` - 指令上下文。
* `new_nonce` - 新的 nonce。

```rust
pub fn reset_nonce(ctx: Context<''_, ''_, ''_, ''_, ResetNonce<''_>>, new_nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `whitelist_spl_mint`

将新的 SPL 代币加入白名单。调用者是 TSS。

参数：

* `ctx` - 指令上下文。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn whitelist_spl_mint(ctx: Context<''_, ''_, ''_, ''_, Whitelist<''_>>, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `unwhitelist_spl_mint`

将 SPL 代币从白名单中移除。调用者是 TSS。

参数：

* `ctx` - 指令上下文。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn unwhitelist_spl_mint(ctx: Context<''_, ''_, ''_, ''_, Unwhitelist<''_>>, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `deposit`

将 SOL 存入程序，并在 ZetaChain zEVM 上贷记 `receiver`。

参数：

* `ctx` - 指令上下文。
* `amount` - 要存入的 lamports 金额。
* `receiver` - ZetaChain zEVM 上接收者的以太坊地址。
* `revert_options` - 由调用者创建的回退选项。

```rust
pub fn deposit(ctx: Context<''_, ''_, ''_, ''_, Deposit<''_>>, amount: u64, receiver: [u8; 20], revert_options: Option<RevertOptions>) -> Result<()> { /* ... */ }
```

#### 函数 `deposit_and_call`

存入 SOL 并调用 ZetaChain zEVM 上的合约。

参数：

* `ctx` - 指令上下文。
* `amount` - 要存入的 lamports 金额。
* `receiver` - ZetaChain zEVM 上接收者的以太坊地址。
* `message` - 传递给合约的消息。
* `revert_options` - 由调用者创建的回退选项。

```rust
pub fn deposit_and_call(ctx: Context<''_, ''_, ''_, ''_, Deposit<''_>>, amount: u64, receiver: [u8; 20], message: Vec<u8>, revert_options: Option<RevertOptions>) -> Result<()> { /* ... */ }
```

#### 函数 `deposit_spl_token`

存入 SPL 代币并在 ZetaChain zEVM 上贷记 `receiver`。

参数：

* `ctx` - 指令上下文。
* `amount` - 要存入的 SPL 代币金额。
* `receiver` - ZetaChain zEVM 上接收者的以太坊地址。
* `revert_options` - 由调用者创建的回退选项。

```rust
pub fn deposit_spl_token(ctx: Context<''_, ''_, ''_, ''_, DepositSplToken<''_>>, amount: u64, receiver: [u8; 20], revert_options: Option<RevertOptions>) -> Result<()> { /* ... */ }
```

#### 函数 `deposit_spl_token_and_call`

存入 SPL 代币并调用 ZetaChain zEVM 上的合约。

参数：

* `ctx` - 指令上下文。
* `amount` - 要存入的 SPL 代币金额。
* `receiver` - ZetaChain zEVM 上接收者的以太坊地址。
* `message` - 传递给合约的消息。
* `revert_options` - 由调用者创建的回退选项。

```rust
pub fn deposit_spl_token_and_call(ctx: Context<''_, ''_, ''_, ''_, DepositSplToken<''_>>, amount: u64, receiver: [u8; 20], message: Vec<u8>, revert_options: Option<RevertOptions>) -> Result<()> { /* ... */ }
```

#### 函数 `call`

调用 ZetaChain zEVM 上的合约。

参数：

* `receiver` - ZetaChain zEVM 上接收者的以太坊地址。
* `message` - 传递给合约的消息。
* `revert_options` - 由调用者创建的回退选项。

```rust
pub fn call(ctx: Context<''_, ''_, ''_, ''_, Call<''_>>, receiver: [u8; 20], message: Vec<u8>, revert_options: Option<RevertOptions>) -> Result<()> { /* ... */ }
```

#### 函数 `withdraw`

提取 SOL。调用者是 TSS。

参数：

* `ctx` - 指令上下文。
* `amount` - 要提取的 SOL 金额。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn withdraw(ctx: Context<''_, ''_, ''_, ''_, Withdraw<''_>>, amount: u64, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

#### 函数 `withdraw_spl_token`

提取 SPL 代币。调用者是 TSS。

参数：

* `ctx` - 指令上下文。
* `decimals` - 用于精度的代币小数位数。
* `amount` - 要提取的代币金额。
* `signature` - TSS 签名。
* `recovery_id` - 用于签名验证的恢复 ID。
* `message_hash` - 用于签名验证的消息哈希。
* `nonce` - 当前 nonce 值。

```rust
pub fn withdraw_spl_token(ctx: Context<''_, ''_, ''_, ''_, WithdrawSPLToken<''_>>, decimals: u8, amount: u64, signature: [u8; 64], recovery_id: u8, message_hash: [u8; 32], nonce: u64) -> Result<()> { /* ... */ }
```

## 模块 `instruction`

一个由 Anchor 生成的模块，包含程序的指令集，其中 `#[program]` 模块中的每个方法处理程序都与一个定义方法输入参数的结构体相关联。当需要序列化 Anchor 指令数据时，例如在客户端上指定指令时，应直接使用这些结构体。

```rust
pub mod instruction { /* ... */ }
```

### 类型

#### 结构体 `Initialize`

指令。

```rust
pub struct Initialize {
    pub tss_address: [u8; 20],
    pub chain_id: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `tss_address` | `[u8; 20]` |  |
| `chain_id` | `u64` |  |

##### 实现

###### 特性实现

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **InstructionData**
- **Freeze**
- **UnwindSafe**
- **RefUnwindSafe**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **Sync**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **IntoEither**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Discriminator**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Same**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Unpin**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Send**

#### 结构体 `IncrementNonce`

指令。

```rust
pub struct IncrementNonce {
    pub amount: u64,
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Same**
- **Send**
- **Unpin**
- **RefUnwindSafe**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Freeze**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **IntoEither**
- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **Discriminator**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **UnwindSafe**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Sync**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **InstructionData**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

#### 结构体 `Execute`

指令。

```rust
pub struct Execute {
    pub amount: u64,
    pub sender: [u8; 20],
    pub data: Vec<u8>,
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `sender` | `[u8; 20]` |  |
| `data` | `Vec<u8>` |  |
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **IntoEither**
- **Same**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Discriminator**
- **RefUnwindSafe**
- **Freeze**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Unpin**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **UnwindSafe**
- **Sync**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Send**
- **InstructionData**

#### 结构体 `ExecuteRevert`

指令。

```rust
pub struct ExecuteRevert {
    pub amount: u64,
    pub sender: Pubkey,
    pub data: Vec<u8>,
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `sender` | `Pubkey` |  |
| `data` | `Vec<u8>` |  |
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **Same**
- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Sync**
- **InstructionData**
- **UnwindSafe**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Freeze**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Discriminator**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Unpin**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **RefUnwindSafe**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **IntoEither**
- **Send**

#### 结构体 `ExecuteSplToken`

指令。

```rust
pub struct ExecuteSplToken {
    pub decimals: u8,
    pub amount: u64,
    pub sender: [u8; 20],
    pub data: Vec<u8>,
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `decimals` | `u8` |  |
| `amount` | `u64` |  |
| `sender` | `[u8; 20]` |  |
| `data` | `Vec<u8>` |  |
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **Same**
- **Send**
- **Sync**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **IntoEither**
- **Unpin**
- **Freeze**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **InstructionData**
- **RefUnwindSafe**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **UnwindSafe**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Discriminator**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

#### 结构体 `ExecuteSplTokenRevert`

指令。

```rust
pub struct ExecuteSplTokenRevert {
    pub decimals: u8,
    pub amount: u64,
    pub sender: Pubkey,
    pub data: Vec<u8>,
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `decimals` | `u8` |  |
| `amount` | `u64` |  |
| `sender` | `Pubkey` |  |
| `data` | `Vec<u8>` |  |
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **UnwindSafe**
- **RefUnwindSafe**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Unpin**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Same**
- **Discriminator**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **InstructionData**
- **Freeze**
- **IntoEither**
- **Send**
- **Sync**

#### 结构体 `SetDepositPaused`

指令。

```rust
pub struct SetDepositPaused {
    pub deposit_paused: bool,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `deposit_paused` | `bool` |  |

##### 实现

###### 特性实现

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Send**
- **Freeze**
- **Unpin**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **UnwindSafe**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Discriminator**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Same**
- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Sync**
- **IntoEither**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **InstructionData**
- **RefUnwindSafe**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

#### 结构体 `UpdateTss`

指令。

```rust
pub struct UpdateTss {
    pub tss_address: [u8; 20],
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `tss_address` | `[u8; 20]` |  |

##### 实现

###### 特性实现

- **Same**
- **InstructionData**
- **Unpin**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **Discriminator**
- **Freeze**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Send**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Sync**
- **IntoEither**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **UnwindSafe**
- **RefUnwindSafe**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

#### 结构体 `UpdateAuthority`

指令。

```rust
pub struct UpdateAuthority {
    pub new_authority_address: Pubkey,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `new_authority_address` | `Pubkey` |  |

##### 实现

###### 特性实现

- **Send**
- **UnwindSafe**
- **RefUnwindSafe**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Sync**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **Same**
- **Freeze**
- **Unpin**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **IntoEither**
- **Discriminator**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **InstructionData**
- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

#### 结构体 `ResetNonce`

指令。

```rust
pub struct ResetNonce {
    pub new_nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `new_nonce` | `u64` |  |

##### 实现

###### 特性实现

- **Same**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **IntoEither**
- **Freeze**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **UnwindSafe**
- **RefUnwindSafe**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **InstructionData**
- **Sync**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Unpin**
- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **Send**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Discriminator**

#### 结构体 `WhitelistSplMint`

指令。

```rust
pub struct WhitelistSplMint {
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **UnwindSafe**
- **Discriminator**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Same**
- **RefUnwindSafe**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **Send**
- **InstructionData**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Freeze**
- **Unpin**
- **IntoEither**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Sync**

#### 结构体 `UnwhitelistSplMint`

指令。

```rust
pub struct UnwhitelistSplMint {
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Send**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **Unpin**
- **Same**
- **Discriminator**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **IntoEither**
- **Freeze**
- **Sync**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **InstructionData**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **RefUnwindSafe**
- **UnwindSafe**

#### 结构体 `Deposit`

指令。

```rust
pub struct Deposit {
    pub amount: u64,
    pub receiver: [u8; 20],
    pub revert_options: Option<RevertOptions>,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `receiver` | `[u8; 20]` |  |
| `revert_options` | `Option<RevertOptions>` |  |

##### 实现

###### 特性实现

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **RefUnwindSafe**
- **Unpin**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Discriminator**
- **InstructionData**
- **Freeze**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **UnwindSafe**
- **Sync**
- **Send**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **IntoEither**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Same**

#### 结构体 `DepositAndCall`

指令。

```rust
pub struct DepositAndCall {
    pub amount: u64,
    pub receiver: [u8; 20],
    pub message: Vec<u8>,
    pub revert_options: Option<RevertOptions>,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `receiver` | `[u8; 20]` |  |
| `message` | `Vec<u8>` |  |
| `revert_options` | `Option<RevertOptions>` |  |

##### 实现

###### 特性实现

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Sync**
- **UnwindSafe**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **Discriminator**
- **Freeze**
- **Same**
- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **IntoEither**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **InstructionData**
- **RefUnwindSafe**
- **Send**
- **Unpin**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

#### 结构体 `DepositSplToken`

指令。

```rust
pub struct DepositSplToken {
    pub amount: u64,
    pub receiver: [u8; 20],
    pub revert_options: Option<RevertOptions>,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `receiver` | `[u8; 20]` |  |
| `revert_options` | `Option<RevertOptions>` |  |

##### 实现

###### 特性实现

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Sync**
- **Discriminator**
- **Freeze**
- **IntoEither**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **RefUnwindSafe**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Same**
- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Send**
- **InstructionData**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **UnwindSafe**
- **Unpin**

#### 结构体 `DepositSplTokenAndCall`

指令。

```rust
pub struct DepositSplTokenAndCall {
    pub amount: u64,
    pub receiver: [u8; 20],
    pub message: Vec<u8>,
    pub revert_options: Option<RevertOptions>,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `receiver` | `[u8; 20]` |  |
| `message` | `Vec<u8>` |  |
| `revert_options` | `Option<RevertOptions>` |  |

##### 实现

###### 特性实现

- **Freeze**
- **Discriminator**
- **Sync**
- **Unpin**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **RefUnwindSafe**
- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **UnwindSafe**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **InstructionData**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **Send**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **IntoEither**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Same**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

#### 结构体 `Call`

指令。

```rust
pub struct Call {
    pub receiver: [u8; 20],
    pub message: Vec<u8>,
    pub revert_options: Option<RevertOptions>,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `receiver` | `[u8; 20]` |  |
| `message` | `Vec<u8>` |  |
| `revert_options` | `Option<RevertOptions>` |  |

##### 实现

###### 特性实现

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Freeze**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **Send**
- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **Sync**
- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **IntoEither**
- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Discriminator**
- **InstructionData**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Same**
- **Unpin**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **RefUnwindSafe**
- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **UnwindSafe**

#### 结构体 `Withdraw`

指令。

```rust
pub struct Withdraw {
    pub amount: u64,
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `amount` | `u64` |  |
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **Same**
- **Unpin**
- **Send**
- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **UnwindSafe**
- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **IntoEither**
- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **InstructionData**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **Freeze**
- **Sync**
- **RefUnwindSafe**
- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Discriminator**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

#### 结构体 `WithdrawSplToken`

指令。

```rust
pub struct WithdrawSplToken {
    pub decimals: u8,
    pub amount: u64,
    pub signature: [u8; 64],
    pub recovery_id: u8,
    pub message_hash: [u8; 32],
    pub nonce: u64,
}
```

##### 字段

| 名称 | 类型 | 文档 |
|------|------|---------------|
| `decimals` | `u8` |  |
| `amount` | `u64` |  |
| `signature` | `[u8; 64]` |  |
| `recovery_id` | `u8` |  |
| `message_hash` | `[u8; 32]` |  |
| `nonce` | `u64` |  |

##### 实现

###### 特性实现

- **Any**
  - ```rust
    fn type_id(self: &Self) -> TypeId { /* ... */ }
    ```

- **IntoEither**
- **BorshSerialize**
  - ```rust
    fn serialize<W: borsh::maybestd::io::Write>(self: &Self, writer: &mut W) -> ::core::result::Result<(), borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Unpin**
- **From**
  - ```rust
    fn from(t: T) -> T { /* ... */ }
    ```
    返回参数不变。

- **Borrow**
  - ```rust
    fn borrow(self: &Self) -> &T { /* ... */ }
    ```

- **Discriminator**
- **InstructionData**
- **Owner**
  - ```rust
    fn owner() -> Pubkey { /* ... */ }
    ```

- **VZip**
  - ```rust
    fn vzip(self: Self) -> V { /* ... */ }
    ```

- **Send**
- **RefUnwindSafe**
- **Same**
- **Freeze**
- **BorshDeserialize**
  - ```rust
    fn deserialize_reader<R: borsh::maybestd::io::Read>(reader: &mut R) -> ::core::result::Result<Self, borsh::maybestd::io::Error> { /* ... */ }
    ```

- **Into**
  - ```rust
    fn into(self: Self) -> U { /* ... */ }
    ```
    调用 `U::from(self)`。

- **Sync**
- **BorrowMut**
  - ```rust
    fn borrow_mut(self: &mut Self) -> &mut T { /* ... */ }
    ```

- **TryInto**
  - ```rust
    fn try_into(self: Self) -> Result<U, <U as TryFrom<T>>::Error> { /* ... */ }
    ```

- **UnwindSafe**
- **TryFrom**
  - ```rust
    fn try_from(value: U) -> Result<T, <T as TryFrom<U>>::Error> { /* ... */ }
    ```

## 模块 `accounts`

一个由 Anchor 生成的模块，提供了一组结构体，这些结构体镜像了派生 `Accounts` 的结构体，其中每个字段都是一个 `Pubkey`。这对于为客户端指定账户非常有用。

```rust
pub mod accounts { /* ... */ }
```

### 重新导出

#### 重新导出 `crate::__client_accounts_deposit_spl_token::*`

```rust
pub use crate::__client_accounts_deposit_spl_token::*;
```

#### 重新导出 `crate::__client_accounts_call::*`

```rust
pub use crate::__client_accounts_call::*;
```

#### 重新导出 `crate::__client_accounts_initialize::*`

```rust
pub use crate::__client_accounts_initialize::*;
```

#### 重新导出 `crate::__client_accounts_whitelist::*`

```rust
pub use crate::__client_accounts_whitelist::*;
```

#### 重新导出 `crate::__client_accounts_update_authority::*`

```rust
pub use crate::__client_accounts_update_authority::*;
```

#### 重新导出 `crate::__client_accounts_unwhitelist::*`

```rust
pub use crate::__client_accounts_unwhitelist::*;
```

#### 重新导出 `crate::__client_accounts_execute::*`

```rust
pub use crate::__client_accounts_execute::*;
```

#### 重新导出 `crate::__client_accounts_withdraw_spl_token::*`

```rust
pub use crate::__client_accounts_withdraw_spl_token::*;
```

#### 重新导出 `crate::__client_accounts_withdraw::*`

```rust
pub use crate::__client_accounts_withdraw::*;
```

#### 重新导出 `crate::__client_accounts_update_tss::*`

```rust
pub use crate::__client_accounts_update_tss::*;
```

#### 重新导出 `crate::__client_accounts_deposit::*`

```rust
pub use crate::__client_accounts_deposit::*;
```

#### 重新导出 `crate::__client_accounts_update_paused::*`

```rust
pub use crate::__client_accounts_update_paused::*;
```

#### 重新导出 `crate::__client_accounts_execute_spl_token::*`

```rust
pub use crate::__client_accounts_execute_spl_token::*;
```

#### 重新导出 `crate::__client_accounts_increment_nonce::*`

```rust
pub use crate::__client_accounts_increment_nonce::*;
```

#### 重新导出 `crate::__client_accounts_reset_nonce::*`

```rust
pub use crate::__client_accounts_reset_nonce::*;
```

## 函数

### 函数 `check_id`

确认给定的公钥是否等同于程序 ID。

```rust
pub fn check_id(id: &anchor_lang::solana_program::pubkey::Pubkey) -> bool { /* ... */ }
```

### 函数 `id`

返回程序 ID。

```rust
pub fn id() -> anchor_lang::solana_program::pubkey::Pubkey { /* ... */ }
```

### 函数 `id_const`

`ID` 的常量版本。

```rust
pub const fn id_const() -> anchor_lang::solana_program::pubkey::Pubkey { /* ... */ }
```

### 函数 `entrypoint`

**属性：**

- `#[no_mangle]`

# 安全性

```rust
pub unsafe extern "C" fn entrypoint(input: *mut u8) -> u64 { /* ... */ }
```

### 函数 `entry`

Anchor 代码生成器暴露了一种编程模型，用户可以在 `#[program]` 模块内定义一组方法，方式类似于编写 RPC 请求处理程序。然后，宏生成大量代码，将这些用户定义的方法包装成可以在 Solana 上执行的内容。

目前，这些方法属于一个类别：

- 全局方法 - `#[program]` 内的常规方法。

代码生成必须小心，以防止这些不同命名空间中的方法发生冲突。因此，Anchor 使用一种 sighash 的变体来执行方法分派，而不是像简单的枚举变体鉴别器之类的东西。

生成代码的执行流程可以大致概述如下：

* 通过入口点启动程序。
* 检查声明的程序 ID 是否与输入的程序 ID 匹配。如果不匹配，则返回错误。
* 根据指令数据是否以方法的鉴别器开头，查找并调用方法。
* 运行方法处理程序包装器。这包装了用户实际编写的代码，包括反序列化账户、构建上下文、调用用户的代码，最后运行退出例程，该例程通常持久化账户更改。

这里的 `entry` 函数定义了 Solana 程序的标准入口，执行从此开始。

```rust
pub fn entry<''info>(program_id: &Pubkey, accounts: &''info [AccountInfo<''info>], data: &[u8]) -> anchor_lang::solana_program::entrypoint::ProgramResult { /* ... */ }
```

## 常量与静态变量

### 静态 `ID`

静态程序 ID

```rust
pub static ID: anchor_lang::solana_program::pubkey::Pubkey = _;
```

### 常量 `ID_CONST`

常量版本的 `ID`

```rust
pub const ID_CONST: anchor_lang::solana_program::pubkey::Pubkey = _;
```

## 重新导出

### 重新导出 `DEPOSIT_FEE`

```rust
pub use utils::DEPOSIT_FEE;
```

### 重新导出 `contexts::*`

```rust
pub use contexts::*;
```

### 重新导出 `errors::*`

```rust
pub use errors::*;
```

### 重新导出 `state::*`

```rust
pub use state::*;
```