# ZetaChain — gRPC Gateway 文档

ZetaChain 的 API 文档。

### /cosmos/auth/v1beta1/account_info/{address}

#### GET
##### 摘要

AccountInfo 查询所有账户类型共有的账户信息。

##### 描述

自： cosmos-sdk 0.47

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是账户地址字符串。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"info"**: { **"address"**: string, **"pub_key"**: { **"type_url"**: string, **"value"**: byte }, **"account_number"**: string (uint64), **"sequence"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/accounts

#### GET
##### 摘要

账户返回所有现有账户。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。  
Since: cosmos-sdk 0.43

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包含可用于分页的总项目数计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。Since: cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"accounts"**: [ { **"type_url"**: string, **"value"**: byte } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/accounts/{address}

#### GET
##### 总结

账户基于地址返回账户详情。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 定义了要查询的地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"account"**: { **"type_url"**: string, **"value"**: byte } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/address_by_id/{id}

#### GET
##### 摘要

AccountAddressByID 根据账户编号返回账户地址。

##### 描述

自：cosmos-sdk 0.46.2

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| id | path | 已弃用，请使用 account_id 代替。id 是要查询地址的账户编号。此字段本应为 uint64（如所有账户编号），并将在 auth 查询的未来版本中更新为 uint64。 | 是 | string (int64) |
| account_id | query | account_id 是要查询地址的账户编号。自：cosmos-sdk 0.47 | 否 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"account_address"**: string } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/bech32

#### GET
##### 摘要

Bech32Prefix 查询 bech32Prefix

##### 描述

自: cosmos-sdk 0.46

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"bech32_prefix"**: string } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/bech32/{address_bytes}

#### GET
##### 摘要

AddressBytesToString 将账户地址字节转换为字符串

##### 描述

自：cosmos-sdk 0.46

##### 参数

| 名称 | 位置 | 描述 | 必填 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address_bytes | path |  | 是 | byte |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"address_string"**: string } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/bech32/{address_string}

#### GET
##### 摘要

AddressStringToBytes 将地址字符串转换为字节

##### 描述

自 cosmos-sdk 0.46 起

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address_string | path |  | Yes | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"address_bytes"**: byte } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/module_accounts

#### GET
##### 摘要

ModuleAccounts 返回所有现有的模块账户。

##### 描述

自 cosmos-sdk 0.46

##### 响应

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"accounts"**: [ { **"type_url"**: string, **"value"**: byte } ] } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/module_accounts/{name}

#### GET
##### 摘要

ModuleAccountByName 通过模块名称返回模块账户信息

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| name | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"account"**: { **"type_url"**: string, **"value"**: byte } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/auth/v1beta1/params

#### GET
##### 总结

