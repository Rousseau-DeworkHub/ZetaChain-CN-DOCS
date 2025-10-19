# TON Gateway 文档

## gateway.fc

**常量**

- **op::internal::donate** = 100
- **op::internal::deposit** = 101
- **op::internal::deposit_and_call** = 102
- **op::internal::call** = 103
- **op::external::withdraw** = 200
- **op::external::increase_seqno** = 205
- **op::authority::set_deposits_enabled** = 201
- **op::authority::update_tss** = 202
- **op::authority::update_code** = 203
- **op::authority::update_authority** = 204
- **op::authority::reset_seqno** = 206

**`handle_deposit`**

```
() handle_deposit(int amount, slice in_msg_body) impure inline {
```


将 TON 存入 gateway 并指定 ZetaChain 上的 EVM 接收者。

**`handle_call`**

```
() handle_call(int amount, slice in_msg_body) impure inline {
```


通过确保 call_data 大小和 gas 成本被覆盖来处理 zeta 的 onCall 方法；

注意：如果发送的金额大于交易费用，此操作不会退还多余金额！我们可以在未来的改进中考虑将多余金额退回。目前请发送等于 calculate_gas_fee(op::call) 的金额。

**`handle_set_deposits_enabled`**

```
() handle_set_deposits_enabled(slice sender, slice message) impure inline {
```


启用或禁用存款。

**`handle_update_tss`**

```
() handle_update_tss(slice sender, slice message) impure inline {
```

更新 TSS 地址。**请格外小心地执行**，错误的 TSS 地址会导致资金损失。

**`handle_update_code`**

```
() handle_update_code(slice sender, slice message) impure inline {
```


更新合约的代码 `Handle_code_update (cell new_code)`

**`handle_reset_seqno`**

```
() handle_reset_seqno(slice sender, slice message) impure inline {
```


将序列号重置为指定值 `Handles reset_seqno (uint32 new_seqno)`

**`recv_internal`**

```
() recv_internal(int my_balance, int msg_value, cell in_msg_full, slice in_msg_body) impure {
```


所有内部消息的输入。

**`handle_withdrawal`**

```shell
() handle_withdrawal(slice payload) impure inline {
```


向接收者提取资产 `Handle_withdrawal (MsgAddr recipient, Coins amount, uint32 seqno)`

**`handle_increase_seqno`**

`() handle_increase_seqno(slice payload) impure inline {`


将序列号增加 1，不执行任何其他操作。`Handle_increase_seqno (uint32 failure_reason, uint32 seqno)`

**`recv_external`**

```
() recv_external(slice message) impure {
```


所有外部消息的入口点。