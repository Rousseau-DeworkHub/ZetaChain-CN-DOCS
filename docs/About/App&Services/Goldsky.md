# 概览

在本教程中，您将学习如何使用 Subgraph 索引器查询全链合约事件数据。出于本教程的目的，我们将使用 [Goldsky Subgraph](https://docs.goldsky.com/introduction)。

本教程假设您已经完成了 [Swap 教程](https://www.zetachain.com/docs/developers/tutorials/swap/)。如果您想获取已完成合约的源代码，可以在 `example-contracts` 仓库中找到。

# 添加 SwapCompleted 事件

添加一个 `SwapCompleted`事件，该事件将在成功的跨链交换后触发：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.7;

import "@zetachain/protocol-contracts/contracts/zevm/SystemContract.sol";
import "@zetachain/protocol-contracts/contracts/zevm/interfaces/zContract.sol";
import "@zetachain/toolkit/contracts/SwapHelperLib.sol";
import "@zetachain/toolkit/contracts/BytesHelperLib.sol";

contract Swap is zContract {
    SystemContract public immutable systemContract;
    uint256 constant BITCOIN = 18332;

    event SwapCompleted(
        address indexed zrc20,
        address indexed targetToken,
        uint256 amount,
        bytes recipient
    );

    constructor(address systemContractAddress) {
        systemContract = SystemContract(systemContractAddress);
    }

    modifier onlySystem() {
        require(
            msg.sender == address(systemContract),
            "Only system contract can call this function"
        );
        _;
    }

    function onCrossChainCall(
        zContext calldata context,
        address zrc20,
        uint256 amount,
        bytes calldata message
    ) external virtual override onlySystem {
        address targetTokenAddress;
        bytes memory recipientAddress;

        if (context.chainID == BITCOIN) {
            targetTokenAddress = BytesHelperLib.bytesToAddress(message, 0);
            recipientAddress = abi.encodePacked(
                BytesHelperLib.bytesToAddress(message, 20)
            );
        } else {
            (address targetToken, bytes memory recipient) = abi.decode(
                message,
                (address, bytes)
            );
            targetTokenAddress = targetToken;
            recipientAddress = recipient;
        }

        (address gasZRC20, uint256 gasFee) = IZRC20(targetTokenAddress)
            .withdrawGasFee();

        uint256 inputForGas = SwapHelperLib.swapTokensForExactTokens(
            systemContract.wZetaContractAddress(),
            systemContract.uniswapv2FactoryAddress(),
            systemContract.uniswapv2Router02Address(),
            zrc20,
            gasFee,
            gasZRC20,
            amount
        );

        uint256 outputAmount = SwapHelperLib._doSwap(
            systemContract.wZetaContractAddress(),
            systemContract.uniswapv2FactoryAddress(),
            systemContract.uniswapv2Router02Address(),
            zrc20,
            amount - inputForGas,
            targetTokenAddress,
            0
        );

        IZRC20(gasZRC20).approve(targetTokenAddress, gasFee);
        IZRC20(targetTokenAddress).withdraw(recipientAddress, outputAmount);

        emit SwapCompleted(zrc20, targetTokenAddress, outputAmount, recipientAddress);
    }
}
```

# 编译和部署合约

```shell
yarn
npx hardhat compile --force
npx hardhat deploy --network zeta_testnet
```

```shell
🔑 Using account: 0x2cD3D070aE1BD365909dD859d29F387AA96911e1
🚀 Successfully deployed contract on ZetaChain.
📜 Contract address: 0x9846BBdE15B857d88DDad4e00CD76962245E1b6f
🌍 Explorer: https://zetascan.com/address/0x9846BBdE15B857d88DDad4e00CD76962245E1b6f
```

# 设置 Goldsky

安装 [Goldsky CLI：](https://docs.goldsky.com/introduction)

```shell
curl https://goldsky.com | sh
```

下一步在https://app.goldsky.com上[创建一个账户](https://docs.goldsky.com/get-started/subgraphs)，在设置页面上创建一个API key，在CLI上登录：

```shell
goldsky login
```

出现提示时粘贴您的 API 密钥。

在项目根目录创建一个 Goldsky 配置文件：

```json
{
  "version": "1",
  "name": "swap",
  "abis": {
    "swap": {
      "path": "artifacts/contracts/Swap.sol/Swap.json"
    }
  },
  "chains": ["zetachain-testnet"],
  "instances": [
    {
      "abi": "swap",
      "address": "0x9846BBdE15B857d88DDad4e00CD76962245E1b6f",
      "chain": "zetachain-testnet",
      "startBlock": 3065396
    }
  ]
}
```

请确保更新 `address`字段为您部署的合约地址，并更新 `startBlock`字段。

创建新的 Subgraph：

```shell
goldsky subgraph deploy swap/v1 --from-abi goldsky.json
```

```shell
Subgraph generated, deploying to your goldsky project
Deployed subgraph API: https://api.goldsky.com/api/public/project_clnujea22c0if34x5965c8c0j/subgraphs/swap-zetachain-testnet/v1/gn
```

# 和合约交互

现在 Subgraph 已部署，您可以通过执行跨链交换来与合约交互。在此示例中，我们将 5 个 tMATIC 交换为 BTC。

```shell
npx hardhat interact --contract 0x9846BBdE15B857d88DDad4e00CD76962245E1b6f --amount 5 --network mumbai_testnet --target-token 0x65a45c57636f9BcCeD4fe193A602008578BcA90b --recipient tb1q2dr85d57450xwde6560qyhj7zvzw9895q25tx
```

```
🔑 Using account: 0x2cD3D070aE1BD365909dD859d29F387AA96911e1
🚀 Successfully broadcasted a token transfer transaction on mumbai_testnet network.
📝 Transaction hash: 0xb4318f04329d6ddd398b11ccba40d0404e1872494a054fb382267e2f1de160e9
```

您现在可以跟踪此交易：

```
npx hardhat cctx 0xb4318f04329d6ddd398b11ccba40d0404e1872494a054fb382267e2f1de160e9
```

```
CCTXs on ZetaChain found.
✓ 0xf5fbf1ba190e074c64adaba044e2c4f6724aeebe70ca01b0998919d0b1059338: 80001 → 7001: OutboundMined (Remote omnichain contract call completed)
⠏⠏⠏ 0xa0cfd783f991bd060239193082594dd3fe5ae239e97b8baaa0a303ee6ba6ba79: 7001 → 18332: PendingOutbound
```

当您看到处于 `PendingOutbound`状态的出站跨链交易时（在上面的示例中是从 ZetaChain 到 Bitcoin，`7001 → 18332`），这意味着交换已成功执行，并且应该触发 `SwapCompleted`事件。

# 查询事件

访问部署 Subgraph 时打印的 Subgraph API URL（您的 URL 会有所不同）：

```shell
https://api.goldsky.com/api/public/project_clnujea22c0if34x5965c8c0j/subgraphs/swap-zetachain-testnet/v1/gn
```

您应该会看到一个 GraphQL playground。您可以使用它来查询事件：

```javascript
query {
  swapCompleteds(first: 5) {
    id
  }
}
```

您应该会看到一个包含 ID 的 `SwapCompleted`事件列表：

```json
{
  "data": {
    "swapCompleteds": [
      {
        "id": "0xbfcc4e8ea59625da42aa3eec6e5aba66bcd120f8e83dea8dc855ebd1d834e1e6-25"
      }
    ]
  }
}
```

您可以查询特定事件的更多信息：

```javascript
query {
  swapCompleteds(where: {id: "0xbfcc4e8ea59625da42aa3eec6e5aba66bcd120f8e83dea8dc855ebd1d834e1e6-25"}) {
    id
    block_number
    timestamp_
    transactionHash_
    contractId_
    zrc20
    targetToken
    amount
    recipient
  }
}
```

您将看到事件详细信息以及我们从合约中触发的所有数据：

```json
{
  "data": {
    "swapCompleteds": [
      {
        "id": "0xbfcc4e8ea59625da42aa3eec6e5aba66bcd120f8e83dea8dc855ebd1d834e1e6-25",
        "block_number": "3065437",
        "timestamp_": "1704357233",
        "transactionHash_": "0xbfcc4e8ea59625da42aa3eec6e5aba66bcd120f8e83dea8dc855ebd1d834e1e6",
        "contractId_": "0x9846bbde15b857d88ddad4e00cd76962245e1b6f",
        "zrc20": "0x48f80608b672dc30dc7e3dbbd0343c5f02c738eb",
        "targetToken": "0x65a45c57636f9bcced4fe193a602008578bca90b",
        "amount": "369767",
        "recipient": "0x74623171326472383564353734353078776465363536307179686a377a767a7739383935687132357478"
      }
    ]
  }
}
```

干得漂亮！您已经成功使用 Goldsky Subgraph 索引器查询了全链合约事件。要了解有关使用 Goldsky 的更多信息，请查看 [Goldsky 文档](https://docs.goldsky.com/introduction)。

# 通用问题

事件未被索引。

请等待 Goldsky 的电子邮件通知，告知您的 Subgraph 已被索引。