Params 查询所有参数。

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"params"**: { **"max_memo_characters"**: string (uint64), **"tx_sig_limit"**: string (uint64), **"tx_size_cost_per_byte"**: string (uint64), **"sig_verify_cost_ed25519"**: string (uint64), **"sig_verify_cost_secp256k1"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/balances/{address}

#### GET
##### 总结

AllBalances 查询单个账户的所有代币余额。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是要查询余额的地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包含可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果应按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |
| resolve_denom | query | resolve_denom 是将 denom 从元数据解析为人类可读形式的标志。自：cosmos-sdk 0.50 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"balances"**: [ { **"denom"**: string, **"amount"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/balances/{address}/by_denom

#### GET
##### 摘要

查询单个账户的单个代币余额。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是要查询余额的地址。 | 是 | string |
| denom | query | denom 是要查询余额的代币单位。 | 否 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"balance"**: { **"denom"**: string, **"amount"**: string } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/denom_owners/{denom}

#### GET
##### 摘要

DenomOwners 查询拥有特定代币面额的所有账户地址。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。  
自 cosmos-sdk 0.46 起

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| denom | path | denom 定义了要查询所有账户持有者的代币面额。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵循。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果应按降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | { **"denom_owners"**: [ { **"address"**: string, **"balance"**: { **"denom"**: string, **"amount"**: string } } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/denom_owners_by_query

#### GET
##### 摘要

DenomOwnersByQuery 查询拥有特定代币面额的所有账户地址。

##### 描述

自：cosmos-sdk 0.50.3

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| denom | query | denom 定义了要查询所有账户持有者的代币面额。 | 否 | string |
| pagination.key | query | key 是在 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是要在结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数，在用户界面中。count_total 仅在 offset 使用时被尊重。当 key 被设置时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"denom_owners"**: [ { **"address"**: string, **"balance"**: { **"denom"**: string, **"amount"**: string } } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/denoms_metadata

#### GET
##### 摘要

DenomsMetadata 查询所有已注册代币面额的客户端元数据。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是在 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，可在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是要在结果页面中返回的结果总数。如果留空，将默认为由每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包含可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 时，结果将以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"metadatas"**: [ { **"description"**: string, **"denom_units"**: [ { **"denom"**: string, **"exponent"**: long, **"aliases"**: [ string ] } ], **"base"**: string, **"display"**: string, **"name"**: string, **"symbol"**: string, **"uri"**: string, **"uri_hash"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/denoms_metadata/{denom}

#### GET
##### 摘要

DenomMetadata 查询给定代币面额的客户端元数据。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| denom | path | denom 是要查询元数据的代币面额。 | 是 | string |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"metadata"**: { **"description"**: string, **"denom_units"**: [ { **"denom"**: string, **"exponent"**: long, **"aliases"**: [ string ] } ], **"base"**: string, **"display"**: string, **"name"**: string, **"symbol"**: string, **"uri"**: string, **"uri_hash"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/denoms_metadata_by_query_string

#### GET
##### 摘要

DenomMetadataByQueryString 查询给定代币单位的客户端元数据。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| denom | query | denom 是要查询元数据的代币单位。 | 否 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"metadata"**: { **"description"**: string, **"denom_units"**: [ { **"denom"**: string, **"exponent"**: long, **"aliases"**: [ string ] } ], **"base"**: string, **"display"**: string, **"name"**: string, **"symbol"**: string, **"uri"**: string, **"uri_hash"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/params

#### GET
##### 摘要

Params 查询 x/bank 模块的参数。

##### 响应

| Code | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 一个成功的响应。 | { **"params"**: { **"send_enabled"**: [ { **"denom"**: string, **"enabled"**: boolean } ], **"default_send_enabled"**: boolean } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/send_enabled

#### GET
##### 摘要

SendEnabled 查询 SendEnabled 条目。

##### 描述

此查询仅返回具有特定 SendEnabled 设置的代币单位。任何没有特定设置的代币单位将使用默认的 params.default_send_enabled，并且不会由此查询返回。自：cosmos-sdk 0.47

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| denoms | query | denoms 是您想要查找的特定代币单位。留空以获取所有条目。 | 否 | [ string ] |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，可在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为由每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数（在 UI 中）。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"send_enabled"**: [ { **"denom"**: string, **"enabled"**: boolean } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/spendable_balances/{address}

#### GET
##### 摘要

SpendableBalances 查询单个账户所有代币的可花费余额。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 Gas。自 cosmos-sdk 0.46 起

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是要查询可花费余额的地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 时，表示结果集应包含可分页项目总数的计数，用于用户界面。count_total 仅在使用了 offset 时被遵循。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 时，结果将按降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"balances"**: [ { **"denom"**: string, **"amount"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/spendable_balances/{address}/by_denom

#### GET
##### 摘要

SpendableBalanceByDenom 查询单个账户的单个代币面额的可花费余额。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。自：cosmos-sdk 0.47

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是要查询余额的地址。 | 是 | string |
| denom | query | denom 是要查询余额的代币面额。 | 否 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"balance"**: { **"denom"**: string, **"amount"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/supply

#### GET
##### 摘要

TotalSupply 查询所有币的总供应量。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项数，在用户界面中。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"supply"**: [ { **"denom"**: string, **"amount"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/bank/v1beta1/supply/by_denom

#### GET
##### 摘要

SupplyOf 查询单个代币的供应量。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| denom | query | denom 是要查询余额的代币单位。 | 否 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"amount"**: { **"denom"**: string, **"amount"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/community_pool

#### GET
##### 摘要

CommunityPool 查询社区池的代币。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"pool"**: [ { **"denom"**: string, **"amount"**: string } ] } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/delegators/{delegator_address}/rewards

#### GET
##### 总结

DelegationTotalRewards 查询每个验证者累积的总奖励。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_address | path | delegator_address 定义了要查询的委托者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"rewards"**: [ { **"validator_address"**: string, **"reward"**: [ { **"denom"**: string, **"amount"**: string } ] } ], **"total"**: [ { **"denom"**: string, **"amount"**: string } ] } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/delegators/{delegator_address}/rewards/{validator_address}

#### GET
##### 摘要

DelegationRewards 查询委托累积的总奖励。

##### 参数

| 名称 | 位置 | 描述 | 必填 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_address | path | delegator_address 定义了要查询的委托者地址。 | 是 | string |
| validator_address | path | validator_address 定义了要查询的验证者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"rewards"**: [ { **"denom"**: string, **"amount"**: string } ] } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/delegators/{delegator_address}/validators

#### GET
##### 总结

DelegatorValidators 查询委托者的验证者。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_address | path | delegator_address 定义了要查询的委托者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"validators"**: [ string ] } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/delegators/{delegator_address}/withdraw_address

#### GET
##### 总结

DelegatorWithdrawAddress 查询委托者的提取地址。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_address | path | delegator_address 定义了要查询的委托者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"withdraw_address"**: string } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/params

#### GET
##### 摘要

Params 查询分发模块的参数。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"params"**: { **"community_tax"**: string, **"base_proposer_reward"**: string, **"bonus_proposer_reward"**: string, **"withdraw_addr_enabled"**: boolean } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/validators/{validator_address}

#### GET
##### 摘要

ValidatorDistributionInfo 查询验证者的佣金和自委托奖励。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_address | path | validator_address 定义了要查询的验证者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"operator_address"**: string, **"self_bond_rewards"**: [ { **"denom"**: string, **"amount"**: string } ], **"commission"**: [ { **"denom"**: string, **"amount"**: string } ] } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/validators/{validator_address}/commission

#### GET
##### Summary

ValidatorCommission 查询验证者的累计佣金。

##### Parameters

| 名称 | 位置 | 描述 | 是否必需 | Schema |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_address | path | validator_address 定义了要查询的验证者地址。 | 是 | string |

##### Responses

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"commission"**: { **"commission"**: [ { **"denom"**: string, **"amount"**: string } ] } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/validators/{validator_address}/outstanding_rewards

#### GET
##### Summary

ValidatorOutstandingRewards 查询验证者地址的奖励。

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_address | path | validator_address 定义了要查询的验证者地址。 | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"rewards"**: { **"rewards"**: [ { **"denom"**: string, **"amount"**: string } ] } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/distribution/v1beta1/validators/{validator_address}/slashes

#### GET
##### 总结

ValidatorSlashes 查询验证者的罚没事件。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_address | path | validator_address 定义要查询的验证者地址。 | 是 | string |
| starting_height | query | starting_height 定义查询罚没事件的可选起始高度。 | 否 | string (uint64) |
| ending_height | query | ending_height 定义查询罚没事件的可选结束高度。 | 否 | string (uint64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。offset 或 key 中只能设置一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，可在 key 不可用时使用。它的效率低于使用 key。offset 或 key 中只能设置一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为由每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包含可分页总项目数的计数，用于用户界面。count_total 仅在使用了 offset 时被遵循。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"slashes"**: [ { **"validator_period"**: string (uint64), **"fraction"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/constitution

#### GET
##### 摘要

Constitution 查询链的宪法。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"constitution"**: string } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/params/{params_type}

#### GET
##### 概述

Params 查询治理模块的所有参数。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| params_type | path | params_type 定义要查询的参数类型，可以是 "voting"、"tallying" 或 "deposit" 之一。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"voting_params"**: { **"voting_period"**: string }, **"deposit_params"**: { **"min_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"max_deposit_period"**: string }, **"tally_params"**: { **"quorum"**: string, **"threshold"**: string, **"veto_threshold"**: string }, **"params"**: { **"min_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"max_deposit_period"**: string, **"voting_period"**: string, **"quorum"**: string, **"threshold"**: string, **"veto_threshold"**: string, **"min_initial_deposit_ratio"**: string, **"proposal_cancel_ratio"**: string, **"proposal_cancel_dest"**: string, **"expedited_voting_period"**: string, **"expedited_threshold"**: string, **"expedited_min_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"burn_vote_quorum"**: boolean, **"burn_proposal_deposit_prevote"**: boolean, **"burn_vote_veto"**: boolean, **"min_deposit_ratio"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/proposals

#### GET
##### 摘要

提案查询基于给定状态的所有提案。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_status | query | proposal_status 定义提案的状态。 - PROPOSAL_STATUS_UNSPECIFIED: PROPOSAL_STATUS_UNSPECIFIED 定义默认提案状态。 - PROPOSAL_STATUS_DEPOSIT_PERIOD: PROPOSAL_STATUS_DEPOSIT_PERIOD 定义存款期间的提案状态。 - PROPOSAL_STATUS_VOTING_PERIOD: PROPOSAL_STATUS_VOTING_PERIOD 定义投票期间的提案状态。 - PROPOSAL_STATUS_PASSED: PROPOSAL_STATUS_PASSED 定义已通过提案的状态。 - PROPOSAL_STATUS_REJECTED: PROPOSAL_STATUS_REJECTED 定义已被拒绝提案的状态。 - PROPOSAL_STATUS_FAILED: PROPOSAL_STATUS_FAILED 定义已失败提案的状态。 | 否 | string |
| voter | query | voter 定义提案的投票者地址。 | 否 | string |
| depositor | query | depositor 定义提案的存款地址。 | 否 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 其中之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 其中之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自 cosmos-sdk 0.43 起。 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"proposals"**: [ { **"id"**: string (uint64), **"messages"**: [ { **"type_url"**: string, **"value"**: byte } ], **"status"**: string, **"final_tally_result"**: { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string }, **"submit_time"**: dateTime, **"deposit_end_time"**: dateTime, **"total_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"voting_start_time"**: dateTime, **"voting_end_time"**: dateTime, **"metadata"**: string, **"title"**: string, **"summary"**: string, **"proposer"**: string, **"expedited"**: boolean, **"failed_reason"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/proposals/{proposal_id}

#### GET
##### 摘要

提案查询基于 ProposalID 的提案详情。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 定义提案的唯一 ID。 | Yes | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"proposal"**: { **"id"**: string (uint64), **"messages"**: [ { **"type_url"**: string, **"value"**: byte } ], **"status"**: string, **"final_tally_result"**: { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string }, **"submit_time"**: dateTime, **"deposit_end_time"**: dateTime, **"total_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"voting_start_time"**: dateTime, **"voting_end_time"**: dateTime, **"metadata"**: string, **"title"**: string, **"summary"**: string, **"proposer"**: string, **"expedited"**: boolean, **"failed_reason"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/proposals/{proposal_id}/deposits

#### GET
##### 摘要

存入查询单个提案的所有存入。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 定义提案的唯一 ID。 | 是 | string (uint64) |
| pagination.key | query | key 是在 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 其中之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，可在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 其中之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是要在结果页面中返回的结果总数。如果留空，将默认设置为每个应用程序定义的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包含可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果应按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"deposits"**: [ { **"proposal_id"**: string (uint64), **"depositor"**: string, **"amount"**: [ { **"denom"**: string, **"amount"**: string } ] } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/proposals/{proposal_id}/deposits/{depositor}

#### GET
##### 摘要

根据 proposalID 和 depositAddr 查询单个存款信息。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 定义提案的唯一 ID。 | Yes | string (uint64) |
| depositor | path | depositor 定义来自提案的存款地址。 | Yes | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"deposit"**: { **"proposal_id"**: string (uint64), **"depositor"**: string, **"amount"**: [ { **"denom"**: string, **"amount"**: string } ] } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/proposals/{proposal_id}/tally

#### GET
##### 摘要

TallyResult 查询提案投票的计票结果。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 定义提案的唯一标识。 | 是 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"tally"**: { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/proposals/{proposal_id}/votes

#### GET

##### 总结

查询给定提案的投票。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 定义提案的唯一 ID。 | 是 | string (uint64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"votes"**: [ { **"proposal_id"**: string (uint64), **"voter"**: string, **"options"**: [ { **"option"**: string, **"weight"**: string } ], **"metadata"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/gov/v1/proposals/{proposal_id}/votes/{voter}

#### GET
##### 摘要

投票查询基于 proposalID 和 voterAddr 的投票信息。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 定义提案的唯一 ID。 | 是 | string (uint64) |
| voter | path | voter 定义提案的投票者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"vote"**: { **"proposal_id"**: string (uint64), **"voter"**: string, **"options"**: [ { **"option"**: string, **"weight"**: string } ], **"metadata"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/params/v1beta1/params

#### GET
##### 摘要

Params 查询模块的特定参数，给定其 subspace 和 key。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| subspace | query | subspace 定义了要查询参数的模块。 | 否 | string |
| key | query | key 定义了 subspace 中参数的键。 | 否 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"param"**: { **"subspace"**: string, **"key"**: string, **"value"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/params/v1beta1/subspaces

#### GET
##### 摘要

子空间查询所有已注册的子空间以及一个子空间的所有键。

##### 描述

自： cosmos-sdk 0.46

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"subspaces"**: [ { **"subspace"**: string, **"keys"**: [ string ] } ] } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/slashing/v1beta1/params

#### GET
##### 摘要

Params 查询惩罚模块的参数

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"params"**: { **"signed_blocks_window"**: string (int64), **"min_signed_per_window"**: byte, **"downtime_jail_duration"**: string, **"slash_fraction_double_sign"**: byte, **"slash_fraction_downtime"**: byte } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/slashing/v1beta1/signing_infos

#### GET
##### 摘要

SigningInfos 查询所有验证者的签名信息

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"info"**: [ { **"address"**: string, **"start_height"**: string (int64), **"index_offset"**: string (int64), **"jailed_until"**: dateTime, **"tombstoned"**: boolean, **"missed_blocks_counter"**: string (int64) } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/slashing/v1beta1/signing_infos/{cons_address}

#### GET
##### 摘要

SigningInfo 查询给定 cons_address 的签名信息

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| cons_address | path | cons_address 是要查询签名信息的地址 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | { **"val_signing_info"**: { **"address"**: string, **"start_height"**: string (int64), **"index_offset"**: string (int64), **"jailed_until"**: dateTime, **"tombstoned"**: boolean, **"missed_blocks_counter"**: string (int64) } } |
| default | 意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/delegations/{delegator_addr}

#### GET
##### 总结

DelegatorDelegations 查询给定委托者地址的所有委托。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_addr | path | delegator_addr 定义了要查询的委托者地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数（在 UI 中）。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 时，结果将以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"delegation_responses"**: [ { **"delegation"**: { **"delegator_address"**: string, **"validator_address"**: string, **"shares"**: string }, **"balance"**: { **"denom"**: string, **"amount"**: string } } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/delegators/{delegator_addr}/redelegations

#### GET
##### 摘要

重新委托查询给定地址的重新委托记录。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_addr | path | delegator_addr 定义要查询的委托者地址。 | 是 | string |
| src_validator_addr | query | src_validator_addr 定义要从中重新委托的验证者地址。 | 否 | string |
| dst_validator_addr | query | dst_validator_addr 定义要重新委托到的验证者地址。 | 否 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果应按降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"redelegation_responses"**: [ { **"redelegation"**: { **"delegator_address"**: string, **"validator_src_address"**: string, **"validator_dst_address"**: string, **"entries"**: [ { **"creation_height"**: string (int64), **"completion_time"**: dateTime, **"initial_balance"**: string, **"shares_dst"**: string, **"unbonding_id"**: string (uint64), **"unbonding_on_hold_ref_count"**: string (int64) } ] }, **"entries"**: [ { **"redelegation_entry"**: { **"creation_height"**: string (int64), **"completion_time"**: dateTime, **"initial_balance"**: string, **"shares_dst"**: string, **"unbonding_id"**: string (uint64), **"unbonding_on_hold_ref_count"**: string (int64) }, **"balance"**: string } ] } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/delegators/{delegator_addr}/unbonding_delegations

#### GET
##### 摘要

DelegatorUnbondingDelegations 查询给定委托者地址的所有解绑委托。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_addr | path | delegator_addr 定义了要查询的委托者地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只应设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，可在 key 不可用时使用。它的效率低于使用 key。只应设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包含可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵循。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果应按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"unbonding_responses"**: [ { **"delegator_address"**: string, **"validator_address"**: string, **"entries"**: [ { **"creation_height"**: string (int64), **"completion_time"**: dateTime, **"initial_balance"**: string, **"balance"**: string, **"unbonding_id"**: string (uint64), **"unbonding_on_hold_ref_count"**: string (int64) } ] } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/delegators/{delegator_addr}/validators

#### GET
##### 摘要

DelegatorValidators 查询给定委托者地址的所有验证者信息。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| delegator_addr | path | delegator_addr 定义了要查询的委托者地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"validators"**: [ { **"operator_address"**: string, **"consensus_pubkey"**: { **"type_url"**: string, **"value"**: byte }, **"jailed"**: boolean, **"status"**: string, **"tokens"**: string, **"delegator_shares"**: string, **"description"**: { **"moniker"**: string, **"identity"**: string, **"website"**: string, **"security_contact"**: string, **"details"**: string }, **"unbonding_height"**: string (int64), **"unbonding_time"**: dateTime, **"commission"**: { **"commission_rates"**: { **"rate"**: string, **"max_rate"**: string, **"max_change_rate"**: string }, **"update_time"**: dateTime }, **"min_self_delegation"**: string, **"unbonding_on_hold_ref_count"**: string (int64), **"unbonding_ids"**: [ string (uint64) ] } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/delegators/{delegator_addr}/validators/{validator_addr}

#### GET
##### 摘要

DelegatorValidator 查询给定委托者验证者对中的验证者信息。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---- | ---- | -------- | ---- |
| delegator_addr | path | delegator_addr 定义了要查询的委托者地址。 | 是 | string |
| validator_addr | path | validator_addr 定义了要查询的验证者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"validator"**: { **"operator_address"**: string, **"consensus_pubkey"**: { **"type_url"**: string, **"value"**: byte }, **"jailed"**: boolean, **"status"**: string, **"tokens"**: string, **"delegator_shares"**: string, **"description"**: { **"moniker"**: string, **"identity"**: string, **"website"**: string, **"security_contact"**: string, **"details"**: string }, **"unbonding_height"**: string (int64), **"unbonding_time"**: dateTime, **"commission"**: { **"commission_rates"**: { **"rate"**: string, **"max_rate"**: string, **"max_change_rate"**: string }, **"update_time"**: dateTime }, **"min_self_delegation"**: string, **"unbonding_on_hold_ref_count"**: string (int64), **"unbonding_ids"**: [ string (uint64) ] } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/historical_info/{height}

#### GET
##### 总结

HistoricalInfo 查询指定高度的历史信息。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| height | path | height 定义了查询历史信息的高度。 | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"hist"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"valset"**: [ { **"operator_address"**: string, **"consensus_pubkey"**: { **"type_url"**: string, **"value"**: byte }, **"jailed"**: boolean, **"status"**: string, **"tokens"**: string, **"delegator_shares"**: string, **"description"**: { **"moniker"**: string, **"identity"**: string, **"website"**: string, **"security_contact"**: string, **"details"**: string }, **"unbonding_height"**: string (int64), **"unbonding_time"**: dateTime, **"commission"**: { **"commission_rates"**: { **"rate"**: string, **"max_rate"**: string, **"max_change_rate"**: string }, **"update_time"**: dateTime }, **"min_self_delegation"**: string, **"unbonding_on_hold_ref_count"**: string (int64), **"unbonding_ids"**: [ string (uint64) ] } ] } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/params

#### GET
##### 总结

查询质押参数。

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"params"**: { **"unbonding_time"**: string, **"max_validators"**: long, **"max_entries"**: long, **"historical_entries"**: long, **"bond_denom"**: string, **"min_commission_rate"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/pool

#### GET
##### 摘要

查询池信息。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"pool"**: { **"not_bonded_tokens"**: string, **"bonded_tokens"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/validators

#### GET
##### 摘要

验证者查询所有匹配给定状态的验证者。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 必填 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| status | query | status 允许查询匹配给定状态的验证者。 | 否 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 其中之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 其中之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"validators"**: [ { **"operator_address"**: string, **"consensus_pubkey"**: { **"type_url"**: string, **"value"**: byte }, **"jailed"**: boolean, **"status"**: string, **"tokens"**: string, **"delegator_shares"**: string, **"description"**: { **"moniker"**: string, **"identity"**: string, **"website"**: string, **"security_contact"**: string, **"details"**: string }, **"unbonding_height"**: string (int64), **"unbonding_time"**: dateTime, **"commission"**: { **"commission_rates"**: { **"rate"**: string, **"max_rate"**: string, **"max_change_rate"**: string }, **"update_time"**: dateTime }, **"min_self_delegation"**: string, **"unbonding_on_hold_ref_count"**: string (int64), **"unbonding_ids"**: [ string (uint64) ] } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/validators/{validator_addr}

#### GET
##### 摘要

验证者查询给定验证者地址的验证者信息。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_addr | path | validator_addr 定义了要查询的验证者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"validator"**: { **"operator_address"**: string, **"consensus_pubkey"**: { **"type_url"**: string, **"value"**: byte }, **"jailed"**: boolean, **"status"**: string, **"tokens"**: string, **"delegator_shares"**: string, **"description"**: { **"moniker"**: string, **"identity"**: string, **"website"**: string, **"security_contact"**: string, **"details"**: string }, **"unbonding_height"**: string (int64), **"unbonding_time"**: dateTime, **"commission"**: { **"commission_rates"**: { **"rate"**: string, **"max_rate"**: string, **"max_change_rate"**: string }, **"update_time"**: dateTime }, **"min_self_delegation"**: string, **"unbonding_on_hold_ref_count"**: string (int64), **"unbonding_ids"**: [ string (uint64) ] } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/validators/{validator_addr}/delegations

#### GET
##### 摘要

ValidatorDelegations 查询给定验证者的委托信息。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_addr | path | validator_addr 定义了要查询的验证者地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"delegation_responses"**: [ { **"delegation"**: { **"delegator_address"**: string, **"validator_address"**: string, **"shares"**: string }, **"balance"**: { **"denom"**: string, **"amount"**: string } } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/validators/{validator_addr}/delegations/{delegator_addr}

#### GET
##### 总结

委托查询给定验证者-委托者对的信息。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_addr | path | validator_addr 定义了要查询的验证者地址。 | 是 | string |
| delegator_addr | path | delegator_addr 定义了要查询的委托者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"delegation_response"**: { **"delegation"**: { **"delegator_address"**: string, **"validator_address"**: string, **"shares"**: string }, **"balance"**: { **"denom"**: string, **"amount"**: string } } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/validators/{validator_addr}/delegations/{delegator_addr}/unbonding_delegation

#### GET
##### 总结

UnbondingDelegation 查询给定验证者和委托者对的解绑信息。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_addr | path | validator_addr 定义了要查询的验证者地址。 | 是 | string |
| delegator_addr | path | delegator_addr 定义了要查询的委托者地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"unbond"**: { **"delegator_address"**: string, **"validator_address"**: string, **"entries"**: [ { **"creation_height"**: string (int64), **"completion_time"**: dateTime, **"initial_balance"**: string, **"balance"**: string, **"unbonding_id"**: string (uint64), **"unbonding_on_hold_ref_count"**: string (int64) } ] } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/staking/v1beta1/validators/{validator_addr}/unbonding_delegations

#### GET
##### 总结

ValidatorUnbondingDelegations 查询验证者的解绑委托。

##### 描述

当从另一个模块调用时，如果分页字段设置不正确，此查询可能会消耗大量 gas。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| validator_addr | path | validator_addr 定义了要查询的验证者地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"unbonding_responses"**: [ { **"delegator_address"**: string, **"validator_address"**: string, **"entries"**: [ { **"creation_height"**: string (int64), **"completion_time"**: dateTime, **"initial_balance"**: string, **"balance"**: string, **"unbonding_id"**: string (uint64), **"unbonding_on_hold_ref_count"**: string (int64) } ] } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/upgrade/v1beta1/applied_plan/{name}

#### GET
##### 摘要

AppliedPlan 通过名称查询先前应用的升级计划。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---- | ---- | -------- | ---- |
| name | path | name 是要查询的应用计划的名称。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"height"**: string (int64) } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/upgrade/v1beta1/authority

#### GET
##### 总结

返回具有执行升级权限的账户。

##### 描述

自 cosmos-sdk 0.46

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 一个成功的响应。 | { **"address"**: string } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/upgrade/v1beta1/current_plan

#### GET
##### 总结

CurrentPlan 查询当前升级计划。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"plan"**: { **"name"**: string, **"time"**: dateTime, **"height"**: string (int64), **"info"**: string, **"upgraded_client_state"**: { **"type_url"**: string, **"value"**: byte } } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/upgrade/v1beta1/module_versions

#### GET
##### Summary

ModuleVersions 从状态查询模块版本的列表。

##### Description

自： cosmos-sdk 0.43

##### Parameters

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| module_name | query | module_name 是一个用于从状态查询特定模块共识版本的字段。留空此字段将从状态获取完整的模块版本列表。 | 否 | string |

##### Responses

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"module_versions"**: [ { **"name"**: string, **"version"**: string (uint64) } ] } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/upgrade/v1beta1/upgraded_consensus_state/{last_height}

#### GET
##### 摘要

UpgradedConsensusState 查询将作为该链下一个版本的可信内核的共识状态。它只会存储在该链的最后一个高度。UpgradedConsensusState RPC 不支持旧版查询器。此 RPC 现已弃用，因为 IBC 有自己的替代方案 (https://github.com/cosmos/ibc-go/blob/2c880a22e9f9cc75f62b527ca94aa75ce1106001/proto/ibc/core/client/v1/query.proto#L54)

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---- | ---- | -------- | ---- |
| last_height | path | 当前链的最后一个高度必须在请求中发送，因为这是存储下一个共识状态的高度 | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"upgraded_consensus_state"**: byte } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/authz/v1beta1/grants

#### GET
##### 摘要

返回由授权者授予被授权者的 `Authorization` 列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| granter | query |  | 否 | string |
| grantee | query |  | 否 | string |
| msg_type_url | query | 可选，msg_type_url，当设置时，将仅查询匹配给定消息类型的授权。 | 否 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 时，表示结果集应包括可用于分页的总项目数计数（在 UI 中）。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 时，结果将以降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | { **"grants"**: [ { **"authorization"**: { **"type_url"**: string, **"value"**: byte }, **"expiration"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/authz/v1beta1/grants/grantee/{grantee}

#### GET
##### 总结

GranteeGrants 返回一个由 grantee 授权的 `GrantAuthorization` 列表。

##### 描述

自： cosmos-sdk 0.46

##### 参数

| 名称 | 位置 | 描述 | 必填 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| grantee | path |  | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括在 UI 中可用于分页的总项目数。count_total 仅在 offset 使用时被尊重。当 key 设置时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自： cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"grants"**: [ { **"granter"**: string, **"grantee"**: string, **"authorization"**: { **"type_url"**: string, **"value"**: byte }, **"expiration"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/authz/v1beta1/grants/granter/{granter}

#### GET
##### 摘要

GranterGrants 返回由授权者授予的 `GrantAuthorization` 列表。

##### 描述

Since: cosmos-sdk 0.46

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| granter | path |  | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的总结果数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。Since: cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"grants"**: [ { **"granter"**: string, **"grantee"**: string, **"authorization"**: { **"type_url"**: string, **"value"**: byte }, **"expiration"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/group_info/{group_id}

#### GET
##### 摘要

GroupInfo 根据组 ID 查询组信息。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| group_id | path | group_id 是组的唯一 ID。 | 是 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"info"**: { **"id"**: string (uint64), **"admin"**: string, **"metadata"**: string, **"version"**: string (uint64), **"total_weight"**: string, **"created_at"**: dateTime } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/group_members/{group_id}

#### GET
##### 摘要

GroupMembers 通过组 ID 查询组的成员。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| group_id | path | group_id 是组的唯一 ID。 | 是 | string (uint64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"members"**: [ { **"group_id"**: string (uint64), **"member"**: { **"address"**: string, **"weight"**: string, **"metadata"**: string, **"added_at"**: dateTime } } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/group_policies_by_admin/{admin}

#### GET
##### 摘要

GroupPoliciesByAdmin 通过管理员地址查询群组策略。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| admin | path | admin 是群组策略的管理员地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 其中之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 其中之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 时，表示结果集应包括可用于分页的总项目数，在 UI 中显示。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 时，结果按降序返回。自 cosmos-sdk 0.43 起。 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"group_policies"**: [ { **"address"**: string, **"group_id"**: string (uint64), **"admin"**: string, **"metadata"**: string, **"version"**: string (uint64), **"decision_policy"**: { **"type_url"**: string, **"value"**: byte }, **"created_at"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/group_policies_by_group/{group_id}

#### GET
##### 摘要

GroupPoliciesByGroup 通过群组 ID 查询群组策略。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| group_id | path | group_id 是群组策略所属群组的唯一 ID。 | Yes | string (uint64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | No | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | No | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | No | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | No | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | No | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"group_policies"**: [ { **"address"**: string, **"group_id"**: string (uint64), **"admin"**: string, **"metadata"**: string, **"version"**: string (uint64), **"decision_policy"**: { **"type_url"**: string, **"value"**: byte }, **"created_at"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/group_policy_info/{address}

#### GET
##### 摘要

GroupPolicyInfo 根据组策略的账户地址查询组策略信息。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是组策略的账户地址。 | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"info"**: { **"address"**: string, **"group_id"**: string (uint64), **"admin"**: string, **"metadata"**: string, **"version"**: string (uint64), **"decision_policy"**: { **"type_url"**: string, **"value"**: byte }, **"created_at"**: dateTime } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/groups

#### GET
##### 摘要

群组查询状态中的所有群组。

##### 描述

自 cosmos-sdk 0.47.1

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以表示结果集应包括可用于分页的总项目数的计数。count_total 仅在 offset 使用时被尊重。当 key 设置时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自 cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"groups"**: [ { **"id"**: string (uint64), **"admin"**: string, **"metadata"**: string, **"version"**: string (uint64), **"total_weight"**: string, **"created_at"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/groups_by_admin/{admin}

#### GET
##### 摘要

GroupsByAdmin 通过管理员地址查询群组。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| admin | path | admin 是群组管理员的账户地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 其中之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 其中之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 时，表示结果集应包含可用于分页的总项目数，用于 UI 中。count_total 仅在使用了 offset 时被尊重，当 key 被设置时会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 时，结果将按降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"groups"**: [ { **"id"**: string (uint64), **"admin"**: string, **"metadata"**: string, **"version"**: string (uint64), **"total_weight"**: string, **"created_at"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/groups_by_member/{address}

#### GET
##### 摘要

GroupsByMember 通过成员地址查询群组。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是群组成员地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵循。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"groups"**: [ { **"id"**: string (uint64), **"admin"**: string, **"metadata"**: string, **"version"**: string (uint64), **"total_weight"**: string, **"created_at"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/proposal/{proposal_id}

#### GET
##### 摘要

根据提案 ID 查询提案。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 是提案的唯一 ID。 | 是 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"proposal"**: { **"id"**: string (uint64), **"group_policy_address"**: string, **"metadata"**: string, **"proposers"**: [ string ], **"submit_time"**: dateTime, **"group_version"**: string (uint64), **"group_policy_version"**: string (uint64), **"status"**: string, **"final_tally_result"**: { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string }, **"voting_period_end"**: dateTime, **"executor_result"**: string, **"messages"**: [ { **"type_url"**: string, **"value"**: byte } ], **"title"**: string, **"summary"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/proposals/{proposal_id}/tally

#### GET
##### 摘要

计票结果返回一个提案的投票结果。如果提案仍在投票期内，则此查询计算当前的计票状态，该状态可能不是最终的。另一方面，如果提案已最终确定，则它直接返回存储在提案本身的 `final_tally_result` 状态。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 是提案的唯一标识符。 | 是 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"tally"**: { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/proposals_by_group_policy/{address}

#### GET
##### 摘要

ProposalsByGroupPolicy 根据组策略的账户地址查询提案。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path | address 是与提案相关的组策略的账户地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包含可分页总项目数的计数，用于用户界面。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"proposals"**: [ { **"id"**: string (uint64), **"group_policy_address"**: string, **"metadata"**: string, **"proposers"**: [ string ], **"submit_time"**: dateTime, **"group_version"**: string (uint64), **"group_policy_version"**: string (uint64), **"status"**: string, **"final_tally_result"**: { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string }, **"voting_period_end"**: dateTime, **"executor_result"**: string, **"messages"**: [ { **"type_url"**: string, **"value"**: byte } ], **"title"**: string, **"summary"**: string } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/vote_by_proposal_voter/{proposal_id}/{voter}

#### GET
##### 摘要

VoteByProposalVoter 通过提案 ID 和投票者查询投票。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 是提案的唯一 ID。 | Yes | string (uint64) |
| voter | path | voter 是提案投票者的账户地址。 | Yes | string |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"vote"**: { **"proposal_id"**: string (uint64), **"voter"**: string, **"option"**: string, **"metadata"**: string, **"submit_time"**: dateTime } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/votes_by_proposal/{proposal_id}

#### GET
##### 摘要

VotesByProposal 通过提案 ID 查询投票。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| proposal_id | path | proposal_id 是提案的唯一 ID。 | 是 | string (uint64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的总结果数。如果留空，将默认设置为每个应用指定的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数计数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"votes"**: [ { **"proposal_id"**: string (uint64), **"voter"**: string, **"option"**: string, **"metadata"**: string, **"submit_time"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/group/v1/votes_by_voter/{voter}

#### GET
##### 摘要

VotesByVoter 查询一个投票者的投票。

##### 参数

| 名称 | 位置 | 描述 | 必需 | Schema |
| ---- | ---------- | ----------- | -------- | ------ |
| voter | path | voter 是一个提案投票者账户地址。 | 是 | string |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 表示结果集应包含可用于分页的总项目数计数。count_total 仅在 offset 使用时被遵守。当 key 设置时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"votes"**: [ { **"proposal_id"**: string (uint64), **"voter"**: string, **"option"**: string, **"metadata"**: string, **"submit_time"**: dateTime } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/consensus/v1/params

#### GET
##### 摘要

Params 查询 x/consensus 模块的参数。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"params"**: { **"block"**: { **"max_bytes"**: string (int64), **"max_gas"**: string (int64) }, **"evidence"**: { **"max_age_num_blocks"**: string (int64), **"max_age_duration"**: string, **"max_bytes"**: string (int64) }, **"validator"**: { **"pub_key_types"**: [ string ] }, **"version"**: { **"app"**: string (uint64) }, **"abci"**: { **"vote_extensions_enable_height"**: string (int64) } } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /zeta-chain/authority/authorization/{msgUrl}

#### GET
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| msgUrl | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.authority.QueryAuthorizationResponse](#zetachainzetacoreauthorityqueryauthorizationresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/authority/authorizations

#### GET
##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.authority.QueryAuthorizationListResponse](#zetachainzetacoreauthorityqueryauthorizationlistresponse) |
| default | 意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/authority/chainInfo

#### GET
##### 摘要

查询 ChainInfo

##### 响应

| 代码 | 描述 | 模式 |
| ---- | -------- | ---- |
| 200 | 一个成功的响应。 | [zetachain.zetacore.authority.QueryGetChainInfoResponse](#zetachainzetacoreauthorityquerygetchaininforesponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/authority/policies

#### GET
##### 摘要

查询策略

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.authority.QueryGetPoliciesResponse](#zetachainzetacoreauthorityquerygetpoliciesresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/cctx

#### GET
##### 摘要

查询 cctx 项目列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | No | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | No | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | No | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数，在用户界面中。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | No | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | No | boolean |
| unordered | query | 批量转储所有 CCTX，不排序。这对于初始化 CCTX 索引器很有用。 | No | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryAllCctxResponse](#zetachainzetacorecrosschainqueryallcctxresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/cctx/{chainID}/{nonce}

#### GET
##### 摘要

通过 nonce 查询一个 cctx。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainID | path |  | 是 | string (int64) |
| nonce | path |  | 是 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryGetCctxResponse](#zetachainzetacorecrosschainquerygetcctxresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/cctx/{index}

#### GET
##### 总结

通过索引查询跨链交易。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---- | ---- | -------- | ---- |
| index | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryGetCctxResponse](#zetachainzetacorecrosschainquerygetcctxresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/convertGasToZeta

#### GET
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | query |  | No | string (int64) |
| gasLimit | query |  | No | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryConvertGasToZetaResponse](#zetachainzetacorecrosschainqueryconvertgastozetaresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/gasPrice

#### GET
##### 摘要

查询燃气价格项目列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数，在用户界面中显示。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllGasPriceResponse](#zetachainzetacorecrosschainqueryallgaspriceresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/gasPrice/{index}

#### GET
##### 摘要

通过索引查询 gasPrice。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| index | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryGetGasPriceResponse](#zetachainzetacorecrosschainquerygetgaspriceresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inTxHashToCctx

#### GET
***已弃用***
##### 摘要

已弃用(v17)：使用 InboundHashToCctxAll

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | No | byte |
| pagination.offset | query | offset 是一个数字偏移量，可在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | No | string (uint64) |
| pagination.limit | query | limit 是要在结果页面中返回的结果总数。如果留空，将默认为由每个应用设置的值。 | No | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包含可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵循。当设置了 key 时，它会被忽略。 | No | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果应按降序返回。自：cosmos-sdk 0.43 | No | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.crosschain.QueryAllInboundHashToCctxResponse](#zetachainzetacorecrosschainqueryallinboundhashtocctxresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inTxHashToCctx/{inboundHash}

#### GET
***已弃用***
##### 摘要

已弃用 (v17)：使用 InboundHashToCctx

##### 参数

| 名称 | 位置 | 描述 | 必填 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| inboundHash | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryGetInboundHashToCctxResponse](#zetachainzetacorecrosschainquerygetinboundhashtocctxresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inTxHashToCctxData/{inboundHash}

#### GET
***已弃用***
##### 摘要

已弃用 (v17)：使用 InboundHashToCctxData

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| inboundHash | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryInboundHashToCctxDataResponse](#zetachainzetacorecrosschainqueryinboundhashtocctxdataresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inTxTracker

#### GET
***已弃用***
##### 摘要

已弃用 (v17)：请使用 InboundTrackerAll

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。仅当使用 offset 时，count_total 才被尊重。当设置 key 时，它将被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllInboundTrackersResponse](#zetachainzetacorecrosschainqueryallinboundtrackersresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inTxTrackerByChain/{chainId}

#### GET
***已弃用***
##### 摘要

已弃用 (v17)：请使用 InboundTrackerAllByChain

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | 是 | string (int64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllInboundTrackerByChainResponse](#zetachainzetacorecrosschainqueryallinboundtrackerbychainresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inboundHashToCctx

#### GET
##### 总结

查询 InboundHashToCctx 项列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllInboundHashToCctxResponse](#zetachainzetacorecrosschainqueryallinboundhashtocctxresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inboundHashToCctx/{inboundHash}

#### GET
##### 总结

通过索引查询 InboundHashToCctx。

##### 参数

| 名称 | 位置 | 描述 | 必填 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| inboundHash | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryGetInboundHashToCctxResponse](#zetachainzetacorecrosschainquerygetinboundhashtocctxresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inboundHashToCctxData/{inboundHash}

#### GET
##### 摘要

按索引查询 InboundHashToCctx 数据。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| inboundHash | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryInboundHashToCctxDataResponse](#zetachainzetacorecrosschainqueryinboundhashtocctxdataresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inboundTracker/{chainId}/{txHash}

#### GET
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | Yes | string (int64) |
| txHash | path |  | Yes | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryInboundTrackerResponse](#zetachainzetacorecrosschainqueryinboundtrackerresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inboundTrackerByChain/{chainId}

#### GET

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---- | ---- | ---- | ---- |
| chainId | path |  | 是 | string (int64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllInboundTrackerByChainResponse](#zetachainzetacorecrosschainqueryallinboundtrackerbychainresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/inboundTrackers

#### GET

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllInboundTrackersResponse] |
| default | 意外错误响应。 | [google.rpc.Status] |

### /zeta-chain/crosschain/lastBlockHeight

#### GET
##### 总结

查询 lastBlockHeight 项目的列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | No | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | No | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | No | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数，在 UI 中。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | No | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | No | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllLastBlockHeightResponse](#zetachainzetacorecrosschainqueryalllastblockheightresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/lastBlockHeight/{index}

#### GET
##### 摘要

通过索引查询 lastBlockHeight。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---- | ---- | ---- | ---- |
| index | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryGetLastBlockHeightResponse](#zetachainzetacorecrosschainquerygetlastblockheightresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/lastZetaHeight

#### GET
##### 摘要

查询 lastMetaHeight 项的列表。

##### 响应

| 代码 | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryLastZetaHeightResponse](#zetachainzetacorecrosschainquerylastzetaheightresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/outTxTracker

#### GET
***已弃用***
##### 摘要

已弃用 (v17)：使用 OutboundTrackerAll

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---- | ---- | ---- | ---- |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，可在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllOutboundTrackerResponse](#zetachainzetacorecrosschainqueryalloutboundtrackerresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/outTxTracker/{chainID}/{nonce}

#### GET
***已弃用***
##### 摘要

已弃用 (v17)：使用 OutboundTracker

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainID | path |  | 是 | string (int64) |
| nonce | path |  | 是 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryGetOutboundTrackerResponse](#zetachainzetacorecrosschainquerygetoutboundtrackerresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/outTxTrackerByChain/{chain}

#### GET
***已弃用***
##### 摘要

已弃用 (v17)：使用 OutboundTrackerAllByChain

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chain | path |  | 是 | string (int64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryAllOutboundTrackerByChainResponse](#zetachainzetacorecrosschainqueryalloutboundtrackerbychainresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/outboundTracker

#### GET
##### 摘要

查询出站调用项目的列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包含可用于分页的总项目数计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果应按降序返回。自 cosmos-sdk 0.43 起。 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllOutboundTrackerResponse](#zetachainzetacorecrosschainqueryalloutboundtrackerresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/outboundTracker/{chainID}/{nonce}

#### GET
##### 总结

通过索引查询出站跟踪器。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainID | path |  | 是 | string (int64) |
| nonce | path |  | 是 | string (uint64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryGetOutboundTrackerResponse](#zetachainzetacorecrosschainquerygetoutboundtrackerresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/outboundTrackerByChain/{chain}

#### GET
##### 参数

| 名称 | 位置 | 描述 | 必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| chain | path |  | 是 | string (int64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认设置为每个应用程序所设定的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包含可用于分页的总项目数计数（在 UI 中）。count_total 仅在使用了 offset 时被遵循。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryAllOutboundTrackerByChainResponse](#zetachainzetacorecrosschainqueryalloutboundtrackerbychainresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/pendingCctx

#### GET
##### 总结

查询待处理的 cctx 列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | query |  | 否 | string (int64) |
| limit | query |  | 否 | long |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryListPendingCctxResponse](#zetachainzetacorecrosschainquerylistpendingcctxresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/pendingCctxWithinRateLimit

#### GET
##### 摘要

查询在速率限制内的待处理 cctxs 列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| limit | query |  | 否 | long |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryListPendingCctxWithinRateLimitResponse](#zetachainzetacorecrosschainquerylistpendingcctxwithinratelimitresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/protocolFee

#### GET
##### 响应

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.crosschain.QueryMessagePassingProtocolFeeResponse](#zetachainzetacorecrosschainquerymessagepassingprotocolfeeresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/rateLimiterFlags

#### GET
##### 摘要

查询速率限制器标志。

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.crosschain.QueryRateLimiterFlagsResponse](#zetachainzetacorecrosschainqueryratelimiterflagsresponse) |
| default | 意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/rateLimiterInput

#### GET
##### 摘要

查询速率限制器的输入数据。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---- | ---- | ---- | ---- |
| limit | query |  | 否 | long |
| window | query |  | 否 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | [zetachain.zetacore.crosschain.QueryRateLimiterInputResponse](#zetachainzetacorecrosschainqueryratelimiterinputresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/crosschain/zetaAccounting

#### GET
##### 响应

| 代码 | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.crosschain.QueryZetaAccountingResponse](#zetachainzetacorecrosschainqueryzetaaccountingresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/emissions/list_addresses

#### GET
##### 摘要

查询 ListBalances 项的列表。

##### 响应

| Code | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.emissions.QueryListPoolAddressesResponse](#zetachainzetacoreemissionsquerylistpooladdressesresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/emissions/params

#### GET
##### 摘要

查询模块的参数。

##### 响应

| 代码 | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.emissions.QueryParamsResponse](#zetachainzetacoreemissionsqueryparamsresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/emissions/show_available_emissions/{address}

#### GET
##### 总结

查询 ShowAvailableEmissions 项列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | Schema |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path |  | 是 | string |

##### 响应

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.emissions.QueryShowAvailableEmissionsResponse](#zetachainzetacoreemissionsqueryshowavailableemissionsresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/fungible/code_hash/{address}

#### GET
##### 摘要

代码哈希查询合约的代码哈希。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| address | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.fungible.QueryCodeHashResponse](#zetachainzetacorefungiblequerycodehashresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/fungible/foreign_coins

#### GET
##### 摘要

查询 ForeignCoins 项目的列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | No | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | No | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，它将默认为由每个应用设置的值。 | No | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以表示结果集应包括可用于分页的总项目数的计数。count_total 仅在 offset 使用时被尊重。当 key 设置时，它被忽略。 | No | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | No | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.fungible.QueryAllForeignCoinsResponse](#zetachainzetacorefungiblequeryallforeigncoinsresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/fungible/foreign_coins/{chainId}/{asset}

#### GET
##### 摘要

通过 chain_id 和 asset 查询 ForeignCoins。

##### 参数

| 名称 | 位置 | 描述 | 必填 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | 是 | string (int64) |
| asset | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.fungible.QueryGetForeignCoinsFromAssetResponse](#zetachainzetacorefungiblequerygetforeigncoinsfromassetresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/fungible/foreign_coins/{index}

#### GET
##### 总结

通过索引查询 ForeignCoins。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | Schema |
| ---- | ---- | ---- | -------- | ------ |
| index | path |  | 是 | string |

##### 响应

| 代码 | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.fungible.QueryGetForeignCoinsResponse](#zetachainzetacorefungiblequerygetforeigncoinsresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/fungible/gas_stability_pool_address

#### GET
##### 摘要

查询指定链上的 gas 稳定性池地址。

##### 响应

| 代码 | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.fungible.QueryGetGasStabilityPoolAddressResponse](#zetachainzetacorefungiblequerygetgasstabilitypooladdressresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/fungible/gas_stability_pool_balance/{chainId}

#### GET
##### 摘要

查询给定链上的 gas 稳定性池余额。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.fungible.QueryGetGasStabilityPoolBalanceResponse](#zetachainzetacorefungiblequerygetgasstabilitypoolbalanceresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/fungible/system_contract

#### GET
##### 概述

查询系统合约

##### 响应

| 状态码 | 描述 | 结构 |
| ---- | ----------- | ------ |
| 200 | 成功响应 | [zetachain.zetacore.fungible.QueryGetSystemContractResponse](#zetachainzetacorefungiblequerygetsystemcontractresponse) |
| default | 意外错误响应 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/lightclient/block_headers

#### GET
***已弃用***
##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 其中之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 其中之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包含可用于分页的总项目数计数（在 UI 中）。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.lightclient.QueryAllBlockHeaderResponse](#zetachainzetacorelightclientqueryallblockheaderresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/lightclient/block_headers/{blockHash}

#### GET
***已弃用***
##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| blockHash | path |  | 是 | byte |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.lightclient.QueryGetBlockHeaderResponse](#zetachainzetacorelightclientquerygetblockheaderresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/lightclient/chain_state

#### GET
***已弃用***
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | No | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | No | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | No | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数的计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | No | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | No | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.lightclient.QueryAllChainStateResponse](#zetachainzetacorelightclientqueryallchainstateresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/lightclient/chain_state/{chainId}

#### GET
***已弃用***
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.lightclient.QueryGetChainStateResponse](#zetachainzetacorelightclientquerygetchainstateresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/lightclient/header_enabled_chains

#### GET
***已弃用***
##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.lightclient.QueryHeaderEnabledChainsResponse](#zetachainzetacorelightclientqueryheaderenabledchainsresponse) |
| default | 意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/lightclient/header_supported_chains

#### GET
***已弃用***
##### 响应

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.lightclient.QueryHeaderSupportedChainsResponse](#zetachainzetacorelightclientqueryheadersupportedchainsresponse) |
| 默认 | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/lightclient/prove

#### GET
***已弃用***
##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | query |  | 否 | string (int64) |
| txHash | query |  | 否 | string |
| proof.ethereumProof.keys | query |  | 否 | [ byte ] |
| proof.ethereumProof.values | query |  | 否 | [ byte ] |
| proof.bitcoinProof.txBytes | query |  | 否 | byte |
| proof.bitcoinProof.path | query |  | 否 | byte |
| proof.bitcoinProof.index | query |  | 否 | long |
| blockHash | query |  | 否 | string |
| txIndex | query |  | 否 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.lightclient.QueryProveResponse](#zetachainzetacorelightclientqueryproveresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/TSS

#### GET
##### 摘要

通过索引查询 TSS。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryGetTSSResponse](#zetachainzetacoreobserverquerygettssresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/ballot_by_identifier/{ballotIdentifier}

#### GET
##### 摘要

查询 VoterByIdentifier 项的列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---- | ---- | ---- | ---- |
| ballotIdentifier | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryBallotByIdentifierResponse](#zetachainzetacoreobserverqueryballotbyidentifierresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/ballot_list_for_height/{height}

#### GET
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| height | path |  | Yes | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryBallotListForHeightResponse](#zetachainzetacoreobserverqueryballotlistforheightresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/ballots

#### GET
##### 摘要

查询所有投票

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是一个在 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryBallotsResponse](#zetachainzetacoreobserverqueryballotsresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/blame_by_chain_and_nonce/{chainId}/{nonce}

#### GET
##### 摘要

查询 VoterByIdentifier 项列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | 是 | string (int64) |
| nonce | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryBlameByChainAndNonceResponse](#zetachainzetacoreobserverqueryblamebychainandnonceresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/blame_by_identifier/{blameIdentifier}

#### GET
##### 摘要

查询 VoterByIdentifier 项的列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| blameIdentifier | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryBlameByIdentifierResponse](#zetachainzetacoreobserverqueryblamebyidentifierresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/chainNonces

#### GET
##### 摘要

查询 chainNonces 项目的列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包括可用于分页的总项目数，在用户界面中显示。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryAllChainNoncesResponse](#zetachainzetacoreobserverqueryallchainnoncesresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/chainNonces/{chainId}

#### GET
##### 总结

通过索引查询 chainNonces。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---- | ---- | ---- | ---- |
| chainId | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryGetChainNoncesResponse](#zetachainzetacoreobserverquerygetchainnoncesresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/crosschain_flags

#### GET
##### 响应

| 代码 | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryGetCrosschainFlagsResponse](#zetachainzetacoreobserverquerygetcrosschainflagsresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/getAllTssFundsMigrators

#### GET
##### 摘要

查询所有 TssFundMigratorInfo

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryTssFundsMigratorInfoAllResponse](#zetachainzetacoreobserverquerytssfundsmigratorinfoallresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/getTssFundsMigrator

#### GET
##### 总结

查询特定链的 TssFundMigratorInfo

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | query |  | 否 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryTssFundsMigratorInfoResponse](#zetachainzetacoreobserverquerytssfundsmigratorinforesponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/get_all_blame_records

#### GET
##### 摘要

查询 VoterByIdentifier 项的列表。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认设置为每个应用所设定的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 表示结果集应包含可用于分页的总项目数计数（在 UI 中）。count_total 仅在使用了 offset 时有效。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自 cosmos-sdk 0.43 起 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryAllBlameRecordsResponse](#zetachainzetacoreobserverqueryallblamerecordsresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/get_chain_params

#### GET
##### 摘要

查询 GetChainParams 项列表。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryGetChainParamsResponse](#zetachainzetacoreobserverquerygetchainparamsresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/get_chain_params_for_chain/{chainId}

#### GET
##### 摘要

查询 GetChainParamsForChain 项的列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryGetChainParamsForChainResponse](#zetachainzetacoreobserverquerygetchainparamsforchainresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/get_tss_address/{bitcoinChainId}

#### GET
##### 摘要

查询 GetTssAddress 项目的列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| bitcoinChainId | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryGetTssAddressResponse](#zetachainzetacoreobserverquerygettssaddressresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/get_tss_address_historical/{finalizedZetaHeight}/{bitcoinChainId}

#### GET
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| finalizedZetaHeight | path |  | 是 | string (int64) |
| bitcoinChainId | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryGetTssAddressByFinalizedHeightResponse](#zetachainzetacoreobserverquerygettssaddressbyfinalizedheightresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/has_voted/{ballotIdentifier}/{voterAddress}

#### GET
##### 摘要

查询投票者是否已为某个投票投票。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| ballotIdentifier | path |  | 是 | string |
| voterAddress | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryHasVotedResponse](#zetachainzetacoreobserverqueryhasvotedresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/keygen

#### GET
##### 摘要

按索引查询 keygen。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | [zetachain.zetacore.observer.QueryGetKeygenResponse](#zetachainzetacoreobserverquerygetkeygenresponse) |
| default | 意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/nodeAccount

#### GET
##### 摘要

查询节点账户项列表。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数，在用户界面中显示。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryAllNodeAccountResponse](#zetachainzetacoreobserverqueryallnodeaccountresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/nodeAccount/{index}

#### GET
##### 总结

通过索引查询 nodeAccount。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| index | path |  | 是 | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryGetNodeAccountResponse](#zetachainzetacoreobserverquerygetnodeaccountresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/observer_set

#### GET
##### 摘要

查询 ObserversByChainAndType 项的列表。

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryObserverSetResponse](#zetachainzetacoreobserverqueryobserversetresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/operationalFlags

#### GET
##### 总结

查询操作标志

##### 响应

| 代码 | 描述 | Schema |
| ---- | ---- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryOperationalFlagsResponse](#zetachainzetacoreobserverqueryoperationalflagsresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/pendingNonces

#### GET
##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，它将默认为由每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项数的计数。count_total 仅在 offset 被使用时有效。当 key 被设置时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryAllPendingNoncesResponse](#zetachainzetacoreobserverqueryallpendingnoncesresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/pendingNonces/{chainId}

#### GET
##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| chainId | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryPendingNoncesByChainResponse](#zetachainzetacoreobserverquerypendingnoncesbychainresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/supportedChains

#### GET
##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QuerySupportedChainsResponse](#zetachainzetacoreobserverquerysupportedchainsresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/observer/tssHistory

#### GET
##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的一个值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，它将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.countTotal | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数的计数。count_total 仅在 offset 使用时被尊重。当 key 被设置时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.observer.QueryTssHistoryResponse](#zetachainzetacoreobserverquerytsshistoryresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/zetacore/fungible/gas_stability_pool_balance

#### GET
##### 摘要

查询所有 gas 稳定性池余额。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [zetachain.zetacore.fungible.QueryAllGasStabilityPoolBalanceResponse](#zetachainzetacorefungiblequeryallgasstabilitypoolbalanceresponse) |
| default | 意外错误响应。 | [google.rpc.Status](#googlerpcstatus) |

### /zeta-chain/zetacore/observer/show_observer_count

#### GET
##### 摘要

查询 ShowObserverCount 项的列表。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 一个成功的响应。 | [zetachain.zetacore.observer.QueryShowObserverCountResponse](#zetachainzetacoreobserverqueryshowobservercountresponse) |
| default | 一个意外的错误响应。 | [google.rpc.Status](#googlerpcstatus) |

---

### /cosmos/base/tendermint/v1beta1/abci_query

#### GET
##### 摘要

ABCIQuery 定义了一个查询处理器，支持直接向应用程序进行 ABCI 查询，完全绕过 Tendermint。ABCI 查询必须包含一个有效且支持的路径，包括 app、custom、p2p 和 store。

##### 描述

自：cosmos-sdk 0.46

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| data | query |  | 否 | byte |
| path | query |  | 否 | string |
| height | query |  | 否 | string (int64) |
| prove | query |  | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | { **"code"**: long, **"log"**: string, **"info"**: string, **"index"**: string (int64), **"key"**: byte, **"value"**: byte, **"proof_ops"**: { **"ops"**: [ { **"type"**: string, **"key"**: byte, **"data"**: byte } ] }, **"height"**: string (int64), **"codespace"**: string } |
| default | 意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/tendermint/v1beta1/blocks/latest

#### GET
##### 摘要

GetLatestBlock 返回最新的区块。

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | { **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"block"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"sdk_block"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: string }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/tendermint/v1beta1/blocks/{height}

#### GET
##### 摘要

GetBlockByHeight 查询给定高度的区块。

##### 参数

| 名称 | 位置 | 描述 | 必需 | Schema |
| ---- | ---------- | ----------- | -------- | ------ |
| height | path |  | 是 | string (int64) |

##### 响应

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"block"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"sdk_block"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: string }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/tendermint/v1beta1/node_info

#### GET
##### 摘要

GetNodeInfo 查询当前节点信息。

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"default_node_info"**: { **"protocol_version"**: { **"p2p"**: string (uint64), **"block"**: string (uint64), **"app"**: string (uint64) }, **"default_node_id"**: string, **"listen_addr"**: string, **"network"**: string, **"version"**: string, **"channels"**: byte, **"moniker"**: string, **"other"**: { **"tx_index"**: string, **"rpc_address"**: string } }, **"application_version"**: { **"name"**: string, **"app_name"**: string, **"version"**: string, **"git_commit"**: string, **"build_tags"**: string, **"go_version"**: string, **"build_deps"**: [ { **"path"**: string, **"version"**: string, **"sum"**: string } ], **"cosmos_sdk_version"**: string } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/tendermint/v1beta1/syncing

#### GET
##### 摘要

GetSyncing 查询节点同步状态。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ------ |
| 200 | 成功的响应。 | { **"syncing"**: boolean } |
| default | 意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/tendermint/v1beta1/validatorsets/latest

#### GET
##### 摘要

GetLatestValidatorSet 查询最新的验证者集。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中返回的结果总数。如果留空，将默认为每个应用程序设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"block_height"**: string (int64), **"validators"**: [ { **"address"**: string, **"pub_key"**: { **"type_url"**: string, **"value"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/tendermint/v1beta1/validatorsets/{height}

#### GET
##### 摘要

GetValidatorSetByHeight 在给定高度查询验证者集。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| height | path |  | 是 | string (int64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 其中之一。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，当 key 不可用时可以使用。它比使用 key 效率低。只能设置 offset 或 key 其中之一。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数，在用户界面中。count_total 仅在使用了 offset 时被尊重。当设置了 key 时，它被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 如果结果要以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | { **"block_height"**: string (int64), **"validators"**: [ { **"address"**: string, **"pub_key"**: { **"type_url"**: string, **"value"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"pagination"**: { **"next_key"**: byte, **"total"**: string (uint64) } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/node/v1beta1/config

#### GET
##### 概述

配置查询用于操作员配置。

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"minimum_gas_price"**: string, **"pruning_keep_recent"**: string, **"pruning_interval"**: string, **"halt_height"**: string (uint64) } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/base/node/v1beta1/status

#### GET
##### 摘要

查询节点状态。

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ---- | ---- |
| 200 | 成功响应。 | { **"earliest_store_height"**: string (uint64), **"height"**: string (uint64), **"timestamp"**: dateTime, **"app_hash"**: byte, **"validator_hash"**: byte } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/decode

#### POST
##### 摘要

TxDecode 解码交易。

##### 描述

自：cosmos-sdk 0.47

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| body | body |  | 是 | { **"tx_bytes"**: byte } |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | [cosmos.tx.v1beta1.TxDecodeResponse](#cosmostxv1beta1txdecoderesponse) |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/decode/amino

#### POST
##### Summary

TxDecodeAmino 将一个 Amino 交易从编码字节解码为 JSON。

##### Description

自 cosmos-sdk 0.47

##### Parameters

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| body | body |  | 是 | { **"amino_binary"**: byte } |

##### Responses

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"amino_json"**: string } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/encode

#### POST
##### 总结

TxEncode 对交易进行编码。

##### 描述

自： cosmos-sdk 0.47

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| body | body |  | 是 | [cosmos.tx.v1beta1.TxEncodeRequest](#cosmostxv1beta1txencoderequest) |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"tx_bytes"**: byte } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/encode/amino

#### POST
##### 摘要

TxEncodeAmino 将 Amino 交易从 JSON 编码为字节。

##### 描述

自：cosmos-sdk 0.47

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| body | body |  | 是 | { **"amino_json"**: string } |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | { **"amino_binary"**: byte } |
| default | 意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/simulate

#### POST
##### 摘要

Simulate 模拟执行交易以估算 gas 使用量。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | Schema |
| ---- | ---------- | ----------- | -------- | ------ |
| body | body |  | 是 | [cosmos.tx.v1beta1.SimulateRequest](#cosmostxv1beta1simulaterequest) |

##### 响应

| 代码 | 描述 | Schema |
| ---- | ----------- | ------ |
| 200 | 一个成功的响应。 | { **"gas_info"**: { **"gas_wanted"**: string (uint64), **"gas_used"**: string (uint64) }, **"result"**: { **"data"**: byte, **"log"**: string, **"events"**: [ { **"type"**: string, **"attributes"**: [ { **"key"**: string, **"value"**: string, **"index"**: boolean } ] } ], **"msg_responses"**: [ { **"type_url"**: string, **"value"**: byte } ] } } |
| default | 一个意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/txs

#### GET
##### 总结

GetTxsEvent 通过事件获取交易。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| events | query | events 是交易事件类型的列表。在 v0.47.x 之后已弃用：使用 query 代替，它应包含一个有效的事件查询。 | 否 | [ string ] |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包含可用于 UI 中分页的总项目数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 时，结果将以降序返回。自：cosmos-sdk 0.43 | 否 | boolean |
| order_by | query |  - ORDER_BY_UNSPECIFIED：ORDER_BY_UNSPECIFIED 指定未知的排序顺序。在这种情况下，OrderBy 默认为 ASC。  - ORDER_BY_ASC：ORDER_BY_ASC 定义升序  - ORDER_BY_DESC：ORDER_BY_DESC 定义降序 | 否 | string |
| page | query | page 是要查询的页码，从 1 开始。如果未提供，将默认为第一页。 | 否 | string (uint64) |
| limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 | string (uint64) |
| query | query | query 定义了交易事件查询，该查询被代理到 Tendermint 的 TxSearch RPC 方法。查询必须有效。自 cosmos-sdk 0.50 | 否 | string |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [cosmos.tx.v1beta1.GetTxsEventResponse](#cosmostxv1beta1gettxseventresponse) |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

#### POST
##### 总结

BroadcastTx 广播交易。

##### 参数

| 名称 | 位置 | 描述 | 必需 | 架构 |
| ---- | ---------- | ----------- | -------- | ------ |
| body | body |  | 是 | { **"tx_bytes"**: byte, **"mode"**: string } |

##### 响应

| 代码 | 描述 | 架构 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | { **"tx_response"**: { **"height"**: string (int64), **"txhash"**: string, **"codespace"**: string, **"code"**: long, **"data"**: string, **"raw_log"**: string, **"logs"**: [ { **"msg_index"**: long, **"log"**: string, **"events"**: [ { **"type"**: string, **"attributes"**: [ { **"key"**: string, **"value"**: string } ] } ] } ], **"info"**: string, **"gas_wanted"**: string (int64), **"gas_used"**: string (int64), **"tx"**: { **"type_url"**: string, **"value"**: byte }, **"timestamp"**: string, **"events"**: [ { **"type"**: string, **"attributes"**: [ { **"key"**: string, **"value"**: string, **"index"**: boolean } ] } ] } } |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/txs/block/{height}

#### GET
##### 摘要

GetBlockWithTxs 获取一个包含解码交易的区块。

##### 描述

自： cosmos-sdk 0.45.2

##### 参数

| 名称 | 位置 | 描述 | 必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| height | path | height 是要查询的区块高度。 | 是 | string (int64) |
| pagination.key | query | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 中的一个。 | 否 | byte |
| pagination.offset | query | offset 是一个数字偏移量，在 key 不可用时使用。它的效率低于使用 key。只能设置 offset 或 key 中的一个。 | 否 | string (uint64) |
| pagination.limit | query | limit 是结果页面中要返回的结果总数。如果留空，将默认为由每个应用设置的值。 | 否 | string (uint64) |
| pagination.count_total | query | count_total 设置为 true 以指示结果集应包括可用于分页的总项目数计数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它会被忽略。 | 否 | boolean |
| pagination.reverse | query | reverse 设置为 true 表示结果按降序返回。自： cosmos-sdk 0.43 | 否 | boolean |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功响应。 | [cosmos.tx.v1beta1.GetBlockWithTxsResponse](#cosmostxv1beta1getblockwithtxsresponse) |
| default | 意外错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

### /cosmos/tx/v1beta1/txs/{hash}

#### GET
##### 摘要

GetTx 通过哈希获取一个 tx。

##### 参数

| 名称 | 位置 | 描述 | 是否必需 | 模式 |
| ---- | ---------- | ----------- | -------- | ------ |
| hash | path | hash 是要查询的 tx 哈希，以十六进制字符串编码。 | Yes | string |

##### 响应

| 代码 | 描述 | 模式 |
| ---- | ----------- | ------ |
| 200 | 成功的响应。 | [cosmos.tx.v1beta1.GetTxResponse](#cosmostxv1beta1gettxresponse) |
| default | 意外的错误响应。 | { **"error"**: string, **"code"**: integer, **"message"**: string, **"details"**: [ { **"type_url"**: string, **"value"**: byte } ] } |

---

### 模型

#### cosmos.auth.v1beta1.AddressBytesToStringResponse

AddressBytesToStringResponse 是 AddressString rpc 方法的响应类型。
自：cosmos-sdk 0.46

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| address_string | string |  | 否 |

#### cosmos.auth.v1beta1.AddressStringToBytesResponse

AddressStringToBytesResponse 是 AddressBytes rpc 方法的响应类型。
自：cosmos-sdk 0.46

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| address_bytes | byte |  | 否 |

#### cosmos.auth.v1beta1.BaseAccount

BaseAccount 定义了一个基础账户类型。它包含了基本账户功能所需的所有必要字段。任何自定义账户类型都应扩展此类型以获取额外功能（例如归属）。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| address | string |  | 否 |
| pub_key | { **"type_url"**: string, **"value"**: byte } | `Any` 包含一个任意序列化的协议缓冲区消息以及一个描述序列化消息类型的 URL。Protobuf 库提供了以实用函数或 Any 类型的额外生成方法的形式来打包/解包 Any 值的支持。示例 1：在 C++ 中打包和解包消息。      Foo foo = ...;     Any any;     any.PackFrom(foo);     ...     if (any.UnpackTo(&foo)) {       ...     } 示例 2：在 Java 中打包和解包消息。      Foo foo = ...;     Any any = Any.pack(foo);     ...     if (any.is(Foo.class)) {       foo = any.unpack(Foo.class);     }     // 或 ...     if (any.isSameTypeAs(Foo.getDefaultInstance())) {       foo = any.unpack(Foo.getDefaultInstance());     } 示例 3：在 Python 中打包和解包消息。      foo = Foo(...)     any = Any()     any.Pack(foo)     ...     if any.Is(Foo.DESCRIPTOR):       any.Unpack(foo)       ... 示例 4：在 Go 中打包和解包消息。       foo := &pb.Foo{...}      any, err := anypb.New(foo)      if err != nil {        ...      }      ...      foo := &pb.Foo{}      if err := any.UnmarshalTo(foo); err != nil {        ...      } Protobuf 库提供的打包方法默认使用 'type.googleapis.com/full.type.name' 作为类型 URL，解包方法仅使用类型 URL 中最后一个 '/' 之后的完全限定类型名称，例如 "foo.bar.com/x/y.z" 将产生类型名称 "y.z"。JSON `Any` 值的 JSON 表示使用反序列化的嵌入消息的常规表示，并带有一个额外的字段 `@type`，其中包含类型 URL。示例：      package google.profile;     message Person {       string first_name = 1;       string last_name = 2;     }      {       "@type": "type.googleapis.com/google.profile.Person",       "firstName": <string>,       "lastName": <string>     } 如果嵌入的消息类型是众所周知的并且具有自定义 JSON 表示，则该表示将被嵌入，添加一个字段 `value`，该字段保存自定义 JSON，此外还有 `@type` 字段。示例（对于消息 [google.protobuf.Duration][]）：      {       "@type": "type.googleapis.com/google.protobuf.Duration",       "value": "1.212s"     } | 否 |
| account_number | string (uint64) |  | 否 |
| sequence | string (uint64) |  | 否 |

#### cosmos.auth.v1beta1.Bech32PrefixResponse

Bech32PrefixResponse 是 Bech32Prefix rpc 方法的响应类型。

自：cosmos-sdk 0.46

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| bech32_prefix | string |  | 否 |

#### cosmos.auth.v1beta1.Params

Params 定义了 auth 模块的参数。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| max_memo_characters | string (uint64) |  | 否 |
| tx_sig_limit | string (uint64) |  | 否 |
| tx_size_cost_per_byte | string (uint64) |  | 否 |
| sig_verify_cost_ed25519 | string (uint64) |  | 否 |
| sig_verify_cost_secp256k1 | string (uint64) |  | 否 |

#### cosmos.auth.v1beta1.QueryAccountAddressByIDResponse

自：cosmos-sdk 0.46.2

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| account_address | string |  | 否 |

#### cosmos.auth.v1beta1.QueryAccountInfoResponse

QueryAccountInfoResponse 是 Query/AccountInfo 的响应类型。

自：cosmos-sdk 0.47

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| info | { **"address"**: string, **"pub_key"**: { **"type_url"**: string, **"value"**: byte }, **"account_number"**: string (uint64), **"sequence"**: string (uint64) } | info 是由 BaseAccount 表示的账户信息。 | 否 |

#### cosmos.auth.v1beta1.QueryAccountResponse

QueryAccountResponse 是 Query/Account RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| account | { **"type_url"**: string, **"value"**: byte } | `Any` 包含一个任意序列化的协议缓冲区消息以及一个描述序列化消息类型的 URL。Protobuf 库提供了以实用函数或 Any 类型的额外生成方法的形式来打包/解包 Any 值的支持。示例 1：在 C++ 中打包和解包消息。      Foo foo = ...;     Any any;     any.PackFrom(foo);     ...     if (any.UnpackTo(&foo)) {       ...     } 示例 2：在 Java 中打包和解包消息。      Foo foo = ...;     Any any = Any.pack(foo);     ...     if (any.is(Foo.class)) {       foo = any.unpack(Foo.class);     }     // 或 ...     if (any.isSameTypeAs(Foo.getDefaultInstance())) {       foo = any.unpack(Foo.getDefaultInstance());     } 示例 3：在 Python 中打包和解包消息。      foo = Foo(...)     any = Any()     any.Pack(foo)     ...     if any.Is(Foo.DESCRIPTOR):       any.Unpack(foo)       ... 示例 4：在 Go 中打包和解包消息。       foo := &pb.Foo{...}      any, err := anypb.New(foo)      if err != nil {        ...      }      ...      foo := &pb.Foo{}      if err := any.UnmarshalTo(foo); err != nil {        ...      } Protobuf 库提供的打包方法默认使用 'type.googleapis.com/full.type.name' 作为类型 URL，解包方法仅使用类型 URL 中最后一个 '/' 之后的完全限定类型名称，例如 "foo.bar.com/x/y.z" 将产生类型名称 "y.z"。JSON `Any` 值的 JSON 表示使用反序列化的嵌入消息的常规表示，并带有一个额外的字段 `@type`，其中包含类型 URL。示例：      package google.profile;     message Person {       string first_name = 1;       string last_name = 2;     }      {       "@type": "type.googleapis.com/google.profile.Person",       "firstName": <string>,       "lastName": <string>     } 如果嵌入的消息类型是众所周知的并且具有自定义 JSON 表示，则该表示将被嵌入，添加一个字段 `value`，该字段保存自定义 JSON，此外还有 `@type` 字段。示例（对于消息 [google.protobuf.Duration][]）：      {       "@type": "type.googleapis.com/google.protobuf.Duration",       "value": "1.212s"     } | 否 |

#### cosmos.auth.v1beta1.QueryAccountsResponse

QueryAccountsResponse 是 Query/Accounts RPC 方法的响应类型。
自：cosmos-sdk 0.43

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| accounts | [ { **"type_url"**: string, **"value"**: byte } ] |  | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.auth.v1beta1.QueryModuleAccountByNameResponse

QueryModuleAccountByNameResponse 是 Query/ModuleAccountByName RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| account | { **"type_url"**: string, **"value"**: byte } | `Any` 包含一个任意序列化的协议缓冲区消息以及一个描述序列化消息类型的 URL。Protobuf 库提供了以实用函数或 Any 类型的额外生成方法的形式来打包/解包 Any 值的支持。示例 1：在 C++ 中打包和解包消息。      Foo foo = ...;     Any any;     any.PackFrom(foo);     ...     if (any.UnpackTo(&foo)) {       ...     } 示例 2：在 Java 中打包和解包消息。      Foo foo = ...;     Any any = Any.pack(foo);     ...     if (any.is(Foo.class)) {       foo = any.unpack(Foo.class);     }     // 或 ...     if (any.isSameTypeAs(Foo.getDefaultInstance())) {       foo = any.unpack(Foo.getDefaultInstance());     } 示例 3：在 Python 中打包和解包消息。      foo = Foo(...)     any = Any()     any.Pack(foo)     ...     if any.Is(Foo.DESCRIPTOR):       any.Unpack(foo)       ... 示例 4：在 Go 中打包和解包消息。       foo := &pb.Foo{...}      any, err := anypb.New(foo)      if err != nil {        ...      }      ...      foo := &pb.Foo{}      if err := any.UnmarshalTo(foo); err != nil {        ...      } Protobuf 库提供的打包方法默认使用 'type.googleapis.com/full.type.name' 作为类型 URL，解包方法仅使用类型 URL 中最后一个 '/' 之后的完全限定类型名称，例如 "foo.bar.com/x/y.z" 将产生类型名称 "y.z"。JSON `Any` 值的 JSON 表示使用反序列化的嵌入消息的常规表示，并带有一个额外的字段 `@type`，其中包含类型 URL。示例：      package google.profile;     message Person {       string first_name = 1;       string last_name = 2;     }      {       "@type": "type.googleapis.com/google.profile.Person",       "firstName": <string>,       "lastName": <string>     } 如果嵌入的消息类型是众所周知的并且具有自定义 JSON 表示，则该表示将被嵌入，添加一个字段 `value`，该字段保存自定义 JSON，此外还有 `@type` 字段。示例（对于消息 [google.protobuf.Duration][]）：      {       "@type": "type.googleapis.com/google.protobuf.Duration",       "value": "1.212s"     } | 否 |

#### cosmos.auth.v1beta1.QueryModuleAccountsResponse

QueryModuleAccountsResponse 是 Query/ModuleAccounts RPC 方法的响应类型。
自：cosmos-sdk 0.46

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| accounts | [ { **"type_url"**: string, **"value"**: byte } ] |  | 否 |

#### cosmos.auth.v1beta1.QueryParamsResponse

QueryParamsResponse 是 Query/Params RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| params | { **"max_memo_characters"**: string (uint64), **"tx_sig_limit"**: string (uint64), **"tx_size_cost_per_byte"**: string (uint64), **"sig_verify_cost_ed25519"**: string (uint64), **"sig_verify_cost_secp256k1"**: string (uint64) } | params 定义了模块的参数。 | 否 |

#### cosmos.base.query.v1beta1.PageRequest

message SomeRequest {
         Foo some_parameter = 1;
         PageRequest pagination = 2;
 }

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| key | byte | key 是 PageResponse.next_key 中返回的值，用于最有效地开始查询下一页。只能设置 offset 或 key 之一。 | 否 |
| offset | string (uint64) | offset 是一个数字偏移量，在 key 不可用时使用。它比使用 key 效率低。只能设置 offset 或 key 之一。 | 否 |
| limit | string (uint64) | limit 是结果页面中要返回的结果总数。如果留空，将默认为每个应用设置的值。 | 否 |
| count_total | boolean | count_total 设置为 true 以指示结果集应包括可用于 UI 中分页的项目总数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 |
| reverse | boolean | reverse 设置为 true 表示结果应按降序返回。自：cosmos-sdk 0.43 | 否 |
| countTotal | boolean | count_total 设置为 true 以指示结果集应包括可用于 UI 中分页的项目总数。count_total 仅在使用了 offset 时被遵守。当设置了 key 时，它被忽略。 | 否 |

#### cosmos.base.query.v1beta1.PageResponse

PageResponse 将嵌入到 gRPC 响应消息中，其中相应的请求消息使用了 PageRequest。

 message SomeResponse {
         repeated Bar results = 1;
         PageResponse page = 2;
 }

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| next_key | byte | next_key 是要传递给 PageRequest.key 以最有效地查询下一页的键。如果没有更多结果，它将为空。 | 否 |
| total | string (uint64) |  | 否 |
| nextKey | byte | next_key 是要传递给 PageRequest.key 以最有效地查询下一页的键。如果没有更多结果，它将为空。 | 否 |

#### google.protobuf.Any

`Any` 包含一个任意序列化的协议缓冲区消息以及一个
描述序列化消息类型的 URL。
Protobuf 库提供了以实用函数或 Any 类型的额外生成方法的形式
来打包/解包 Any 值的支持。
示例 1：在 C++ 中打包和解包消息。

    Foo foo = ...;
    Any any;
    any.PackFrom(foo);
    ...
    if (any.UnpackTo(&foo)) {
      ...
    }

示例 2：在 Java 中打包和解包消息。

    Foo foo = ...;
    Any any = Any.pack(foo);
    ...
    if (any.is(Foo.class)) {
      foo = any.unpack(Foo.class);
    }
    // 或 ...
    if (any.isSameTypeAs(Foo.getDefaultInstance())) {
      foo = any.unpack(Foo.getDefaultInstance());
    }

示例 3：在 Python 中打包和解包消息。

    foo = Foo(...)
    any = Any()
    any.Pack(foo)
    ...
    if any.Is(Foo.DESCRIPTOR):
      any.Unpack(foo)
      ...

示例 4：在 Go 中打包和解包消息

     foo := &pb.Foo{...}
     any, err := anypb.New(foo)
     if err != nil {
       ...
     }
     ...
     foo := &pb.Foo{}
     if err := any.UnmarshalTo(foo); err != nil {
       ...
     }

Protobuf 库提供的打包方法默认使用
'type.googleapis.com/full.type.name' 作为类型 URL，解包
方法仅使用类型 URL 中最后一个 '/'
之后的完全限定类型名称，例如 "foo.bar.com/x/y.z" 将产生类型
名称 "y.z"。
JSON
`Any` 值的 JSON 表示使用反序列化的
嵌入消息的常规表示，并带有一个
额外的字段 `@type`，其中包含类型 URL。示例：

    package google.profile;
    message Person {
      string first_name = 1;
      string last_name = 2;
    }

    {
      "@type": "type.googleapis.com/google.profile.Person",
      "firstName": <string>,
      "lastName": <string>
    }

如果嵌入的消息类型是众所周知的并且具有自定义 JSON
表示，则该表示将被嵌入，添加一个字段
`value`，该字段保存自定义 JSON，此外还有 `@type`
字段。示例（对于消息 [google.protobuf.Duration][])：

    {
      "@type": "type.googleapis.com/google.protobuf.Duration",
      "value": "1.212s"
    }

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| type_url | string | 一个 URL/资源名称，唯一标识序列化协议缓冲区消息的类型。此字符串必须包含至少一个 "/" 字符。URL 路径的最后一个段必须表示类型的完全限定名称（如 `path/google.protobuf.Duration`）。名称应采用规范形式（例如，不接受前导 "."）。在实践中，团队通常预编译二进制文件中他们期望在 Any 上下文中使用的所有类型。但是，对于使用 `http`、`https` 或无方案的 URL，可以选择设置一个类型服务器，将类型 URL 映射到消息定义，如下所示： * 如果未提供方案，则假定为 `https`。 * 对 URL 的 HTTP GET 必须产生一个 [google.protobuf.Type][]   二进制格式的值，或产生错误。 * 允许应用程序基于 URL 缓存查找结果，   或将其预编译到二进制文件中以避免任何查找。因此，在类型更改时需要保持二进制兼容性   （使用版本化的类型名称来管理破坏性更改）。  注意：此功能目前在官方 protobuf 版本中不可用，并且不用于以 type.googleapis.com 开头的类型 URL。除 `http`、`https`（或空方案）之外的方案可能用于具有实现特定语义的情况。 | 否 |
| value | byte | 必须是上述指定类型的有效序列化协议缓冲区。 | 否 |
| @type | string |  | 否 |

#### grpc.gateway.runtime.Error

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| error | string |  | 否 |
| code | integer |  | 否 |
| message | string |  | 否 |
| details | [ { **"type_url"**: string, **"value"**: byte } ] |  | 否 |

#### cosmos.bank.v1beta1.DenomOwner

DenomOwner 定义了表示拥有或持有特定面额代币的账户的结构。它包含该面额代币的账户地址和账户余额。

自：cosmos-sdk 0.46

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| address | string | address 定义了拥有特定面额的地址。 | 否 |
| balance | { **"denom"**: string, **"amount"**: string } | Coin 定义了一个具有面额和数量的代币。  注意：amount 字段是一个实现了 gogoproto 所需自定义方法签名的 Int。 | 否 |

#### cosmos.bank.v1beta1.DenomUnit

DenomUnit 表示描述基本代币的给定面额单元的结构。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| denom | string | denom 表示给定面额单元的字符串名称（例如 uatom）。 | 否 |
| exponent | long | exponent 表示必须将 base_denom 提高到的 10 的幂指数，以等于给定 DenomUnit 的 denom 1 denom = 10^exponent base_denom（例如，对于 base_denom 为 uatom，可以创建一个 exponent = 6 的 'atom' DenomUnit，因此：1 atom = 10^6 uatom）。 | 否 |
| aliases | [ string ] |  | 否 |

#### cosmos.bank.v1beta1.Metadata

Metadata 表示描述基本代币的结构。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| description | string |  | 否 |
| denom_units | [ { **"denom"**: string, **"exponent"**: long, **"aliases"**: [ string ] } ] |  | 否 |
| base | string | base 表示基础面额（应为 exponent = 0 的 DenomUnit）。 | 否 |
| display | string | display 指示建议在客户端中显示的面额。 | 否 |
| name | string | 自：cosmos-sdk 0.43 | 否 |
| symbol | string | symbol 是通常在交易所显示的代币符号（例如：ATOM）。这可能与 display 相同。自：cosmos-sdk 0.43 | 否 |
| uri | string | URI 指向包含附加信息的文档（链上或链下）。可选。自：cosmos-sdk 0.46 | 否 |
| uri_hash | string | URIHash 是指向 URI 的文档的 sha256 哈希。用于验证文档是否未更改。可选。自：cosmos-sdk 0.46 | 否 |

#### cosmos.bank.v1beta1.Params

Params 定义了 bank 模块的参数。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| send_enabled | [ { **"denom"**: string, **"enabled"**: boolean } ] | 已弃用：在 params 中使用 SendEnabled 已弃用。对于创世，使用创世对象中新添加的 send_enabled 字段。此信息的存储、查找和操作现在在 keeper 中。自 cosmos-sdk 0.47 起，此字段仅用于创世文件的向后兼容性。 | 否 |
| default_send_enabled | boolean |  | 否 |

#### cosmos.bank.v1beta1.QueryAllBalancesResponse

QueryAllBalancesResponse 是 Query/AllBalances RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| balances | [ { **"denom"**: string, **"amount"**: string } ] | balances 是所有代币的余额。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.bank.v1beta1.QueryBalanceResponse

QueryBalanceResponse 是 Query/Balance RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| balance | { **"denom"**: string, **"amount"**: string } | Coin 定义了一个具有面额和数量的代币。  注意：amount 字段是一个实现了 gogoproto 所需自定义方法签名的 Int。 | 否 |

#### cosmos.bank.v1beta1.QueryDenomMetadataByQueryStringResponse

QueryDenomMetadataByQueryStringResponse 是 Query/DenomMetadata RPC 方法的响应类型。与 QueryDenomMetadataResponse 相同，但在请求中以查询字符串形式接收 denom。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| metadata | { **"description"**: string, **"denom_units"**: [ { **"denom"**: string, **"exponent"**: long, **"aliases"**: [ string ] } ], **"base"**: string, **"display"**: string, **"name"**: string, **"symbol"**: string, **"uri"**: string, **"uri_hash"**: string } | Metadata 表示描述基本代币的结构。 | 否 |

#### cosmos.bank.v1beta1.QueryDenomMetadataResponse

QueryDenomMetadataResponse 是 Query/DenomMetadata RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| metadata | { **"description"**: string, **"denom_units"**: [ { **"denom"**: string, **"exponent"**: long, **"aliases"**: [ string ] } ], **"base"**: string, **"display"**: string, **"name"**: string, **"symbol"**: string, **"uri"**: string, **"uri_hash"**: string } | Metadata 表示描述基本代币的结构。 | 否 |

#### cosmos.bank.v1beta1.QueryDenomOwnersByQueryResponse

QueryDenomOwnersByQueryResponse 定义了 DenomOwnersByQuery RPC 查询的 RPC 响应类型。
自：cosmos-sdk 0.50.3

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| denom_owners | [ { **"address"**: string, **"balance"**: { **"denom"**: string, **"amount"**: string } } ] |  | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.bank.v1beta1.QueryDenomOwnersResponse

QueryDenomOwnersResponse 定义了 DenomOwners RPC 查询的 RPC 响应类型。
自：cosmos-sdk 0.46

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| denom_owners | [ { **"address"**: string, **"balance"**: { **"denom"**: string, **"amount"**: string } } ] |  | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.bank.v1beta1.QueryDenomsMetadataResponse

QueryDenomsMetadataResponse 是 Query/DenomsMetadata RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| metadatas | [ { **"description"**: string, **"denom_units"**: [ { **"denom"**: string, **"exponent"**: long, **"aliases"**: [ string ] } ], **"base"**: string, **"display"**: string, **"name"**: string, **"symbol"**: string, **"uri"**: string, **"uri_hash"**: string } ] | metadata 提供所有注册代币的客户端信息。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.bank.v1beta1.QueryParamsResponse

QueryParamsResponse 定义了查询 x/bank 参数的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| params | { **"send_enabled"**: [ { **"denom"**: string, **"enabled"**: boolean } ], **"default_send_enabled"**: boolean } | params 提供 bank 模块的参数。 | 否 |

#### cosmos.bank.v1beta1.QuerySendEnabledResponse

QuerySendEnabledResponse 定义了 SendEnable 查询的 RPC 响应类型。

自：cosmos-sdk 0.47

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| send_enabled | [ { **"denom"**: string, **"enabled"**: boolean } ] |  | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。仅当请求中的 denoms 字段为空时，才会填充此字段。 | 否 |

#### cosmos.bank.v1beta1.QuerySpendableBalanceByDenomResponse

QuerySpendableBalanceByDenomResponse 定义了查询账户特定面额可花费余额的 gRPC 响应结构。
自：cosmos-sdk 0.47

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| balance | { **"denom"**: string, **"amount"**: string } | Coin 定义了一个具有面额和数量的代币。  注意：amount 字段是一个实现了 gogoproto 所需自定义方法签名的 Int。 | 否 |

#### cosmos.bank.v1beta1.QuerySpendableBalancesResponse

QuerySpendableBalancesResponse 定义了查询账户可花费余额的 gRPC 响应结构。
自：cosmos-sdk 0.46

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| balances | [ { **"denom"**: string, **"amount"**: string } ] | balances 是所有代币的可花费余额。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.bank.v1beta1.QuerySupplyOfResponse

QuerySupplyOfResponse 是 Query/SupplyOf RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| amount | { **"denom"**: string, **"amount"**: string } | Coin 定义了一个具有面额和数量的代币。  注意：amount 字段是一个实现了 gogoproto 所需自定义方法签名的 Int。 | 否 |

#### cosmos.bank.v1beta1.QueryTotalSupplyResponse

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| supply | [ { **"denom"**: string, **"amount"**: string } ] |  | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。  自：cosmos-sdk 0.43 | 否 |

#### cosmos.bank.v1beta1.SendEnabled

SendEnabled 将代币面额映射到 send_enabled 状态（面额是否可发送）。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| denom | string |  | 否 |
| enabled | boolean |  | 否 |

#### cosmos.base.v1beta1.Coin

Coin 定义了一个具有面额和数量的代币。

注意：amount 字段是一个实现了 gogoproto 所需自定义方法
签名的 Int。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| denom | string |  | 否 |
| amount | string |  | 否 |

#### cosmos.base.tendermint.v1beta1.ABCIQueryResponse

ABCIQueryResponse 定义了 ABCIQuery gRPC 查询的响应结构。
注意：此类型是 Tendermint 中定义的 ResponseQuery proto 类型的重复。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| code | long |  | 否 |
| log | string |  | 否 |
| info | string |  | 否 |
| index | string (int64) |  | 否 |
| key | byte |  | 否 |
| value | byte |  | 否 |
| proof_ops | { **"ops"**: [ { **"type"**: string, **"key"**: byte, **"data"**: byte } ] } | ProofOps 是由 ProofOps 列表定义的默克尔证明。注意：此类型是 Tendermint 中定义的 ProofOps proto 类型的重复。 | 否 |
| height | string (int64) |  | 否 |
| codespace | string |  | 否 |

#### cosmos.base.tendermint.v1beta1.Block

Block 是 tendermint 类型 Block，其中 Header 提议者地址字段转换为 bech32 字符串。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| header | { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: string } | Header 定义了 Tendermint 区块头的结构。 | 否 |
| data | { **"txs"**: [ byte ] } |  | 否 |
| evidence | { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] } |  | 否 |
| last_commit | { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } | Commit 包含一组验证者已提交区块的证据。 | 否 |

#### cosmos.base.tendermint.v1beta1.GetBlockByHeightResponse

GetBlockByHeightResponse 是 Query/GetBlockByHeight RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| block_id | { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } } |  | 否 |
| block | { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } } |  | 否 |
| sdk_block | { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: string }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } } | Block 是 tendermint 类型 Block，其中 Header 提议者地址字段转换为 bech32 字符串。 | 否 |

#### cosmos.base.tendermint.v1beta1.GetLatestBlockResponse

GetLatestBlockResponse 是 Query/GetLatestBlock RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| block_id | { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } } |  | 否 |
| block | { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } } |  | 否 |
| sdk_block | { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: string }, **"data"**: { **"txs"**: [ byte ] }, **"evidence"**: { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] }, **"last_commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } } | Block 是 tendermint 类型 Block，其中 Header 提议者地址字段转换为 bech32 字符串。 | 否 |

#### cosmos.base.tendermint.v1beta1.GetLatestValidatorSetResponse

GetLatestValidatorSetResponse 是 Query/GetValidatorSetByHeight RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| block_height | string (int64) |  | 否 |
| validators | [ { **"address"**: string, **"pub_key"**: { **"type_url"**: string, **"value"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ] |  | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.base.tendermint.v1beta1.GetNodeInfoResponse

GetNodeInfoResponse 是 Query/GetNodeInfo RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| default_node_info | { **"protocol_version"**: { **"p2p"**: string (uint64), **"block"**: string (uint64), **"app"**: string (uint64) }, **"default_node_id"**: string, **"listen_addr"**: string, **"network"**: string, **"version"**: string, **"channels"**: byte, **"moniker"**: string, **"other"**: { **"tx_index"**: string, **"rpc_address"**: string } } |  | 否 |
| application_version | { **"name"**: string, **"app_name"**: string, **"version"**: string, **"git_commit"**: string, **"build_tags"**: string, **"go_version"**: string, **"build_deps"**: [ { **"path"**: string, **"version"**: string, **"sum"**: string } ], **"cosmos_sdk_version"**: string } | VersionInfo 是 GetNodeInfoResponse 消息的类型。 | 否 |

#### cosmos.base.tendermint.v1beta1.GetSyncingResponse

GetSyncingResponse 是 Query/GetSyncing RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| syncing | boolean |  | 否 |

#### cosmos.base.tendermint.v1beta1.GetValidatorSetByHeightResponse

GetValidatorSetByHeightResponse 是 Query/GetValidatorSetByHeight RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| block_height | string (int64) |  | 否 |
| validators | [ { **"address"**: string, **"pub_key"**: { **"type_url"**: string, **"value"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ] |  | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.base.tendermint.v1beta1.Header

Header 定义了 Tendermint 区块头的结构。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| version | { **"block"**: string (uint64), **"app"**: string (uint64) } | Consensus 捕获了处理区块链中区块的共识规则，包括所有区块链数据结构和应用程序状态转换机的规则。 | 否 |
| chain_id | string |  | 否 |
| height | string (int64) |  | 否 |
| time | dateTime |  | 否 |
| last_block_id | { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } } |  | 否 |
| last_commit_hash | byte |  | 否 |
| data_hash | byte |  | 否 |
| validators_hash | byte |  | 否 |
| next_validators_hash | byte |  | 否 |
| consensus_hash | byte |  | 否 |
| app_hash | byte |  | 否 |
| last_results_hash | byte |  | 否 |
| evidence_hash | byte |  | 否 |
| proposer_address | string | proposer_address 是原始区块提议者地址，格式化为 Bech32 字符串。在 Tendermint 中，此类型是 `bytes`，但在 SDK 中，我们将其转换为 Bech32 字符串以获得更好的用户体验。 | 否 |

#### cosmos.base.tendermint.v1beta1.Module

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| path | string |  | 否 |
| version | string |  | 否 |
| sum | string |  | 否 |

#### cosmos.base.tendermint.v1beta1.ProofOp

ProofOp 定义了用于计算默克尔根的操作。数据可以是任意格式，提供必要的数据，例如相邻节点哈希。
注意：此类型是 Tendermint 中定义的 ProofOp proto 类型的重复。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| type | string |  | 否 |
| key | byte |  | 否 |
| data | byte |  | 否 |

#### cosmos.base.tendermint.v1beta1.ProofOps

ProofOps 是由 ProofOps 列表定义的默克尔证明。
注意：此类型是 Tendermint 中定义的 ProofOps proto 类型的重复。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| ops | [ { **"type"**: string, **"key"**: byte, **"data"**: byte } ] |  | 否 |

#### cosmos.base.tendermint.v1beta1.Validator

Validator 是验证者集的类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| address | string |  | 否 |
| pub_key | { **"type_url"**: string, **"value"**: byte } | `Any` 包含一个任意序列化的协议缓冲区消息以及一个描述序列化消息类型的 URL。Protobuf 库提供了以实用函数或 Any 类型的额外生成方法的形式来打包/解包 Any 值的支持。示例 1：在 C++ 中打包和解包消息。      Foo foo = ...;     Any any;     any.PackFrom(foo);     ...     if (any.UnpackTo(&foo)) {       ...     } 示例 2：在 Java 中打包和解包消息。      Foo foo = ...;     Any any = Any.pack(foo);     ...     if (any.is(Foo.class)) {       foo = any.unpack(Foo.class);     }     // 或 ...     if (any.isSameTypeAs(Foo.getDefaultInstance())) {       foo = any.unpack(Foo.getDefaultInstance());     } 示例 3：在 Python 中打包和解包消息。      foo = Foo(...)     any = Any()     any.Pack(foo)     ...     if any.Is(Foo.DESCRIPTOR):       any.Unpack(foo)       ... 示例 4：在 Go 中打包和解包消息。       foo := &pb.Foo{...}      any, err := anypb.New(foo)      if err != nil {        ...      }      ...      foo := &pb.Foo{}      if err := any.UnmarshalTo(foo); err != nil {        ...      } Protobuf 库提供的打包方法默认使用 'type.googleapis.com/full.type.name' 作为类型 URL，解包方法仅使用类型 URL 中最后一个 '/' 之后的完全限定类型名称，例如 "foo.bar.com/x/y.z" 将产生类型名称 "y.z"。JSON `Any` 值的 JSON 表示使用反序列化的嵌入消息的常规表示，并带有一个额外的字段 `@type`，其中包含类型 URL。示例：      package google.profile;     message Person {       string first_name = 1;       string last_name = 2;     }      {       "@type": "type.googleapis.com/google.profile.Person",       "firstName": <string>,       "lastName": <string>     } 如果嵌入的消息类型是众所周知的并且具有自定义 JSON 表示，则该表示将被嵌入，添加一个字段 `value`，该字段保存自定义 JSON，此外还有 `@type` 字段。示例（对于消息 [google.protobuf.Duration][]）：      {       "@type": "type.googleapis.com/google.protobuf.Duration",       "value": "1.212s"     } | 否 |
| voting_power | string (int64) |  | 否 |
| proposer_priority | string (int64) |  | 否 |

#### cosmos.base.tendermint.v1beta1.VersionInfo

VersionInfo 是 GetNodeInfoResponse 消息的类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| name | string |  | 否 |
| app_name | string |  | 否 |
| version | string |  | 否 |
| git_commit | string |  | 否 |
| build_tags | string |  | 否 |
| go_version | string |  | 否 |
| build_deps | [ { **"path"**: string, **"version"**: string, **"sum"**: string } ] |  | 否 |
| cosmos_sdk_version | string |  | 否 |

#### tendermint.crypto.PublicKey

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| ed25519 | byte |  | 否 |
| secp256k1 | byte |  | 否 |

#### tendermint.p2p.DefaultNodeInfo

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| protocol_version | { **"p2p"**: string (uint64), **"block"**: string (uint64), **"app"**: string (uint64) } |  | 否 |
| default_node_id | string |  | 否 |
| listen_addr | string |  | 否 |
| network | string |  | 否 |
| version | string |  | 否 |
| channels | byte |  | 否 |
| moniker | string |  | 否 |
| other | { **"tx_index"**: string, **"rpc_address"**: string } |  | 否 |

#### tendermint.p2p.DefaultNodeInfoOther

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| tx_index | string |  | 否 |
| rpc_address | string |  | 否 |

#### tendermint.p2p.ProtocolVersion

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| p2p | string (uint64) |  | 否 |
| block | string (uint64) |  | 否 |
| app | string (uint64) |  | 否 |

#### tendermint.types.Block

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| header | { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte } | Header 定义了区块头的结构。 | 否 |
| data | { **"txs"**: [ byte ] } |  | 否 |
| evidence | { **"evidence"**: [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] } |  | 否 |
| last_commit | { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } | Commit 包含一组验证者已提交区块的证据。 | 否 |

#### tendermint.types.BlockID

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| hash | byte |  | 否 |
| part_set_header | { **"total"**: long, **"hash"**: byte } |  | 否 |

#### tendermint.types.BlockIDFlag

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| tendermint.types.BlockIDFlag | string |  |  |

#### tendermint.types.Commit

Commit 包含一组验证者已提交区块的证据。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| height | string (int64) |  | 否 |
| round | integer |  | 否 |
| block_id | { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } } |  | 否 |
| signatures | [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] |  | 否 |

#### tendermint.types.CommitSig

CommitSig 是包含在 Commit 中的投票的一部分。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| block_id_flag | string | *枚举:* `"BLOCK_ID_FLAG_UNKNOWN"`, `"BLOCK_ID_FLAG_ABSENT"`, `"BLOCK_ID_FLAG_COMMIT"`, `"BLOCK_ID_FLAG_NIL"` | 否 |
| validator_address | byte |  | 否 |
| timestamp | dateTime |  | 否 |
| signature | byte |  | 否 |

#### tendermint.types.Data

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| txs | [ byte ] | 将在 state @ block.Height+1 处应用的交易。注意：这里的交易并非全部有效。我们只是先就顺序达成一致。这意味着 block.AppHash 不包括这些交易。 | 否 |

#### tendermint.types.DuplicateVoteEvidence

DuplicateVoteEvidence 包含验证者签署了两个冲突投票的证据。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| vote_a | { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte } | Vote 表示验证者用于共识的预投票或预提交投票。 | 否 |
| vote_b | { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte } | Vote 表示验证者用于共识的预投票或预提交投票。 | 否 |
| total_voting_power | string (int64) |  | 否 |
| validator_power | string (int64) |  | 否 |
| timestamp | dateTime |  | 否 |

#### tendermint.types.Evidence

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| duplicate_vote_evidence | { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime } | DuplicateVoteEvidence 包含验证者签署了两个冲突投票的证据。 | 否 |
| light_client_attack_evidence | { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } | LightClientAttackEvidence 包含一组验证者试图误导轻客户端的证据。 | 否 |

#### tendermint.types.EvidenceList

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| evidence | [ { **"duplicate_vote_evidence"**: { **"vote_a"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"vote_b"**: { **"type"**: string, **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"timestamp"**: dateTime, **"validator_address"**: byte, **"validator_index"**: integer, **"signature"**: byte, **"extension"**: byte, **"extension_signature"**: byte }, **"total_voting_power"**: string (int64), **"validator_power"**: string (int64), **"timestamp"**: dateTime }, **"light_client_attack_evidence"**: { **"conflicting_block"**: { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } }, **"common_height"**: string (int64), **"byzantine_validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"total_voting_power"**: string (int64), **"timestamp"**: dateTime } } ] |  | 否 |

#### tendermint.types.Header

Header 定义了区块头的结构。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| version | { **"block"**: string (uint64), **"app"**: string (uint64) } | Consensus 捕获了处理区块链中区块的共识规则，包括所有区块链数据结构和应用程序状态转换机的规则。 | 否 |
| chain_id | string |  | 否 |
| height | string (int64) |  | 否 |
| time | dateTime |  | 否 |
| last_block_id | { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } } |  | 否 |
| last_commit_hash | byte |  | 否 |
| data_hash | byte |  | 否 |
| validators_hash | byte |  | 否 |
| next_validators_hash | byte |  | 否 |
| consensus_hash | byte |  | 否 |
| app_hash | byte |  | 否 |
| last_results_hash | byte |  | 否 |
| evidence_hash | byte |  | 否 |
| proposer_address | byte |  | 否 |

#### tendermint.types.LightBlock

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| signed_header | { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } } |  | 否 |
| validator_set | { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } |  | 否 |

#### tendermint.types.LightClientAttackEvidence

LightClientAttackEvidence 包含一组验证者试图误导轻客户端的证据。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| conflicting_block | { **"signed_header"**: { **"header"**: { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte }, **"commit"**: { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } }, **"validator_set"**: { **"validators"**: [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ], **"proposer"**: { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) }, **"total_voting_power"**: string (int64) } } |  | 否 |
| common_height | string (int64) |  | 否 |
| byzantine_validators | [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ] |  | 否 |
| total_voting_power | string (int64) |  | 否 |
| timestamp | dateTime |  | 否 |

#### tendermint.types.PartSetHeader

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| total | long |  | 否 |
| hash | byte |  | 否 |

#### tendermint.types.SignedHeader

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| header | { **"version"**: { **"block"**: string (uint64), **"app"**: string (uint64) }, **"chain_id"**: string, **"height"**: string (int64), **"time"**: dateTime, **"last_block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"last_commit_hash"**: byte, **"data_hash"**: byte, **"validators_hash"**: byte, **"next_validators_hash"**: byte, **"consensus_hash"**: byte, **"app_hash"**: byte, **"last_results_hash"**: byte, **"evidence_hash"**: byte, **"proposer_address"**: byte } | Header 定义了区块头的结构。 | 否 |
| commit | { **"height"**: string (int64), **"round"**: integer, **"block_id"**: { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } }, **"signatures"**: [ { **"block_id_flag"**: string, **"validator_address"**: byte, **"timestamp"**: dateTime, **"signature"**: byte } ] } | Commit 包含一组验证者已提交区块的证据。 | 否 |

#### tendermint.types.SignedMsgType

SignedMsgType 是共识中签名消息的类型。

 - SIGNED_MSG_TYPE_PREVOTE: 投票
 - SIGNED_MSG_TYPE_PROPOSAL: 提案

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| tendermint.types.SignedMsgType | string | SignedMsgType 是共识中签名消息的类型。   - SIGNED_MSG_TYPE_PREVOTE: 投票  - SIGNED_MSG_TYPE_PROPOSAL: 提案 |  |

#### tendermint.types.Validator

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| address | byte |  | 否 |
| pub_key | { **"ed25519"**: byte, **"secp256k1"**: byte } |  | 否 |
| voting_power | string (int64) |  | 否 |
| proposer_priority | string (int64) |  | 否 |

#### tendermint.types.ValidatorSet

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| validators | [ { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } ] |  | 否 |
| proposer | { **"address"**: byte, **"pub_key"**: { **"ed25519"**: byte, **"secp256k1"**: byte }, **"voting_power"**: string (int64), **"proposer_priority"**: string (int64) } |  | 否 |
| total_voting_power | string (int64) |  | 否 |

#### tendermint.types.Vote

Vote 表示验证者用于共识的预投票或预提交投票。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| type | string | SignedMsgType 是共识中签名消息的类型。   - SIGNED_MSG_TYPE_PREVOTE: 投票  - SIGNED_MSG_TYPE_PROPOSAL: 提案<br>*枚举:* `"SIGNED_MSG_TYPE_UNKNOWN"`, `"SIGNED_MSG_TYPE_PREVOTE"`, `"SIGNED_MSG_TYPE_PRECOMMIT"`, `"SIGNED_MSG_TYPE_PROPOSAL"` | 否 |
| height | string (int64) |  | 否 |
| round | integer |  | 否 |
| block_id | { **"hash"**: byte, **"part_set_header"**: { **"total"**: long, **"hash"**: byte } } |  | 否 |
| timestamp | dateTime |  | 否 |
| validator_address | byte |  | 否 |
| validator_index | integer |  | 否 |
| signature | byte | 验证者参与相关区块共识时的投票签名。 | 否 |
| extension | byte | 应用程序提供的投票扩展。仅对预提交消息有效。 | 否 |
| extension_signature | byte | 验证者参与相关区块共识时的投票扩展签名。仅对预提交消息有效。 | 否 |

#### tendermint.version.Consensus

Consensus 捕获了处理区块链中区块的共识规则，包括所有区块链数据结构和应用程序状态转换机的规则。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| block | string (uint64) |  | 否 |
| app | string (uint64) |  | 否 |

#### cosmos.base.node.v1beta1.ConfigResponse

ConfigResponse 定义了 Config gRPC 查询的响应结构。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| minimum_gas_price | string |  | 否 |
| pruning_keep_recent | string |  | 否 |
| pruning_interval | string |  | 否 |
| halt_height | string (uint64) |  | 否 |

#### cosmos.base.node.v1beta1.StatusResponse

StateResponse 定义了节点状态的响应结构。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| earliest_store_height | string (uint64) |  | 否 |
| height | string (uint64) |  | 否 |
| timestamp | dateTime |  | 否 |
| app_hash | byte |  | 否 |
| validator_hash | byte |  | 否 |

#### cosmos.base.v1beta1.DecCoin

DecCoin 定义了一个具有面额和十进制数量的代币。

注意：amount 字段是一个实现了 gogoproto 所需自定义方法
签名的 Dec。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| denom | string |  | 否 |
| amount | string |  | 否 |

#### cosmos.distribution.v1beta1.DelegationDelegatorReward

DelegationDelegatorReward 表示委托人的委托奖励的属性。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| validator_address | string |  | 否 |
| reward | [ { **"denom"**: string, **"amount"**: string } ] |  | 否 |

#### cosmos.distribution.v1beta1.Params

Params 定义了 distribution 模块的参数集。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| community_tax | string |  | 否 |
| base_proposer_reward | string | 已弃用：base_proposer_reward 字段已弃用，不再在 x/distribution 模块的奖励机制中使用。 | 否 |
| bonus_proposer_reward | string | 已弃用：bonus_proposer_reward 字段已弃用，不再在 x/distribution 模块的奖励机制中使用。 | 否 |
| withdraw_addr_enabled | boolean |  | 否 |

#### cosmos.distribution.v1beta1.QueryCommunityPoolResponse

QueryCommunityPoolResponse 是 Query/CommunityPool RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| pool | [ { **"denom"**: string, **"amount"**: string } ] | pool 定义了社区池的代币。 | 否 |

#### cosmos.distribution.v1beta1.QueryDelegationRewardsResponse

QueryDelegationRewardsResponse 是 Query/DelegationRewards RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| rewards | [ { **"denom"**: string, **"amount"**: string } ] | rewards 定义了委托所累积的奖励。 | 否 |

#### cosmos.distribution.v1beta1.QueryDelegationTotalRewardsResponse

QueryDelegationTotalRewardsResponse 是 Query/DelegationTotalRewards RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| rewards | [ { **"validator_address"**: string, **"reward"**: [ { **"denom"**: string, **"amount"**: string } ] } ] | rewards 定义了委托人累积的所有奖励。 | 否 |
| total | [ { **"denom"**: string, **"amount"**: string } ] | total 定义了所有奖励的总和。 | 否 |

#### cosmos.distribution.v1beta1.QueryDelegatorValidatorsResponse

QueryDelegatorValidatorsResponse 是 Query/DelegatorValidators RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| validators | [ string ] | validators 定义了委托人正在委托的验证者。 | 否 |

#### cosmos.distribution.v1beta1.QueryDelegatorWithdrawAddressResponse

QueryDelegatorWithdrawAddressResponse 是 Query/DelegatorWithdrawAddress RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| withdraw_address | string | withdraw_address 定义了要查询的委托人地址。 | 否 |

#### cosmos.distribution.v1beta1.QueryParamsResponse

QueryParamsResponse 是 Query/Params RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| params | { **"community_tax"**: string, **"base_proposer_reward"**: string, **"bonus_proposer_reward"**: string, **"withdraw_addr_enabled"**: boolean } | params 定义了模块的参数。 | 否 |

#### cosmos.distribution.v1beta1.QueryValidatorCommissionResponse

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| commission | { **"commission"**: [ { **"denom"**: string, **"amount"**: string } ] } | commission 定义了验证者收到的佣金。 | 否 |

#### cosmos.distribution.v1beta1.QueryValidatorDistributionInfoResponse

QueryValidatorDistributionInfoResponse 是 Query/ValidatorDistributionInfo RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| operator_address | string | operator_address 定义了验证者操作员地址。 | 否 |
| self_bond_rewards | [ { **"denom"**: string, **"amount"**: string } ] | self_bond_rewards 定义了自我委托的奖励。 | 否 |
| commission | [ { **"denom"**: string, **"amount"**: string } ] | commission 定义了验证者收到的佣金。 | 否 |

#### cosmos.distribution.v1beta1.QueryValidatorOutstandingRewardsResponse

QueryValidatorOutstandingRewardsResponse 是 Query/ValidatorOutstandingRewards RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| rewards | { **"rewards"**: [ { **"denom"**: string, **"amount"**: string } ] } | ValidatorOutstandingRewards 表示验证者的未提取奖励，跟踪成本低，允许简单的健全性检查。 | 否 |

#### cosmos.distribution.v1beta1.QueryValidatorSlashesResponse

QueryValidatorSlashesResponse 是 Query/ValidatorSlashes RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| slashes | [ { **"validator_period"**: string (uint64), **"fraction"**: string } ] | slashes 定义了验证者收到的削减。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.distribution.v1beta1.ValidatorAccumulatedCommission

ValidatorAccumulatedCommission 表示验证者累积的佣金，作为运行计数器维护，可以随时提取。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| commission | [ { **"denom"**: string, **"amount"**: string } ] |  | 否 |

#### cosmos.distribution.v1beta1.ValidatorOutstandingRewards

ValidatorOutstandingRewards 表示验证者的未提取奖励，跟踪成本低，允许简单的健全性检查。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| rewards | [ { **"denom"**: string, **"amount"**: string } ] |  | 否 |

#### cosmos.distribution.v1beta1.ValidatorSlashEvent

ValidatorSlashEvent 表示验证者削减事件。
高度在存储键中是隐式的。
这用于计算在削减发生后提取的委托的适当数量的质押代币。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| validator_period | string (uint64) |  | 否 |
| fraction | string |  | 否 |

#### cosmos.evidence.v1beta1.QueryAllEvidenceResponse

QueryAllEvidenceResponse 是 Query/AllEvidence RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| evidence | [ { **"type_url"**: string, **"value"**: byte } ] | evidence 返回所有证据。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.evidence.v1beta1.QueryEvidenceResponse

QueryEvidenceResponse 是 Query/Evidence RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| evidence | { **"type_url"**: string, **"value"**: byte } | `Any` 包含一个任意序列化的协议缓冲区消息以及一个描述序列化消息类型的 URL。Protobuf 库提供了以实用函数或 Any 类型的额外生成方法的形式来打包/解包 Any 值的支持。示例 1：在 C++ 中打包和解包消息。      Foo foo = ...;     Any any;     any.PackFrom(foo);     ...     if (any.UnpackTo(&foo)) {       ...     } 示例 2：在 Java 中打包和解包消息。      Foo foo = ...;     Any any = Any.pack(foo);     ...     if (any.is(Foo.class)) {       foo = any.unpack(Foo.class);     }     // 或 ...     if (any.isSameTypeAs(Foo.getDefaultInstance())) {       foo = any.unpack(Foo.getDefaultInstance());     } 示例 3：在 Python 中打包和解包消息。      foo = Foo(...)     any = Any()     any.Pack(foo)     ...     if any.Is(Foo.DESCRIPTOR):       any.Unpack(foo)       ... 示例 4：在 Go 中打包和解包消息。       foo := &pb.Foo{...}      any, err := anypb.New(foo)      if err != nil {        ...      }      ...      foo := &pb.Foo{}      if err := any.UnmarshalTo(foo); err != nil {        ...      } Protobuf 库提供的打包方法默认使用 'type.googleapis.com/full.type.name' 作为类型 URL，解包方法仅使用类型 URL 中最后一个 '/' 之后的完全限定类型名称，例如 "foo.bar.com/x/y.z" 将产生类型名称 "y.z"。JSON `Any` 值的 JSON 表示使用反序列化的嵌入消息的常规表示，并带有一个额外的字段 `@type`，其中包含类型 URL。示例：      package google.profile;     message Person {       string first_name = 1;       string last_name = 2;     }      {       "@type": "type.googleapis.com/google.profile.Person",       "firstName": <string>,       "lastName": <string>     } 如果嵌入的消息类型是众所周知的并且具有自定义 JSON 表示，则该表示将被嵌入，添加一个字段 `value`，该字段保存自定义 JSON，此外还有 `@type` 字段。示例（对于消息 [google.protobuf.Duration][]）：      {       "@type": "type.googleapis.com/google.protobuf.Duration",       "value": "1.212s"     } | 否 |

#### cosmos.gov.v1beta1.Deposit

Deposit 定义了账户地址向活跃提案存入的金额。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposal_id | string (uint64) | proposal_id 定义了提案的唯一 id。 | 否 |
| depositor | string | depositor 定义了提案的存款地址。 | 否 |
| amount | [ { **"denom"**: string, **"amount"**: string } ] | 由存款人存入的金额。 | 否 |

#### cosmos.gov.v1beta1.DepositParams

DepositParams 定义了治理提案存款的参数。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| min_deposit | [ { **"denom"**: string, **"amount"**: string } ] | 提案进入投票期的最低存款。 | 否 |
| max_deposit_period | string | Atom 持有者在提案上存款的最长期限。初始值：2 个月。 | 否 |

#### cosmos.gov.v1beta1.Proposal

Proposal 定义了治理提案的核心字段成员。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposal_id | string (uint64) | proposal_id 定义了提案的唯一 id。 | 否 |
| content | { **"type_url"**: string, **"value"**: byte } | `Any` 包含一个任意序列化的协议缓冲区消息以及一个描述序列化消息类型的 URL。Protobuf 库提供了以实用函数或 Any 类型的额外生成方法的形式来打包/解包 Any 值的支持。示例 1：在 C++ 中打包和解包消息。      Foo foo = ...;     Any any;     any.PackFrom(foo);     ...     if (any.UnpackTo(&foo)) {       ...     } 示例 2：在 Java 中打包和解包消息。      Foo foo = ...;     Any any = Any.pack(foo);     ...     if (any.is(Foo.class)) {       foo = any.unpack(Foo.class);     }     // 或 ...     if (any.isSameTypeAs(Foo.getDefaultInstance())) {       foo = any.unpack(Foo.getDefaultInstance());     } 示例 3：在 Python 中打包和解包消息。      foo = Foo(...)     any = Any()     any.Pack(foo)     ...     if any.Is(Foo.DESCRIPTOR):       any.Unpack(foo)       ... 示例 4：在 Go 中打包和解包消息。       foo := &pb.Foo{...}      any, err := anypb.New(foo)      if err != nil {        ...      }      ...      foo := &pb.Foo{}      if err := any.UnmarshalTo(foo); err != nil {        ...      } Protobuf 库提供的打包方法默认使用 'type.googleapis.com/full.type.name' 作为类型 URL，解包方法仅使用类型 URL 中最后一个 '/' 之后的完全限定类型名称，例如 "foo.bar.com/x/y.z" 将产生类型名称 "y.z"。JSON `Any` 值的 JSON 表示使用反序列化的嵌入消息的常规表示，并带有一个额外的字段 `@type`，其中包含类型 URL。示例：      package google.profile;     message Person {       string first_name = 1;       string last_name = 2;     }      {       "@type": "type.googleapis.com/google.profile.Person",       "firstName": <string>,       "lastName": <string>     } 如果嵌入的消息类型是众所周知的并且具有自定义 JSON 表示，则该表示将被嵌入，添加一个字段 `value`，该字段保存自定义 JSON，此外还有 `@type` 字段。示例（对于消息 [google.protobuf.Duration][]）：      {       "@type": "type.googleapis.com/google.protobuf.Duration",       "value": "1.212s"     } | 否 |
| status | string | status 定义了提案状态。<br>*枚举:* `"PROPOSAL_STATUS_UNSPECIFIED"`, `"PROPOSAL_STATUS_DEPOSIT_PERIOD"`, `"PROPOSAL_STATUS_VOTING_PERIOD"`, `"PROPOSAL_STATUS_PASSED"`, `"PROPOSAL_STATUS_REJECTED"`, `"PROPOSAL_STATUS_FAILED"` | 否 |
| final_tally_result | { **"yes"**: string, **"abstain"**: string, **"no"**: string, **"no_with_veto"**: string } | final_tally_result 是提案的最终计票结果。当通过 gRPC 查询提案时，此字段在提案投票期结束之前不会填充。 | 否 |
| submit_time | dateTime | submit_time 是提案提交的时间。 | 否 |
| deposit_end_time | dateTime | deposit_end_time 是存款结束的时间。 | 否 |
| total_deposit | [ { **"denom"**: string, **"amount"**: string } ] | total_deposit 是提案上的总存款。 | 否 |
| voting_start_time | dateTime | voting_start_time 是开始对提案投票的时间。 | 否 |
| voting_end_time | dateTime | voting_end_time 是提案投票结束的时间。 | 否 |

#### cosmos.gov.v1beta1.ProposalStatus

ProposalStatus 枚举了提案的有效状态。

 - PROPOSAL_STATUS_UNSPECIFIED: PROPOSAL_STATUS_UNSPECIFIED 定义了默认提案状态。
 - PROPOSAL_STATUS_DEPOSIT_PERIOD: PROPOSAL_STATUS_DEPOSIT_PERIOD 定义了存款期内的提案状态。
 - PROPOSAL_STATUS_VOTING_PERIOD: PROPOSAL_STATUS_VOTING_PERIOD 定义了投票期内的提案状态。
 - PROPOSAL_STATUS_PASSED: PROPOSAL_STATUS_PASSED 定义了已通过提案的提案状态。
 - PROPOSAL_STATUS_REJECTED: PROPOSAL_STATUS_REJECTED 定义了已被拒绝提案的提案状态。
 - PROPOSAL_STATUS_FAILED: PROPOSAL_STATUS_FAILED 定义了已失败提案的提案状态。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| cosmos.gov.v1beta1.ProposalStatus | string | ProposalStatus 枚举了提案的有效状态。   - PROPOSAL_STATUS_UNSPECIFIED: PROPOSAL_STATUS_UNSPECIFIED 定义了默认提案状态。  - PROPOSAL_STATUS_DEPOSIT_PERIOD: PROPOSAL_STATUS_DEPOSIT_PERIOD 定义了存款期内的提案状态。  - PROPOSAL_STATUS_VOTING_PERIOD: PROPOSAL_STATUS_VOTING_PERIOD 定义了投票期内的提案状态。  - PROPOSAL_STATUS_PASSED: PROPOSAL_STATUS_PASSED 定义了已通过提案的提案状态。  - PROPOSAL_STATUS_REJECTED: PROPOSAL_STATUS_REJECTED 定义了已被拒绝提案的提案状态。  - PROPOSAL_STATUS_FAILED: PROPOSAL_STATUS_FAILED 定义了已失败提案的提案状态。 |  |

#### cosmos.gov.v1beta1.QueryDepositResponse

QueryDepositResponse 是 Query/Deposit RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| deposit | { **"proposal_id"**: string (uint64), **"depositor"**: string, **"amount"**: [ { **"denom"**: string, **"amount"**: string } ] } | Deposit 定义了账户地址向活跃提案存入的金额。 | 否 |

#### cosmos.gov.v1beta1.QueryDepositsResponse

QueryDepositsResponse 是 Query/Deposits RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| deposits | [ { **"proposal_id"**: string (uint64), **"depositor"**: string, **"amount"**: [ { **"denom"**: string, **"amount"**: string } ] } ] | deposits 定义了请求的存款。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.gov.v1beta1.QueryParamsResponse

QueryParamsResponse 是 Query/Params RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| voting_params | { **"voting_period"**: string } | voting_params 定义了与投票相关的参数。 | 否 |
| deposit_params | { **"min_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"max_deposit_period"**: string } | deposit_params 定义了与存款相关的参数。 | 否 |
| tally_params | { **"quorum"**: byte, **"threshold"**: byte, **"veto_threshold"**: byte } | tally_params 定义了与计票相关的参数。 | 否 |

#### cosmos.gov.v1beta1.QueryProposalResponse

QueryProposalResponse 是 Query/Proposal RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposal | { **"proposal_id"**: string (uint64), **"content"**: { **"type_url"**: string, **"value"**: byte }, **"status"**: string, **"final_tally_result"**: { **"yes"**: string, **"abstain"**: string, **"no"**: string, **"no_with_veto"**: string }, **"submit_time"**: dateTime, **"deposit_end_time"**: dateTime, **"total_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"voting_start_time"**: dateTime, **"voting_end_time"**: dateTime } | Proposal 定义了治理提案的核心字段成员。 | 否 |

#### cosmos.gov.v1beta1.QueryProposalsResponse

QueryProposalsResponse 是 Query/Proposals RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposals | [ { **"proposal_id"**: string (uint64), **"content"**: { **"type_url"**: string, **"value"**: byte }, **"status"**: string, **"final_tally_result"**: { **"yes"**: string, **"abstain"**: string, **"no"**: string, **"no_with_veto"**: string }, **"submit_time"**: dateTime, **"deposit_end_time"**: dateTime, **"total_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"voting_start_time"**: dateTime, **"voting_end_time"**: dateTime } ] | proposals 定义了所有请求的治理提案。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.gov.v1beta1.QueryTallyResultResponse

QueryTallyResultResponse 是 Query/Tally RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| tally | { **"yes"**: string, **"abstain"**: string, **"no"**: string, **"no_with_veto"**: string } | tally 定义了请求的计票结果。 | 否 |

#### cosmos.gov.v1beta1.QueryVoteResponse

QueryVoteResponse 是 Query/Vote RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| vote | { **"proposal_id"**: string (uint64), **"voter"**: string, **"option"**: string, **"options"**: [ { **"option"**: string, **"weight"**: string } ] } | Vote 定义了治理提案的投票。一个投票由提案 ID、投票人和投票选项组成。 | 否 |

#### cosmos.gov.v1beta1.QueryVotesResponse

QueryVotesResponse 是 Query/Votes RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| votes | [ { **"proposal_id"**: string (uint64), **"voter"**: string, **"option"**: string, **"options"**: [ { **"option"**: string, **"weight"**: string } ] } ] | votes 定义了查询的投票。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.gov.v1beta1.TallyParams

TallyParams 定义了治理提案投票计票的参数。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| quorum | byte | 总质押中需要投票以使结果被视为有效的最小百分比。 | 否 |
| threshold | byte | 提案通过所需赞成票的最小比例。默认值：0.5。 | 否 |
| veto_threshold | byte | 提案被否决所需否决票与总票数比率的最小值。默认值：1/3。 | 否 |

#### cosmos.gov.v1beta1.TallyResult

TallyResult 定义了治理提案的标准计票结果。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| yes | string | yes 是提案的赞成票数。 | 否 |
| abstain | string | abstain 是提案的弃权票数。 | 否 |
| no | string | no 是提案的反对票数。 | 否 |
| no_with_veto | string | no_with_veto 是提案的带否决反对票数。 | 否 |

#### cosmos.gov.v1beta1.Vote

Vote 定义了治理提案的投票。
一个投票由提案 ID、投票人和投票选项组成。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposal_id | string (uint64) | proposal_id 定义了提案的唯一 id。 | 否 |
| voter | string | voter 是提案的投票人地址。 | 否 |
| option | string | 已弃用：建议使用 `options` 代替。当且仅当 `len(options) == 1` 且该选项权重为 1 时，此字段在查询中设置。在所有其他情况下，此字段将默认为 VOTE_OPTION_UNSPECIFIED。<br>*枚举:* `"VOTE_OPTION_UNSPECIFIED"`, `"VOTE_OPTION_YES"`, `"VOTE_OPTION_ABSTAIN"`, `"VOTE_OPTION_NO"`, `"VOTE_OPTION_NO_WITH_VETO"` | 否 |
| options | [ { **"option"**: string, **"weight"**: string } ] | options 是加权投票选项。  自：cosmos-sdk 0.43 | 否 |

#### cosmos.gov.v1beta1.VoteOption

VoteOption 枚举了给定治理提案的有效投票选项。

 - VOTE_OPTION_UNSPECIFIED: VOTE_OPTION_UNSPECIFIED 定义了一个无操作的投票选项。
 - VOTE_OPTION_YES: VOTE_OPTION_YES 定义了一个赞成投票选项。
 - VOTE_OPTION_ABSTAIN: VOTE_OPTION_ABSTAIN 定义了一个弃权投票选项。
 - VOTE_OPTION_NO: VOTE_OPTION_NO 定义了一个反对投票选项。
 - VOTE_OPTION_NO_WITH_VETO: VOTE_OPTION_NO_WITH_VETO 定义了一个带否决的反对投票选项。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| cosmos.gov.v1beta1.VoteOption | string | VoteOption 枚举了给定治理提案的有效投票选项。   - VOTE_OPTION_UNSPECIFIED: VOTE_OPTION_UNSPECIFIED 定义了一个无操作的投票选项。  - VOTE_OPTION_YES: VOTE_OPTION_YES 定义了一个赞成投票选项。  - VOTE_OPTION_ABSTAIN: VOTE_OPTION_ABSTAIN 定义了一个弃权投票选项。  - VOTE_OPTION_NO: VOTE_OPTION_NO 定义了一个反对投票选项。  - VOTE_OPTION_NO_WITH_VETO: VOTE_OPTION_NO_WITH_VETO 定义了一个带否决的反对投票选项。 |  |

#### cosmos.gov.v1beta1.VotingParams

VotingParams 定义了治理提案投票的参数。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| voting_period | string | 投票期的持续时间。 | 否 |

#### cosmos.gov.v1beta1.WeightedVoteOption

WeightedVoteOption 定义了投票分割的投票单位。

自：cosmos-sdk 0.43

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| option | string | option 定义了有效的投票选项，不得包含重复的投票选项。<br>*枚举:* `"VOTE_OPTION_UNSPECIFIED"`, `"VOTE_OPTION_YES"`, `"VOTE_OPTION_ABSTAIN"`, `"VOTE_OPTION_NO"`, `"VOTE_OPTION_NO_WITH_VETO"` | 否 |
| weight | string | weight 是与投票选项关联的投票权重。 | 否 |

#### cosmos.gov.v1.Deposit

Deposit 定义了账户地址向活跃提案存入的金额。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposal_id | string (uint64) | proposal_id 定义了提案的唯一 id。 | 否 |
| depositor | string | depositor 定义了提案的存款地址。 | 否 |
| amount | [ { **"denom"**: string, **"amount"**: string } ] | 由存款人存入的金额。 | 否 |

#### cosmos.gov.v1.DepositParams

DepositParams 定义了治理提案存款的参数。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| min_deposit | [ { **"denom"**: string, **"amount"**: string } ] | 提案进入投票期的最低存款。 | 否 |
| max_deposit_period | string | Atom 持有者在提案上存款的最长期限。初始值：2 个月。 | 否 |

#### cosmos.gov.v1.Params

Params 定义了 x/gov 模块的参数。

自：cosmos-sdk 0.47

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| min_deposit | [ { **"denom"**: string, **"amount"**: string } ] | 提案进入投票期的最低存款。 | 否 |
| max_deposit_period | string | Atom 持有者在提案上存款的最长期限。初始值：2 个月。 | 否 |
| voting_period | string | 投票期的持续时间。 | 否 |
| quorum | string | 总质押中需要投票以使结果被视为有效的最小百分比。 | 否 |
| threshold | string | 提案通过所需赞成票的最小比例。默认值：0.5。 | 否 |
| veto_threshold | string | 提案被否决所需否决票与总票数比率的最小值。默认值：1/3。 | 否 |
| min_initial_deposit_ratio | string | 表示提案提交时必须支付的存款价值比例。 | 否 |
| proposal_cancel_ratio | string | 提案取消时不会返还给存款人的取消比例。自：cosmos-sdk 0.50 | 否 |
| proposal_cancel_dest | string | 将接收（proposal_cancel_ratio * deposit）提案存款的地址。如果为空，（proposal_cancel_ratio * deposit）提案存款将被销毁。自：cosmos-sdk 0.50 | 否 |
| expedited_voting_period | string | 快速提案的投票期持续时间。  自：cosmos-sdk 0.50 | 否 |
| expedited_threshold | string | 提案通过所需赞成票的最小比例。默认值：0.67。自：cosmos-sdk 0.50 | 否 |
| expedited_min_deposit | [ { **"denom"**: string, **"amount"**: string } ] | 快速提案进入投票期的最低存款。 | 否 |
| burn_vote_quorum | boolean |  | 否 |
| burn_proposal_deposit_prevote | boolean |  | 否 |
| burn_vote_veto | boolean |  | 否 |
| min_deposit_ratio | string | 表示存款时必须满足的存款价值最小比例。默认值：0.01。这意味着对于最小存款为 100stake 的链，需要 1stake 的存款。自：cosmos-sdk 0.50 | 否 |

#### cosmos.gov.v1.Proposal

Proposal 定义了治理提案的核心字段成员。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| id | string (uint64) | id 定义了提案的唯一 id。 | 否 |
| messages | [ { **"type_url"**: string, **"value"**: byte } ] | messages 是提案通过时要执行的任意消息。 | 否 |
| status | string | status 定义了提案状态。<br>*枚举:* `"PROPOSAL_STATUS_UNSPECIFIED"`, `"PROPOSAL_STATUS_DEPOSIT_PERIOD"`, `"PROPOSAL_STATUS_VOTING_PERIOD"`, `"PROPOSAL_STATUS_PASSED"`, `"PROPOSAL_STATUS_REJECTED"`, `"PROPOSAL_STATUS_FAILED"` | 否 |
| final_tally_result | { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string } | final_tally_result 是提案的最终计票结果。当通过 gRPC 查询提案时，此字段在提案投票期结束之前不会填充。 | 否 |
| submit_time | dateTime | submit_time 是提案提交的时间。 | 否 |
| deposit_end_time | dateTime | deposit_end_time 是存款结束的时间。 | 否 |
| total_deposit | [ { **"denom"**: string, **"amount"**: string } ] | total_deposit 是提案上的总存款。 | 否 |
| voting_start_time | dateTime | voting_start_time 是开始对提案投票的时间。 | 否 |
| voting_end_time | dateTime | voting_end_time 是提案投票结束的时间。 | 否 |
| metadata | string |  | 否 |
| title | string | 自：cosmos-sdk 0.47 | 否 |
| summary | string | 自：cosmos-sdk 0.47 | 否 |
| proposer | string | 自：cosmos-sdk 0.47 | 否 |
| expedited | boolean | 自：cosmos-sdk 0.50 | 否 |
| failed_reason | string | 自：cosmos-sdk 0.50 | 否 |

#### cosmos.gov.v1.ProposalStatus

ProposalStatus 枚举了提案的有效状态。

 - PROPOSAL_STATUS_UNSPECIFIED: PROPOSAL_STATUS_UNSPECIFIED 定义了默认提案状态。
 - PROPOSAL_STATUS_DEPOSIT_PERIOD: PROPOSAL_STATUS_DEPOSIT_PERIOD 定义了存款期内的提案状态。
 - PROPOSAL_STATUS_VOTING_PERIOD: PROPOSAL_STATUS_VOTING_PERIOD 定义了投票期内的提案状态。
 - PROPOSAL_STATUS_PASSED: PROPOSAL_STATUS_PASSED 定义了已通过提案的提案状态。
 - PROPOSAL_STATUS_REJECTED: PROPOSAL_STATUS_REJECTED 定义了已被拒绝提案的提案状态。
 - PROPOSAL_STATUS_FAILED: PROPOSAL_STATUS_FAILED 定义了已失败提案的提案状态。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| cosmos.gov.v1.ProposalStatus | string | ProposalStatus 枚举了提案的有效状态。   - PROPOSAL_STATUS_UNSPECIFIED: PROPOSAL_STATUS_UNSPECIFIED 定义了默认提案状态。  - PROPOSAL_STATUS_DEPOSIT_PERIOD: PROPOSAL_STATUS_DEPOSIT_PERIOD 定义了存款期内的提案状态。  - PROPOSAL_STATUS_VOTING_PERIOD: PROPOSAL_STATUS_VOTING_PERIOD 定义了投票期内的提案状态。  - PROPOSAL_STATUS_PASSED: PROPOSAL_STATUS_PASSED 定义了已通过提案的提案状态。  - PROPOSAL_STATUS_REJECTED: PROPOSAL_STATUS_REJECTED 定义了已被拒绝提案的提案状态。  - PROPOSAL_STATUS_FAILED: PROPOSAL_STATUS_FAILED 定义了已失败提案的提案状态。 |  |

#### cosmos.gov.v1.QueryConstitutionResponse

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| constitution | string |  | 否 |

#### cosmos.gov.v1.QueryDepositResponse

QueryDepositResponse 是 Query/Deposit RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| deposit | { **"proposal_id"**: string (uint64), **"depositor"**: string, **"amount"**: [ { **"denom"**: string, **"amount"**: string } ] } | Deposit 定义了账户地址向活跃提案存入的金额。 | 否 |

#### cosmos.gov.v1.QueryDepositsResponse

QueryDepositsResponse 是 Query/Deposits RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| deposits | [ { **"proposal_id"**: string (uint64), **"depositor"**: string, **"amount"**: [ { **"denom"**: string, **"amount"**: string } ] } ] | deposits 定义了请求的存款。 | 否 |
| pagination | { **"next_key"**: byte, **"total"**: string (uint64) } | pagination 定义了响应中的分页。 | 否 |

#### cosmos.gov.v1.QueryParamsResponse

QueryParamsResponse 是 Query/Params RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| voting_params | { **"voting_period"**: string } | 已弃用：建议使用 `params` 代替。voting_params 定义了与投票相关的参数。 | 否 |
| deposit_params | { **"min_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"max_deposit_period"**: string } | 已弃用：建议使用 `params` 代替。deposit_params 定义了与存款相关的参数。 | 否 |
| tally_params | { **"quorum"**: string, **"threshold"**: string, **"veto_threshold"**: string } | 已弃用：建议使用 `params` 代替。tally_params 定义了与计票相关的参数。 | 否 |
| params | { **"min_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"max_deposit_period"**: string, **"voting_period"**: string, **"quorum"**: string, **"threshold"**: string, **"veto_threshold"**: string, **"min_initial_deposit_ratio"**: string, **"proposal_cancel_ratio"**: string, **"proposal_cancel_dest"**: string, **"expedited_voting_period"**: string, **"expedited_threshold"**: string, **"expedited_min_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"burn_vote_quorum"**: boolean, **"burn_proposal_deposit_prevote"**: boolean, **"burn_vote_veto"**: boolean, **"min_deposit_ratio"**: string } | params 定义了 x/gov 模块的所有参数。  自：cosmos-sdk 0.47 | 否 |

#### cosmos.gov.v1.QueryProposalResponse

QueryProposalResponse 是 Query/Proposal RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposal | { **"id"**: string (uint64), **"messages"**: [ { **"type_url"**: string, **"value"**: byte } ], **"status"**: string, **"final_tally_result"**: { **"yes_count"**: string, **"abstain_count"**: string, **"no_count"**: string, **"no_with_veto_count"**: string }, **"submit_time"**: dateTime, **"deposit_end_time"**: dateTime, **"total_deposit"**: [ { **"denom"**: string, **"amount"**: string } ], **"voting_start_time"**: dateTime, **"voting_end_time"**: dateTime, **"metadata"**: string, **"title"**: string, **"summary"**: string, **"proposer"**: string, **"expedited"**: boolean, **"failed_reason"**: string } | Proposal 定义了治理提案的核心字段成员。 | 否 |

#### cosmos.gov.v1.QueryProposalsResponse

QueryProposalsResponse 是 Query/Proposals RPC 方法的响应类型。

| 名称 | 类型 | 描述 | 是否必需 |
| ---- | ---- | ----------- | -------- |
| proposals | [ { **"id"**: string (uint64), **"messages