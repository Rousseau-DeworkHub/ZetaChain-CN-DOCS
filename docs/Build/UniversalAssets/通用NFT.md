| 标题     | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| 通用 NFT | 通用 NFT 标准允许在任何链上铸造非同质化代币（ERC-721 NFT），并在连接的链之间无缝转移。 |

通用 NFT 是完全可互操作的 ERC-721 代币，能够在任意连接链之间进行铸造与转移，无需包装或桥接。每个 NFT 都具有在所有链上保持不变的持久化 Token ID，且在跨链转移过程中其元数据会被保留。由此实现真正与链无关的所有权与交互，可用于跨链游戏、市场以及身份等场景。

在 ZetaChain 上，通用 NFT 基于标准的 [OpenZeppelin ERC-721](https://docs.openzeppelin.com/contracts/5.x/api/token/erc721) 实现，并采用 [UUPS 可升级](https://docs.openzeppelin.com/contracts/5.x/api/proxy#UUPSUpgradeable) 代理模式，允许开发者在确保安全的前提下随时间扩展与升级 NFT 逻辑。

## 选项 1：创建新的通用 NFT

创建一个新的通用 NFT 项目：

```
npx zetachain@latest new --project nft
```

安装依赖：

```
cd nft
yarn
forge soldeer update
```

编译合约：

```
forge build
```

## 选项 2：升级现有 ERC-721 项目

你可以通过安装官方标准合约包，将现有的 ERC-721 项目升级为通用 NFT：

```bash
yarn add @zetachain/standard-contracts
```

然后参考 [示例实现](https://github.com/zeta-chain/example-contracts/tree/main/examples/nft/contracts) 更新你的合约，查看带有通用 NFT 特定逻辑注释的部分，以便集成 ZetaChain。

这样一来，你的 NFT 将支持在 ZetaChain 与连接的 EVM 链之间进行跨链铸造、转移，并保持持久化的 Token ID。

## 部署到测试网

```
RPC_ETHEREUM=$(zetachain q chains show --chain-id 11155111 -f rpc)
RPC_BASE=$(zetachain q chains show --chain-id 84532 -f rpc)
RPC_ZETACHAIN=$(zetachain q chains show --chain-id 7001 -f rpc)

ZRC20_ETHEREUM=$(zetachain q tokens show -s ETH.ETHSEP -f zrc20)
ZRC20_BASE=$(zetachain q tokens show -s ETH.BASESEP -f zrc20)

GATEWAY_ETHEREUM=0x0c487a766110c85d301d96e33579c5b317fa4995
GATEWAY_BASE=0x0c487a766110c85d301d96e33579c5b317fa4995
GATEWAY_ZETACHAIN=0x6c533f7fe93fae114d0954697069df33c9b74fd7
UNISWAP_ROUTER=0x2ca7d64A7EFE2D62A725E2B35Cf7230D6677FfEe

GAS_LIMIT=1000000
```

```
PRIVATE_KEY=...
```

在 ZetaChain、Base 与 Ethereum 上部署合约。

```
NFT_ZETACHAIN=$(npx tsx commands deploy   --rpc $RPC_ZETACHAIN   --private-key $PRIVATE_KEY   --name ZetaChainUniversalNFT   --uniswap-router $UNISWAP_ROUTER   --gateway $GATEWAY_ZETACHAIN   --gas-limit $GAS_LIMIT | jq -r .contractAddress) && echo $NFT_ZETACHAIN
```

```
0x6335bAB2eF31B79eE01dCFDB656a1eEf5ACd0840
```

```
NFT_BASE=$(npx tsx commands deploy   --rpc $RPC_BASE   --private-key $PRIVATE_KEY   --name EVMUniversalNFT   --gateway $GATEWAY_BASE   --gas-limit $GAS_LIMIT | jq -r .contractAddress) && echo $NFT_BASE
```

```
0xB7c73Ee9B4E65458C972d64bbfAe653d0E6F389A
```

```
NFT_ETHEREUM=$(npx tsx commands deploy   --rpc $RPC_ETHEREUM   --private-key $PRIVATE_KEY   --name EVMUniversalNFT   --gateway $GATEWAY_ETHEREUM   --gas-limit $GAS_LIMIT | jq -r .contractAddress) && echo $NFT_ETHEREUM
```

```
0x166d406a3049C04bF884a4C8cfe99c5bdCebC928
```

### 连接合约

部署完成后，需要将合约互相连接，使其能够彼此信任以进行跨链通信。在 ZetaChain 上使用 `setConnected`，按 ZRC-20 Gas 代币（用于标识链）注册连接链上的合约：

```
cast send $NFT_ZETACHAIN 'setConnected(address,bytes)' $ZRC20_BASE $NFT_BASE --rpc-url $RPC_ZETACHAIN --private-key $PRIVATE_KEY
```

```
cast send $NFT_ZETACHAIN 'setConnected(address,bytes)' $ZRC20_ETHEREUM $NFT_ETHEREUM --rpc-url $RPC_ZETACHAIN --private-key $PRIVATE_KEY
```

随后，在每条连接链上使用 `setUniversal` 指向 ZetaChain 上的通用合约：

```
cast send $NFT_BASE 'setUniversal(address)' $NFT_ZETACHAIN --rpc-url $RPC_BASE --private-key $PRIVATE_KEY
```

```
cast send $NFT_ETHEREUM 'setUniversal(address)' $NFT_ZETACHAIN --rpc-url $RPC_ETHEREUM --private-key $PRIVATE_KEY
```

这能确保只有被授权的合约可以在链与链之间发送并接收 NFT 转移。

### 在 ZetaChain 上铸造

```
TOKEN_ID=$(npx tsx commands mint   --rpc $RPC_ZETACHAIN   --private-key $PRIVATE_KEY   --contract $NFT_ZETACHAIN   --token-uri https://example.com/nft/metadata/1 | jq -r .tokenId) && echo $TOKEN_ID
```

### 从 ZetaChain 转移到 Base

将该 NFT 从 ZetaChain 转移到 Base。Gas 数量（以 ZETA 指定）为估算值，未使用的部分会退还给用户。

使用 Base 的 ZRC-20 ETH 作为目标地址以指定目标链：

```
npx tsx commands transfer   --rpc $RPC_ZETACHAIN   --private-key $PRIVATE_KEY   --contract $NFT_ZETACHAIN   --token-id $TOKEN_ID   --destination $ZRC20_BASE   --gas-amount 5 | jq -r .transferTransactionHash
```

### 从 Base 转移到 Ethereum

让我们再次移动该 NFT——这一次从 Base 转移到 Ethereum。你将复用相同的 Token ID，该 ID 在各链上保持不变。

```
npx tsx commands transfer   --rpc $RPC_BASE   --private-key $PRIVATE_KEY   --contract $NFT_BASE   --token-id $TOKEN_ID   --destination $ZRC20_ETHEREUM   --gas-amount 0.05 | jq -r .transferTransactionHash
```

## 源代码

https://github.com/zeta-chain/example-contracts/tree/main/examples/nft
