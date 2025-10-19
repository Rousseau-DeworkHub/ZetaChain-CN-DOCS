# 添加账户

# 必要条件

本教程需要安装 `zetacored` CLI。请查看有关[安装 CLI](https://www.zetachain.com/docs/users/cli/setup) 的文档。

**本指南使用的是测试密钥环，并不安全。请勿将其用于持有真实资金的账户。**

在使用 CLI 与 ZetaChain 交互之前，您需要添加一个账户。

# 创建新账户

创建新账户：

```shell
zetacored keys add alice
```

其中 `alice`是账户的名称。

```shell
- address: zeta10r4ygmwhd5jyrfrve72u3vz0ujdr8lvatw0gw9
  name: alice
  pubkey: '{"@type":"/ethermint.crypto.v1.ethsecp256k1.PubKey","key":"A4pXWBWe/MK8gRhBCuOgeVZu33IaMX08TYTznbHiUg5R"}'
  type: local
```

**重要提示**：请将此助记词短语妥善保存在安全的地方。它是您在忘记密码时恢复账户的唯一方式。

```
fade sunset wink lonely seek glass load group shove scan tape shop rather connect enhance absurd illness patch void save skirt fee code mushroom
```

在本指南及后续指南中，我们将使用 `alice`作为示例账户名。当命令需要地址时，我们将使用以下命令 `$(zetacored keys show alice -a)`，该命令仅返回给定密钥的地址。请注意在以下示例中，请将 `alice`替换为您自己的密钥名称。

# 导入现有账户

如果您已有现有账户，可以使用助记词短语导入：

```shell
zetacored keys add bob --recover
```

终端将要求您输入助记词短语：

```shell
> Enter your bip39 mnemonic
man promote grunt cube venture shaft fix scorpion payment tobacco bunker cannon sugar funny time lake foster believe raccoon then shadow price hour weekend
- address: zeta130c4smfsmdncp0vgqc8nh64dn80q3tkz3hjj4n
  name: bob
  pubkey: '{"@type":"/ethermint.crypto.v1.ethsecp256k1.PubKey","key":"AlwIbpaOnvauaiRXTGZgyzRBqexCUUvwzACG+j4KzceW"}'
  type: local
```

**注意**：上面的助记词短语仅用于演示目的。请勿使用它。

# 列出所有账户

```shell
zetacored keys list
```

```shell
- address: zeta10r4ygmwhd5jyrfrve72u3vz0ujdr8lvatw0gw9
  name: alice
  pubkey: '{"@type":"/ethermint.crypto.v1.ethsecp256k1.PubKey","key":"A4pXWBWe/MK8gRhBCuOgeVZu33IaMX08TYTznbHiUg5R"}'
  type: local

- address: zeta130c4smfsmdncp0vgqc8nh64dn80q3tkz3hjj4n
  name: bob
  pubkey: '{"@type":"/ethermint.crypto.v1.ethsecp256k1.PubKey","key":"AlwIbpaOnvauaiRXTGZgyzRBqexCUUvwzACG+j4KzceW"}'
  type: local
```

# 地址格式转换

ZetaChain 使用两种类型的地址：

- 类似 `zeta***`的 bech32 地址
- 类似 `0x***`的 hex 地址

您可以使用 `debug addr`命令在两种格式之间进行转换：

```shell
zetacored debug addr zeta10r4ygmwhd5jyrfrve72u3vz0ujdr8lvatw0gw9
```

```shell
Address: [120 234 68 109 215 109 36 65 164 108 207 149 200 176 79 228 154 51 253 157]
Address (hex): 78EA446DD76D2441A46CCF95C8B04FE49A33FD9D
Bech32 Acc: zeta10r4ygmwhd5jyrfrve72u3vz0ujdr8lvatw0gw9
Bech32 Val: zetavaloper10r4ygmwhd5jyrfrve72u3vz0ujdr8lva0wh5rn
```

单个账户可以用 bech32 地址或 hex 地址表示。您不需要在 `zeta***`和 `0x***`地址之间转移代币，因为这两个地址代表的是同一个账户，持有相同数量的代币。