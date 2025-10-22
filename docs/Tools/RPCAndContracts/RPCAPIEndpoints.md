# RPC/API 端点

用于与 ZetaChain 交互的 API 端点。

# 私有端点

如果您是开发者，我们强烈建议您通过 [AllThatNode](https://www.allthatnode.com/zetachain.dsrv)、[BlockPI](https://blockpi.io/zeta)、[InfStones](https://infstones.com/fast-api)、[Blast API](https://blastapi.io/chains/zetachain)、[dRPC](https://drpc.org/chainlist/zeta-chain-mainnet-rpc)、[Alchemy](https://www.alchemy.com/zetachain) 或其他 RPC 提供商注册免费的私有端点。私有端点具有更高的吞吐量、更少的限制，并将提供比公共 RPC 更一致的体验。

# 公共端点

以下是可用于从钱包软件或 Web 应用程序前端与 ZetaChain 交互的公共 API 端点列表。公共端点不应用于后端服务或高流量应用程序。

**主网 Beta**

| Type            | Provider     | Endpoint                                                     |
| --------------- | ------------ | ------------------------------------------------------------ |
| Cosmos SDK HTTP | Allthatnode  | https://zetachain-mainnet.g.allthatnode.com/archive/rest     |
| EVM RPC         | Allthatnode  | https://zetachain-mainnet.g.allthatnode.com/archive/evm      |
| EVM WebSocket   | Allthatnode  | wss://zetachain-mainnet.g.allthatnode.com/archive/evm        |
| Tendermint HTTP | Allthatnode  | https://zetachain-mainnet.g.allthatnode.com/archive/tendermint |
| Cosmos SDK HTTP | Blockpi      | https://zetachain.blockpi.network:443/lcd/v1/public          |
| EVM RPC         | Blockpi      | https://zetachain-evm.blockpi.network:443/v1/rpc/public      |
| Tendermint HTTP | Blockpi      | https://zetachain.blockpi.network:443/rpc/v1/public          |
| EVM RPC         | Drpc         | https://zeta-chain.drpc.org                                  |
| Cosmos SDK gRPC | F5nodes      | https://zetachain-grpc.f5nodes.com                           |
| Cosmos SDK HTTP | F5nodes      | https://zetachain-api.f5nodes.com                            |
| Tendermint RPC  | F5nodes      | https://zetachain-rpc.f5nodes.com                            |
| Cosmos SDK gRPC | Lavenderfive | https://zetachain-grpc.lavenderfive.com:443                  |
| Cosmos SDK HTTP | Lavenderfive | https://zetachain-api.lavenderfive.com:443                   |
| EVM RPC         | Lavenderfive | https://zetachain-jsonrpc.lavenderfive.com:443               |
| Tendermint RPC  | Lavenderfive | https://zetachain-rpc.lavenderfive.com:443                   |
| Cosmos SDK HTTP | Nodeshub     | https://zetachain.api.nodeshub.online:443                    |
| Tendermint RPC  | Nodeshub     | https://zetachain.rpc.nodeshub.online:443                    |

 **测试网**

| Type            | Provider    | Endpoint                                                     |
| --------------- | ----------- | ------------------------------------------------------------ |
| Cosmos SDK HTTP | Allthatnode | https://zetachain-athens.g.allthatnode.com/archive/rest      |
| EVM RPC         | Allthatnode | https://zetachain-athens.g.allthatnode.com/archive/evm       |
| Tendermint HTTP | Allthatnode | https://zetachain-athens.g.allthatnode.com/archive/tendermint |
| Cosmos SDK HTTP | Blockpi     | https://zetachain-athens.blockpi.network/lcd/v1/public       |
| EVM RPC         | Blockpi     | https://zetachain-athens.evm.blockpi.network/v1/rpc/public   |
| Tendermint RPC  | Blockpi     | https://zetachain-athens.blockpi.network/rpc/v1/public/websocket |
| EVM RPC         | Drpc        | https://zeta-chain-testnet.drpc.org                          |
| Cosmos SDK gRPC | Itrocket    | https://zetachain-testnet-grpc.itrocket.net:14090            |
| Cosmos SDK HTTP | Itrocket    | https://zetachain-testnet-api.itrocket.net                   |
| EVM RPC         | Itrocket    | https://zetachain-testnet-evm.itrocket.net                   |
| Tendermint RPC  | Itrocket    | https://zetachain-testnet-rpc.itrocket.net                   |

# EVM RPC

ZetaChain 是一个与 EVM 兼容的区块链。EVM RPC 允许您连接到 ZetaChain 区块链并与 EVM 交互。这使您能够直接读取以太坊格式的交易或将交易发送到网络。

例如，查询最新的区块号：

```shell
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' https://zetachain-athens-evm.blockpi.network/v1/rpc/public
```

# Tendermint HTTP

ZetaChain 由 Tendermint Core BFT 共识引擎驱动。Tendermint HTTP API 允许您查询区块、验证者信息、创世文件等。

例如，查询创世文件：

https://zetachain-athens.blockpi.network/rpc/v1/public/genesis

# Tendermint RPC

Tendermint RPC API 允许通过 JSON RPC 接口广播交易和查询区块链。

例如，请求特定区块：

```shell
curl --header "Content-Type: application/json" --request POST --data '{"method": "block", "params": ["3336883"], "id": 1}' https://rpc.ankr.com/zetachain_tendermint_athens_testnet
```

# Tendermint WebSocket

Tendermint WebSocket API 通过 WebSocket 提供对 JSON RPC 的访问。

例如，使用 wscat 连接到 WebSocket：

```shell
wscat -c wss://zetachain-athens.blockpi.network/rpc/v1/public/websocket
```

## Cosmos SDK HTTP

ZetaChain 是使用 Cosmos SDK 构建的。Cosmos SDK HTTP API 允许查询 ZetaChain 区块链的状态并广播交易。

例如，查询最新区块：

https://zetachain-athens.blockpi.network/lcd/v1/public//cosmos/base/tendermint/v1beta1/blocks/latest