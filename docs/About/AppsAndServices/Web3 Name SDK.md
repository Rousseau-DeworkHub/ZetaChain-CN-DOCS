# Web3 Name SDK

| 标题 | 描述 |
| :- | :- |
| Web3 Name SDK | 解析 Web3 域名与反向解析地址的快速集成指南 |

解析 Web3 域名或反向解析常规地址

## 概述

该 SDK 的主要功能包括：

- 域名解析：解析域名以获取有关域名的基本信息，包括其关联的常规地址、各种记录（如头像、IPFS 链接、社交数据）和元数据等。
- 反向解析：SDK 支持反向地址解析。此功能使得确定与给定地址关联的主域名成为可能，即使跨越不同的区块链或 TLD，也能返回链主域名或 TLD 主域名。

### 关键术语

TLD 主域名：

- 每个地址都能够设置 TLD 主域名，为每个顶级域名配置一个反向解析域，无论其是否已在 SPACE ID 上得到验证。
- 示例包括为 .eth 设置 "allen.eth" 作为 TLD 主域名，为 .zeta 设置 "allen.zeta"，为 .bnb 设置 "allen.bnb"。

链主域名：

- 每个地址在每个区块链或网络上只允许拥有一个唯一的链主域名。
- 具体来说，当单个链上存在多个已验证的 TLD 时，只能选择一个域名作为该特定链的反向解析域。
- 例如，"allen.eth" 可以作为以太坊的链主域名，而 "allen.zeta" 则可以作为 ZetaChain 的主域名。

默认情况下，Web3 Name SDK 支持所有基于 EVM 的域名的域名解析。反向解析为每个 EVM 链返回一个链主域名。项目管理员可以灵活选择是集成对所有链和 TLD 的支持，还是仅支持特定的链和 TLD。他们还可以根据需要配置反向解析的自定义设置。这种适应性允许项目根据其特定需求定制 SDK 的功能。

## 快速入门

开发者可以使用 Web3 Name SDK 解析 Web3 域名或反向解析常规地址，无需任何配置。

## 安装

```bash
npm install @web3-name-sdk/core viem@^1.20
```

如果您使用的是 Next.js，请在 `next.config.js` 中添加以下配置，以便转译 CommonJS 依赖项：

```typescript
const nextConfig = {
  transpilePackages: ["@web3-name-sdk/core"],
};
```

### 1. 设置客户端

```typescript
import { createWeb3Name } from "@web3-name-sdk/core";

const web3Name = createWeb3Name();
```

### 2. 解析域名

您可以通过单个请求从域名获取地址：

```typescript
const address = await web3name.getAddress("zeta.zeta");
const address = await web3name.getAddress("bts_official.lens");
const address = await web3name.getAddress("beresnev.crypto");
const address = await web3name.getAddress("registry.zeta");
```

### 3. 解析地址

该方法中有可选参数，用于选择您的目标链或 TLD (顶级域名)。
通过提供链 ID，您可以在选定的链上解析地址，并从部署在这些链上的所有 TLD 中获取一个可用的域名。

```typescript
// 从 ZetaChain 解析地址
const name = await web3name.getDomainName({
  address: "0x253a4ee0acb7c89bab7c20097200ea240119049a",
  queryChainIdList: [7000],
}); // 预期：karlyshka.zeta
```

通过提供 TLD，可以从选定的 TLD 中解析地址，并获取一个可用的 TLD 主域名。

```typescript
// 从 .zeta TLD 解析地址
const name = await web3name.getDomainName({
  address: "0x253a4ee0acb7c89bab7c20097200ea240119049a",
  queryTldList: ["zeta"],
}); // 预期：karlyshka.zeta
```

### 4. 记录

通过提供域名和键 (key)，可以获取域名的文本记录。例如，给定键名 `avatar`，此方法将返回 `zeta.zeta` 的头像记录：

```typescript
const record = await web3Name.getDomainRecord({
  name: "zeta.zeta",
  key: "avatar",
});
```

### 5. 元数据

域名元数据可以由 SDK 直接获取。

```typescript
// 请求中
const metadata = await web3Name.getMetadata({ name: "public.zeta" });
```
