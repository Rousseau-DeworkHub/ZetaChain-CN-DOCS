# Sui

| 标题 | 描述               |
| :--- | :----------------- |
| Sui  | Sui 协议合约库文档 |

# 模块 `gateway::gateway`

- [结构体 `Vault`](#结构体-vault)
- [结构体 `Gateway`](#结构体-gateway)
- [结构体 `WithdrawCap`](#结构体-withdrawcap)
- [结构体 `WhitelistCap`](#结构体-whitelistcap)
- [结构体 `AdminCap`](#结构体-admincap)
- [结构体 `DepositEvent`](#结构体-depositevent)
- [结构体 `DepositAndCallEvent`](#结构体-depositandcallevent)
- [结构体 `WithdrawEvent`](#结构体-withevent)
- [结构体 `NonceIncreaseEvent`](#结构体-nonceincreaseevent)
- [结构体 `DonateEvent`](#结构体-donateevent)
- [常量（Constants）](#常量constants)
- [函数 `init`](#函数-init)
- [函数 `increase_nonce`](#函数-increase_nonce)
- [函数 `withdraw`](#函数-withdraw)
- [函数 `whitelist`](#函数-whitelist)
- [函数 `unwhitelist`](#函数-unwhitelist)
- [函数 `issue_withdraw_and_whitelist_cap`](#函数-issue_withdraw_and_whitelist_cap)
- [函数 `pause`](#函数-pause)
- [函数 `unpause`](#函数-unpause)
- [函数 `reset_nonce`](#函数-reset_nonce)
- [函数 `deposit`](#函数-deposit)
- [函数 `deposit_and_call`](#函数-deposit_and_call)
- [函数 `donate`](#函数-donate)
- [函数 `check_receiver_and_deposit_to_vault`](#函数-check_receiver_and_deposit_to_vault)
- [函数 `withdraw_impl`](#函数-withdraw_impl)
- [函数 `whitelist_impl`](#函数-whitelist_impl)
- [函数 `unwhitelist_impl`](#函数-unwhitelist_impl)
- [函数 `issue_withdraw_and_whitelist_cap_impl`](#函数-issue_withdraw_and_whitelist_cap_impl)
- [函数 `pause_impl`](#函数-pause_impl)
- [函数 `unpause_impl`](#函数-unpause_impl)
- [函数 `nonce`](#函数-nonce)
- [函数 `active_withdraw_cap`](#函数-active_withdraw_cap)
- [函数 `active_whitelist_cap`](#函数-active_whitelist_cap)
- [函数 `vault_balance`](#函数-vault_balance)
- [函数 `is_paused`](#函数-is_paused)
- [函数 `is_whitelisted`](#函数-is_whitelisted)
- [函数 `coin_name`](#函数-coin_name)

```move
use gateway::evm;
use std::address;
use std::ascii;
use std::bcs;
use std::option;
use std::string;
use std::type_name;
use std::vector;
use sui::address;
use sui::bag;
use sui::balance;
use sui::coin;
use sui::config;
use sui::deny_list;
use sui::dynamic_field;
use sui::dynamic_object_field;
use sui::event;
use sui::hex;
use sui::object;
use sui::party;
use sui::sui;
use sui::table;
use sui::transfer;
use sui::tx_context;
use sui::types;
use sui::url;
use sui::vec_map;
use sui::vec_set;
```
