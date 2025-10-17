| 标题       | 描述                                                       |
| :--------- | :--------------------------------------------------------- |
| EVM 区块链 | 从 Ethereum、BNB、Polygon、Base 等链调用通用应用并存入代币 |

若要从 EVM 兼容链（如 Ethereum、BNB、Polygon 等）与通用应用交互，请使用 EVM 网关（EVM Gateway）。

EVM 网关支持以下操作：

- 将 Gas 代币存入 ZetaChain 上的通用应用或账户  
- 存入受支持的 ERC-20 代币（包括 ZETA 代币）  
- 存入 Gas 代币并调用通用应用  
- 存入受支持的 ERC-20 代币并调用通用应用  
- 直接调用通用应用  

## 存入 Gas 代币

要将代币存入外部账户（EOA）或通用合约，请调用网关合约（Gateway Contract）的 `deposit` 函数：

```solidity
deposit(address receiver, RevertOptions calldata revertOptions) external payable;
```

`deposit` 函数是 payable 的，意味着它可以接收原生 Gas 代币（例如以太坊上的 ETH），并将其发送到 ZetaChain 上的 `receiver`。`receiver` 可以是外部账户（EOA）或 ZetaChain 上的通用应用地址。即使接收方是带有标准 `receive` 函数的通用应用合约，`deposit` 函数也不会触发合约调用。如果希望在存入代币的同时调用通用应用，请使用 `depositAndCall` 函数。

存入完成后，接收方会收到存入代币的 [ZRC-20 版本](/developers/evm/zrc20)，例如 ZRC-20 ETH。

## 存入 ERC-20 代币

`deposit` 函数也可用于将受支持的 ERC-20 代币发送到 ZetaChain 上的外部账户或通用应用：

```solidity
deposit(address receiver, uint256 amount, address asset, RevertOptions calldata revertOptions) external;
```

仅可存入 [受支持的 ERC-20 资产](/developers/evm/zrc20)。接收方会收到该代币的 ZRC-20 版本（例如 ZRC-20 USDC.ETH）。

`amount` 参数指定存入数量，`asset` 为要存入的 ERC-20 代币地址。

## 存入 Gas 代币并调用通用应用

若要存入代币并调用通用应用合约，请使用 `depositAndCall` 函数：

```solidity
depositAndCall(address receiver, bytes calldata payload, RevertOptions calldata revertOptions) external payable;
```

跨链交易处理完成后，通用应用合约中的 `onCall` 函数会被执行。

`receiver` 必须是通用应用合约的地址。

```solidity
pragma solidity 0.8.26;

import "@zetachain/protocol-contracts/contracts/zevm/interfaces/UniversalContract.sol";

contract UniversalApp is UniversalContract {
    function onCall(
        MessageContext calldata context,
        address zrc20,
        uint256 amount,
        bytes calldata message
    ) external virtual override {
        // ...
    }
}
```

在 `onCall` 函数中，参数含义如下：

- `message`：传入的 `payload` 数据  
- `amount`：存入的代币数量  
- `zrc20`：所存入代币的 ZRC-20 地址（例如 ZRC-20 ETH 的合约地址）  
- `context`：  
  - `context.sender`：连接链上的发送者地址（调用网关的账户或合约）  
  - `context.chainID`：调用发起链的链 ID  

调用通用应用时，`payload` 会作为 `message` 传递给 `onCall`。无需在 payload 中包含函数选择器，因为 `onCall` 是唯一可从连接链调用的函数。

## 存入 ERC-20 代币并调用通用应用

`depositAndCall` 函数也可用于向通用应用合约发送 ERC-20 代币并调用它：

```solidity
depositAndCall(address receiver, uint256 amount, address asset, bytes calldata payload, RevertOptions calldata revertOptions) external;
```

其中 `amount` 指定存入数量，`asset` 为 ERC-20 代币地址。

当前协议版本中，一次仅可存入一种 ERC-20 资产。

## 调用通用应用

若要在不存入任何代币的情况下调用通用应用，请使用 `call` 函数：

```solidity
call(address receiver, bytes calldata payload, RevertOptions calldata revertOptions) external;
```

`call` 函数会调用指定 `receiver` 的通用合约的 `onCall` 函数，并将 `payload` 作为 `message` 参数传入。

`call` 函数不支持回退处理（revert handling）。如果 `revertOptions.callOnRevert` 被设置为 `true`，交易将失败。这是因为在执行回退时需要 ZetaChain 上的代币来支付 Gas 费用，而 `call` 函数本身不转移任何资产。如需支持回退，请使用 `depositAndCall`，并确保存入足够的代币以覆盖可能的 Gas 费用。

## 回退交易

关于 `RevertOptions` 的更多信息，请参考 [ZetaChain 回退交易](/developers/chains/zetachain#revert-transactions)。
