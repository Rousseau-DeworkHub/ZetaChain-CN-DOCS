| 标题 | 描述                                              |
| :--- | :------------------------------------------------ |
| TON  | 从 TON 调用通用应用并进行存入 |

若要从 TON 与通用应用交互，请使用 TON 网关（TON Gateway）。

TON 网关支持以下操作：

- 将 TON 存入 ZetaChain 上的通用应用或账户  
- 存入 TON 并调用通用应用  
- 从 ZetaChain 提取 TON 

## 存入 TON

要将 TON 存入外部账户（EOA）或通用合约，请向网关合约（Gateway Contract）发送一条内部消息，结构如下：

```func
op_code:uint32 query_id:uint64 evm_recipient:slice (160 bits)
```

存入操作的 `op_code` 为 `101`。`query_id` 保留供未来使用，请将其设为 `0`。

`evm_recipient` 指定 ZetaChain 上接收存入 TON 的地址，可以是外部账户（EOA）或通用应用地址。

以下是使用 TypeScript 构建存入消息的示例：

```typescript
const opDeposit = 101;
const body = beginCell().storeUint(opDeposit, 32).storeUint(0, 64).storeUint(zevmRecipient, 160).endCell();
```

存入处理完成后，接收方会收到存入 TON 的 [ZRC-20 版本](/developers/evm/zrc20)。

## 存入 TON 并调用通用应用

若要存入 TON 并调用通用应用合约，请向网关合约发送一条内部消息，结构如下：

```func
op_code:uint32 query_id:uint64 evm_recipient:slice (160 bits) call_data:cell
```

存入并调用操作的 `op_code` 为 `102`。`query_id` 保留供未来使用，请设为 `0`。同时请注意，`call_data` 应采用 ["snake data"](https://docs.ton.org/v3/guidelines/dapps/asset-processing/nft-processing/metadata-parsing#snake-data-encoding) 格式编码（大多数 TON 库均支持该格式）。

`evm_recipient` 必须是通用应用合约的地址。

`call_data` 单元包含将传递给通用应用合约中 `onCall` 函数的载荷（payload）。

以下是使用 TypeScript 构建存入并调用消息的示例：

```typescript
const opDepositAndCall = 102;
const body = beginCell()
  .storeUint(opDepositAndCall, 32)
  .storeUint(0, 64)
  .storeUint(zevmRecipient, 160)
  .storeRef(callDataCell) // callDataCell 应为包含 payload 的单元
  .endCell();
```

跨链交易处理完成后，通用应用合约中的 `onCall` 函数会被执行。
