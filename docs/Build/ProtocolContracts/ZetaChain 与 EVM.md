# ZetaChain 与 EVM  

|标题|描述|
|:-|:-|
|ZetaChain 与 EVM |ZetaChain 与 EVM 的协议合约库文档|

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/GatewayEVM.sol)

GatewayEVM 合约是调用外部链上智能合约的端点。

*该合约不持有任何资金，且不应有任何活跃的授权额度。*

### 状态变量
#### custody
托管合约的地址。

```solidity
address public custody;
```

#### tssAddress
TSS（门限签名方案）合约的地址。

```solidity
address public tssAddress;
```

#### zetaConnector
ZetaConnector 合约的地址。

```solidity
address public zetaConnector;
```

#### zetaToken
Zeta 代币合约的地址。

```solidity
address public zetaToken;
```

#### additionalActionFeeWei
在同一笔交易内进行额外跨链操作时收取的费用。

*交易中的第一笔操作免费，后续操作将收取此费用。*

*此费用可由管理员角色配置，以允许进行费用调整。*

```solidity
uint256 public additionalActionFeeWei;
```

#### TSS_ROLE
TSS 角色的新角色标识符。

```solidity
bytes32 public constant TSS_ROLE = keccak256("TSS_ROLE");
```

#### ASSET_HANDLER_ROLE
资产处理者角色的新角色标识符。

```solidity
bytes32 public constant ASSET_HANDLER_ROLE = keccak256("ASSET_HANDLER_ROLE");
```

#### PAUSER_ROLE
暂停者角色的新角色标识符。

```solidity
bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```

#### MAX_PAYLOAD_SIZE
payload + revertOptions 回退消息的最大大小。

```solidity
uint256 public constant MAX_PAYLOAD_SIZE = 2880;
```

#### _TRANSACTION_ACTION_COUNT_KEY
用于跟踪交易操作次数的存储槽键。

*使用瞬态存储（tload/tstore）以提高 Gas 效率。*

*值 0x01 用作此存储槽的唯一标识符。*

```solidity
uint256 private constant _TRANSACTION_ACTION_COUNT_KEY = 0x01;
```

### 函数
#### constructor

**注意：**
oz-upgrades-unsafe-allow: constructor

```solidity
constructor();
```

#### initialize
使用 TSS 地址进行初始化。Zeta 代币地址和管理员账户被设置为 DEFAULT_ADMIN_ROLE。

*使用管理员来授权升级和暂停操作，使用 TSS 来担任 TSS 角色。*

```solidity
function initialize(address tssAddress_, address zetaToken_, address admin_) public initializer;
```

#### _authorizeUpgrade
*授权合约升级，发送者必须是所有者。*

```solidity
function _authorizeUpgrade(address newImplementation) internal override onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `newImplementation` | `address` | 新实现的地址。 |

#### updateTSSAddress
更新 TSS 地址。

```solidity
function updateTSSAddress(address newTSSAddress) external onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `newTSSAddress` | `address` | 新的 TSS 地址。 |

#### pause
暂停合约。

```solidity
function pause() external onlyRole(PAUSER_ROLE);
```

#### unpause
取消暂停合约。

```solidity
function unpause() external onlyRole(PAUSER_ROLE);
```

#### updateAdditionalActionFee
更新额外操作费用。

*仅可由管理员角色调用。这允许根据网络状况调整费用。*

*将费用设置为 0 将完全禁用额外操作费用。*

*应根据链的原生代币精度调整费用。*

```solidity
function updateAdditionalActionFee(uint256 newFeeWei) external onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `newFeeWei` | `uint256` | 同一交易中额外操作的新费用金额（以 wei 为单位）。 |

#### executeRevert
将 msg.value 转移到目标合约并执行其 onRevert 函数。

*此函数只能由 TSS 地址调用，并且它是 payable 的。*

```solidity
function executeRevert(
    address destination,
    bytes calldata data,
    RevertContext calldata revertContext
)
    public
    payable
    nonReentrant
    onlyRole(TSS_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `destination` | `address` | 要调用的地址。 |
| `data` | `bytes` | 传递给调用的 Calldata。 |
| `revertContext` | `RevertContext` |  |

#### execute
在不涉及 ERC20 代币的情况下执行对目标地址的调用。

*此函数只能由 TSS 地址调用，并且它是 payable 的。*

```solidity
function execute(
    MessageContext calldata messageContext,
    address destination,
    bytes calldata data
)
    external
    payable
    nonReentrant
    onlyRole(TSS_ROLE)
    whenNotPaused
    returns (bytes memory);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `messageContext` | `MessageContext` | 包含发送者的消息上下文。 |
| `destination` | `address` | 要调用的地址。 |
| `data` | `bytes` | 传递给调用的 Calldata。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `bytes` | 调用的结果。 |

#### executeWithERC20
使用 ERC20 代币执行对目标合约的调用。

*此函数只能由托管或连接器地址调用。
它使用 ERC20 授权系统，最后重置网关的授权额度。*

```solidity
function executeWithERC20(
    MessageContext calldata messageContext,
    address token,
    address to,
    uint256 amount,
    bytes calldata data
)
    public
    nonReentrant
    onlyRole(ASSET_HANDLER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `messageContext` | `MessageContext` | 包含发送者的消息上下文。 |
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 要调用的合约地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `data` | `bytes` | 传递给调用的 Calldata。 |

#### revertWithERC20
直接转移 ERC20 代币并调用 onRevert。

*此函数只能由托管或连接器地址调用。*

```solidity
function revertWithERC20(
    address token,
    address to,
    uint256 amount,
    bytes calldata data,
    RevertContext calldata revertContext
)
    external
    nonReentrant
    onlyRole(ASSET_HANDLER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 要调用的合约地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `data` | `bytes` | 传递给调用的 Calldata。 |
| `revertContext` | `RevertContext` | 传递给 onRevert 的回退上下文。 |

#### deposit
将 ETH 存入 TSS 地址。

*此函数仅对交易中的第一笔操作有效（向后兼容）。*

*对于后续操作，请使用带 amount 参数的重载版本。*

```solidity
function deposit(address receiver, RevertOptions calldata revertOptions) external payable whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### deposit
将指定数量的 ETH 存入 TSS 地址。

*msg.value 必须等于 amount + 该操作所需费用。*

```solidity
function deposit(
    address receiver,
    uint256 amount,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的 ETH 数量（不包括费用）。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### deposit
将 ERC20 代币存入托管或连接器合约。

```solidity
function deposit(
    address receiver,
    uint256 amount,
    address asset,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的代币数量。 |
| `asset` | `address` | ERC20 代币的地址。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### depositAndCall
将 ETH 存入 TSS 地址并调用全链智能合约。

*此函数仅对交易中的第一笔操作有效（向后兼容）。*

*对于后续操作，请使用带 amount 参数的重载版本。*

```solidity
function depositAndCall(
    address receiver,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `payload` | `bytes` | 传递给调用的 Calldata。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### depositAndCall
将指定数量的 ETH 存入 TSS 地址并调用全链智能合约。

*msg.value 必须等于 amount + 该操作所需费用。*

```solidity
function depositAndCall(
    address receiver,
    uint256 amount,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的 ETH 数量（不包括费用）。 |
| `payload` | `bytes` | 传递给调用的 Calldata。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### depositAndCall
将 ERC20 代币存入托管或连接器合约并调用全链智能合约。

```solidity
function depositAndCall(
    address receiver,
    uint256 amount,
    address asset,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的代币数量。 |
| `asset` | `address` | ERC20 代币的地址。 |
| `payload` | `bytes` | 传递给调用的 Calldata。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### call
在不进行资产转移的情况下调用全链智能合约。

```solidity
function call(
    address receiver,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `payload` | `bytes` | 传递给调用的 Calldata。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### setCustody
设置托管合约地址。

```solidity
function setCustody(address custody_) external onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `custody_` | `address` | 托管合约的地址。 |

#### setConnector
设置连接器合约地址。

```solidity
function setConnector(address zetaConnector_) external onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `zetaConnector_` | `address` | 连接器合约的地址。 |

#### _resetApproval
重置对指定地址的代币授权。
这用于确保在将授权设置为新值之前先将其设为零。

```solidity
function _resetApproval(address token, address to) private returns (bool);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 要重置授权的地址。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `bool` | 如果授权重置成功，或者代币在零授权时回退，则返回 True。 |

#### _transferFromToAssetHandler
*将代币从发送者转移到资产处理者。
此函数根据资产类型处理将代币转移到连接器或托管合约。*

```solidity
function _transferFromToAssetHandler(address from, address token, uint256 amount) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `from` | `address` | 发送者地址。 |
| `token` | `address` | ERC20 代币的地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |

#### _transferToAssetHandler
*将代币转移到资产处理者。
此函数根据资产类型处理将代币转移到连接器或托管合约。*

```solidity
function _transferToAssetHandler(address token, uint256 amount) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `token` | `address` | ERC20 代币的地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |

#### _executeArbitraryCall
*私有函数，用于执行对目标地址的任意调用。*

```solidity
function _executeArbitraryCall(address destination, bytes calldata data) private returns (bytes memory);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `destination` | `address` | 要调用的地址。 |
| `data` | `bytes` | 传递给调用的 Calldata。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `bytes` | 调用的结果。 |

#### _executeAuthenticatedCall
*私有函数，用于执行对目标地址的认证调用。*

```solidity
function _executeAuthenticatedCall(
    MessageContext calldata messageContext,
    address destination,
    bytes calldata data
)
    private
    returns (bytes memory);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `messageContext` | `MessageContext` | 包含发送者和任意调用标志的消息上下文。 |
| `destination` | `address` | 要调用的地址。 |
| `data` | `bytes` | 传递给调用的 Calldata。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `bytes` | 调用的结果。 |

#### _revertIfOnCallOrOnRevert

```solidity
function _revertIfOnCallOrOnRevert(bytes calldata data) private pure;
```

#### _processFee
处理交易内跨链操作的费用收取。

*交易中的第一笔操作免费，后续操作将收取 ADDITIONAL_ACTION_FEE_WEI。*

*如果费用为 0，则整个功能被禁用并将回退。*

```solidity
function _processFee() internal returns (uint256);
```
**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `uint256` | 实际收取的费用金额（第一笔操作为 0，后续操作为 ADDITIONAL_ACTION_FEE_WEI）。 |

#### _validateChargedFeeForERC20
验证 ERC20 操作（deposit、depositAndCall、call）的费用支付。

*验证 msg.value 是否等于所需费用（不允许有额外的 ETH）。*

```solidity
function _validateChargedFeeForERC20(uint256 feeCharged) internal view;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `feeCharged` | `uint256` | 已收取的费用金额。 |

#### _validateChargedFeeForETHWithAmount
验证带指定数量的 ETH 操作的费用支付。

*验证 msg.value 是否等于 amount + feeCharged。*

```solidity
function _validateChargedFeeForETHWithAmount(uint256 amount, uint256 feeCharged) internal view;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `amount` | `uint256` | 要存入的数量（不包括费用）。 |
| `feeCharged` | `uint256` | 已收取的费用金额。 |

#### _getNextActionIndex
使用瞬态存储获取并递增交易操作计数器。

*使用汇编以通过 tload/tstore 操作提高 Gas 效率。*

*瞬态存储是交易作用域的，并在每笔交易后自动清除。*

```solidity
function _getNextActionIndex() internal returns (uint256 currentIndex);
```
**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `currentIndex` | `uint256` | 交易中当前的操作索引（从 0 开始）。 |

## GatewayZEVM

[Git 源码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/GatewayZEVM.sol)

GatewayZEVM 合约是在全链上调用智能合约的端点。

*该合约不持有任何资金，并且永远不应拥有活跃的授权额度。*

### 状态变量

#### PROTOCOL_ADDRESS
协议的常量地址。

```solidity
address public constant PROTOCOL_ADDRESS = 0x735b14BB79463307AAcBED86DAf3322B1e6226aB;
```

#### PAUSER_ROLE
暂停者角色的新角色标识符。

```solidity
bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```

#### zetaToken
ZETA 代币的地址。

```solidity
address public zetaToken;
```

#### registry
ZetaChain 上注册表合约的地址。

```solidity
address public registry;
```

### 函数

#### onlyProtocol

*仅允许协议地址的修饰符。*

```solidity
modifier onlyProtocol();
```

#### constructor

**注意：**
oz-upgrades-unsafe-allow: constructor

```solidity
constructor();
```

#### initialize

使用 ZETA 代币地址和设置为 DEFAULT_ADMIN_ROLE 的管理员账户进行初始化。

*使用管理员来授权升级和暂停操作。*

```solidity
function initialize(address zetaToken_, address admin_) public initializer;
```

#### _authorizeUpgrade

*授权合约的升级。*

```solidity
function _authorizeUpgrade(address newImplementation) internal override onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `newImplementation` | `address` | 新实现的地址。 |

#### receive

*接收函数，用于从 `WETH9.withdraw()` 接收 ZETA。*

```solidity
receive() external payable whenNotPaused;
```

#### pause

暂停合约。

```solidity
function pause() external onlyRole(PAUSER_ROLE);
```

#### unpause

取消暂停合约。

```solidity
function unpause() external onlyRole(PAUSER_ROLE);
```

#### setRegistryAddress

设置注册表地址，仅可由 DEFAULT_ADMIN_ROLE 调用。

```solidity
function setRegistryAddress(address _registry) external onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `_registry` | `address` | 注册表合约的地址。 |

#### _safeTransferFrom

安全执行 `transferFrom` 的辅助函数。

```solidity
function _safeTransferFrom(address zrc20, address from, address to, uint256 amount) private returns (bool);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `zrc20` | `address` | ZRC20 代币地址 |
| `from` | `address` | 发送方地址 |
| `to` | `address` | 接收方地址 |
| `amount` | `uint256` | 要转移的数量 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `bool` | 如果转移成功则为 true，否则为 false。 |

#### _safeBurn

```solidity
function _safeBurn(address zrc20, uint256 amount) private returns (bool);
```

#### _safeDeposit

```solidity
function _safeDeposit(address zrc20, address target, uint256 amount) private returns (bool);
```

#### _burnProtocolFees

燃烧 Gas 费的辅助函数。

```solidity
function _burnProtocolFees(address gasZRC20, uint256 gasFee) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `gasZRC20` | `address` | Gas ZRC20 代币的地址。 |
| `gasFee` | `uint256` | 应燃烧的 `gasZRC20` 数量。 |

#### _burnZRC20ProtocolFees

用于 ZRC20 提款的燃烧 Gas 费的辅助函数。

```solidity
function _burnZRC20ProtocolFees(address zrc20, uint256 gasLimit) private returns (uint256);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `gasLimit` | `uint256` | Gas 限制。 |

#### _withdrawZRC20WithGasLimit

*使用 Gas 限制提取 ZRC20 代币的私有函数。*

```solidity
function _withdrawZRC20WithGasLimit(uint256 amount, address zrc20, uint256 gasLimit) private returns (uint256);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `amount` | `uint256` | 要提取的代币数量。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `gasLimit` | `uint256` | Gas 限制。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `uint256` | 提款的 Gas 费。 |

#### _getGasLimitForZETATransfer

*获取向外部链转移 ZETA 的 Gas 限制的辅助函数。*

```solidity
function _getGasLimitForZETATransfer(uint256 chainId) private view returns (uint256 gasLimit);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 外部链的链 ID。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `gasLimit` | `uint256` | Gas 限制。 |

#### _getProtocolFlatFeeFromRegistry

*从注册表获取外部链的协议固定费用的辅助函数。*

```solidity
function _getProtocolFlatFeeFromRegistry(uint256 chainId) private view returns (uint256 protocolFlatFee);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 外部链的链 ID。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `protocolFlatFee` | `uint256` | 协议固定费用。 |

#### _computeAndPayFeesForZETAWithdrawals

*计算并支付 ZETA 提款的 Gas 费的辅助函数。*

```solidity
function _computeAndPayFeesForZETAWithdrawals(
    uint256 chainId,
    uint256 gasLimit
)
    private
    returns (uint256 gasFee, uint256 protocolFlatFee, uint256 gasLimit_);
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 外部链的链 ID。 |
| `gasLimit` | `uint256` | Gas 限制。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `gasFee` | `uint256` | 提款的 Gas 费。 |
| `protocolFlatFee` | `uint256` | 协议固定费用。 |
| `gasLimit_` | `uint256` | 用于提款的 Gas 限制。 |

#### _transferZETA

*转移 ZETA 代币的私有函数。*

```solidity
function _transferZETA(uint256 amount, address to) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `amount` | `uint256` | 要转移的代币数量。 |
| `to` | `address` | 接收代币的地址。 |

#### withdraw

将 ZRC20 代币提取到外部链。

```solidity
function withdraw(
    bytes memory receiver,
    uint256 amount,
    address zrc20,
    RevertOptions calldata revertOptions
)
    external
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### withdraw

使用自定义 Gas 限制将 ZRC20 代币提取到外部链。

*使用此函数进行简单的 Gas ZRC20 提款，目标是智能合约账户或具有自定义接收/回退实现的智能合约。*

```solidity
function withdraw(
    bytes memory receiver,
    uint256 amount,
    address zrc20,
    uint256 gasLimit,
    RevertOptions calldata revertOptions
)
    external
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `gasLimit` | `uint256` | 提款的自定义 Gas 限制（必须 >= `MIN_GAS_LIMIT`）。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### withdrawAndCall

提取 ZRC20 代币并在外部链上调用智能合约。

```solidity
function withdrawAndCall(
    bytes memory receiver,
    uint256 amount,
    address zrc20,
    bytes calldata message,
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions
)
    external
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |
| `callOptions` | `CallOptions` | 调用选项，包括 Gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### withdraw

将 ZETA 代币提取到外部链。

```solidity
function withdraw(
    bytes memory receiver,
    uint256 chainId,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused
    nonReentrant;
```

#### withdrawAndCall

提取 ZETA 代币并在外部链上调用智能合约。

```solidity
function withdrawAndCall(
    bytes memory receiver,
    uint256 chainId,
    bytes calldata message,
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions
)
    external
    payable
    whenNotPaused
    nonReentrant;
```

#### call

在不转移资产的情况下调用外部链上的智能合约。

```solidity
function call(
    bytes memory receiver,
    address zrc20,
    bytes calldata message,
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions
)
    external
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `zrc20` | `address` | 用于支付费用的 zrc20 地址。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |
| `callOptions` | `CallOptions` | 调用选项，包括 Gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### _call

```solidity
function _call(
    bytes memory receiver,
    address zrc20,
    bytes calldata message,
    CallOptions memory callOptions,
    RevertOptions memory revertOptions
)
    private;
```

#### deposit

将外部币存入 ZRC20。

```solidity
function deposit(address zrc20, uint256 amount, address target) external onlyProtocol whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要存入的代币数量。 |
| `target` | `address` | 接收存入代币的目标地址。 |

#### deposit

存入原生 ZETA。

```solidity
function deposit(address target) external payable nonReentrant onlyProtocol whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `target` | `address` | 接收 ZETA 的目标地址。 |

#### execute

在 ZEVM 上执行用户指定的合约。

```solidity
function execute(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    address target,
    bytes calldata message
)
    external
    nonReentrant
    onlyProtocol
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `context` | `MessageContext` | 跨链调用的上下文。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `target` | `address` | 要调用的目标合约。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |

#### depositAndCall

将外部币存入 ZRC20 并在 ZEVM 上调用用户指定的合约。

```solidity
function depositAndCall(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    address target,
    bytes calldata message
)
    external
    nonReentrant
    onlyProtocol
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `context` | `MessageContext` | 跨链调用的上下文。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `target` | `address` | 要调用的目标合约。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |

#### depositAndCall

存入原生 ZETA 并在 ZEVM 上调用用户指定的合约。

```solidity
function depositAndCall(
    MessageContext calldata context,
    address target,
    bytes calldata message
)
    external
    payable
    nonReentrant
    onlyProtocol
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `context` | `MessageContext` | 跨链调用的上下文。 |
| `target` | `address` | 要调用的目标合约。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |

#### executeRevert

在 ZEVM 上回退用户指定的合约。

```solidity
function executeRevert(
    address target,
    RevertContext calldata revertContext
)
    external
    nonReentrant
    onlyProtocol
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `target` | `address` | 要调用的目标合约。 |
| `revertContext` | `RevertContext` | 传递给 `onRevert` 的回退上下文。 |

#### depositAndRevert

将外部币存入 ZRC20 并在 ZEVM 上回退用户指定的合约。

```solidity
function depositAndRevert(
    address zrc20,
    uint256 amount,
    address target,
    RevertContext calldata revertContext
)
    external
    nonReentrant
    onlyProtocol
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要回退的代币数量。 |
| `target` | `address` | 要调用的目标合约。 |
| `revertContext` | `RevertContext` | 传递给 `onRevert` 的回退上下文。 |

#### depositAndRevert

存入原生 ZETA 并在 ZEVM 上回退用户指定的合约。

```solidity
function depositAndRevert(
    address target,
    RevertContext calldata revertContext
)
    external
    payable
    nonReentrant
    onlyProtocol
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `target` | `address` | 要调用的目标合约。 |
| `revertContext` | `RevertContext` | 传递给 `onRevert` 的回退上下文。 |

#### executeAbort

在 ZEVM 上调用用户指定合约的 `onAbort`。
此函数不会将资产存入目标合约。此操作直接由协议完成。
即使 `onAbort` 回退，资产也会存入目标合约。

```solidity
function executeAbort(
    address target,
    AbortContext calldata abortContext
)
    external
    nonReentrant
    onlyProtocol
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `target` | `address` | 要调用的目标合约。 |
| `abortContext` | `AbortContext` | 传递给 `onAbort` 的中止上下文。 |

#### getMaxMessageSize

返回最大消息大小。

```solidity
function getMaxMessageSize() external pure returns (uint256);
```
**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `uint256` | 最大消息大小。 |

#### getMinGasLimit

返回允许的最小 Gas 限制。

```solidity
function getMinGasLimit() external pure returns (uint256);
```
**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `uint256` | 最小 Gas 限制。 |

#### getMaxRevertGasLimit

返回允许的最大回退 Gas 限制。

```solidity
function getMaxRevertGasLimit() external pure returns (uint256);
```
**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `uint256` | 最大回退 Gas 限制。 |

## INotSupportedMethods

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Errors.sol)

包含不支持方法的合约接口。

### 错误
#### CallOnRevertNotSupported

```solidity
error CallOnRevertNotSupported();
```

## ERC20Custody

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/ERC20Custody.sol)

持有在 ZetaChain 上存入的 ERC20 代币，并包含调用合约的功能。

*此合约不直接调用智能合约，而是通过 Gateway 合约传递。*

### 状态变量
#### gateway
Gateway 合约。

```solidity
IGatewayEVM public gateway;
```

#### whitelisted
白名单代币的映射 => true/false。

```solidity
mapping(address => bool) public whitelisted;
```

#### tssAddress
TSS（阈值签名方案）合约的地址。

```solidity
address public tssAddress;
```

#### supportsLegacy
用于标记合约是否支持旧版方法（例如 deposit）。

```solidity
bool public supportsLegacy;
```

#### PAUSER_ROLE
暂停者角色的新角色标识符。

```solidity
bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```

#### WITHDRAWER_ROLE
提取者角色的新角色标识符。

```solidity
bytes32 public constant WITHDRAWER_ROLE = keccak256("WITHDRAWER_ROLE");
```

#### WHITELISTER_ROLE
白名单管理者角色的新角色标识符。

```solidity
bytes32 public constant WHITELISTER_ROLE = keccak256("WHITELISTER_ROLE");
```

### 函数
#### initialize
ERC20Custody 的初始化函数。

*将管理员设置为默认管理员和暂停者，并将 tssAddress 设置为 TSS 角色。*

```solidity
function initialize(address gateway_, address tssAddress_, address admin_) public initializer;
```

#### _authorizeUpgrade
*授权合约升级，发送者必须为所有者。*

```solidity
function _authorizeUpgrade(address newImplementation) internal override onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`newImplementation`|`address`|新实现的地址。|

#### pause
暂停合约。

```solidity
function pause() external onlyRole(PAUSER_ROLE);
```

#### unpause
取消暂停合约。

```solidity
function unpause() external onlyRole(PAUSER_ROLE);
```

#### updateTSSAddress
更新 TSS 地址。

```solidity
function updateTSSAddress(address newTSSAddress) external onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`newTSSAddress`|`address`|新的 TSS 地址。|

#### setSupportsLegacy
取消暂停合约。

```solidity
function setSupportsLegacy(bool _supportsLegacy) external onlyRole(DEFAULT_ADMIN_ROLE);
```

#### whitelist
将 ERC20 代币加入白名单。

```solidity
function whitelist(address token) external onlyRole(WHITELISTER_ROLE);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`token`|`address`|ERC20 代币的地址。|

#### unwhitelist
将 ERC20 代币从白名单中移除。

```solidity
function unwhitelist(address token) external onlyRole(WHITELISTER_ROLE);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`token`|`address`|ERC20 代币的地址。|

#### withdraw
直接提取代币到目标地址，不进行合约调用。

*此函数只能由 TSS 地址调用。*

```solidity
function withdraw(
    address to,
    address token,
    uint256 amount
)
    external
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`to`|`address`|代币的目标地址。|
|`token`|`address`|ERC20 代币的地址。|
|`amount`|`uint256`|要提取的代币数量。|

#### withdrawAndCall
提取代币到 Gateway 并通过 Gateway 调用合约。

*此函数只能由 TSS 地址调用。*

```solidity
function withdrawAndCall(
    MessageContext calldata messageContext,
    address to,
    address token,
    uint256 amount,
    bytes calldata data
)
    public
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`messageContext`|`MessageContext`|包含发送者的消息上下文。|
|`to`|`address`|要调用的合约地址。|
|`token`|`address`|ERC20 代币的地址。|
|`amount`|`uint256`|要提取的代币数量。|
|`data`|`bytes`|传递给合约调用的调用数据。|

#### withdrawAndRevert
提取代币到 Gateway 并通过 Gateway 调用具有回滚功能的合约。

*此函数只能由 TSS 地址调用。*

```solidity
function withdrawAndRevert(
    address to,
    address token,
    uint256 amount,
    bytes calldata data,
    RevertContext calldata revertContext
)
    public
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`to`|`address`|要调用的合约地址。|
|`token`|`address`|ERC20 代币的地址。|
|`amount`|`uint256`|要提取的代币数量。|
|`data`|`bytes`|传递给合约调用的调用数据。|
|`revertContext`|`RevertContext`|传递给 onRevert 的回滚上下文。|

#### deposit
将资产存入托管并以 zeta erc20 支付费用。

**注意：**
已弃用：此方法已弃用。

```solidity
function deposit(
    bytes calldata recipient,
    IERC20 asset,
    uint256 amount,
    bytes calldata message
)
    external
    nonReentrant
    whenNotPaused;
```

## IERC20Custody

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IERC20Custody.sol)

### 函数

#### whitelisted

白名单代币映射 => true/false。

```solidity
function whitelisted(address token) external view returns (bool);
```

#### withdraw

直接提现，将代币直接转移到目标地址，无需合约调用。

*此函数只能由 TSS 地址调用。*

```solidity
function withdraw(address token, address to, uint256 amount) external;
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 接收代币的目标地址。 |
| `amount` | `uint256` | 要提现的代币数量。 |

#### withdrawAndCall

提现并调用，将代币转移到 Gateway 并通过 Gateway 调用合约。

*此函数只能由 TSS 地址调用。*

```solidity
function withdrawAndCall(
    MessageContext calldata messageContext,
    address token,
    address to,
    uint256 amount,
    bytes calldata data
)
    external;
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `messageContext` | `MessageContext` | 包含发送者信息的消息上下文。 |
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 要调用的合约地址。 |
| `amount` | `uint256` | 要提现的代币数量。 |
| `data` | `bytes` | 传递给合约调用的 Calldata。 |

#### withdrawAndRevert

提现并回退，将代币转移到 Gateway 并通过 Gateway 调用具有回退功能的合约。

*此函数只能由 TSS 地址调用。*

```solidity
function withdrawAndRevert(
    address token,
    address to,
    uint256 amount,
    bytes calldata data,
    RevertContext calldata revertContext
)
    external;
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 要调用的合约地址。 |
| `amount` | `uint256` | 要提现的代币数量。 |
| `data` | `bytes` | 传递给合约调用的 Calldata。 |
| `revertContext` | `RevertContext` | 传递给 onRevert 的回退上下文。 |

## IERC20CustodyErrors

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IERC20Custody.sol)

用于 ERC20 托管合约中的错误的接口。

### 错误

#### ZeroAddress

零地址输入的错误。

```solidity
error ZeroAddress();
```

#### NotWhitelisted

未列入白名单的 ERC20 代币的错误。

```solidity
error NotWhitelisted();
```

#### LegacyMethodsNotSupported

调用不受支持的旧版方法的错误。

```solidity
error LegacyMethodsNotSupported();
```

## IERC20CustodyEvents

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IERC20Custody.sol)

ERC20 托管合约发出的事件接口。

### 事件
#### Withdrawn
当代币被提取时发出。

```solidity
event Withdrawn(address indexed to, address indexed token, uint256 amount);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`to`|`address`|接收代币的地址。|
|`token`|`address`|ERC20 代币的地址。|
|`amount`|`uint256`|提取的代币数量。|

#### WithdrawnAndCalled
当代币被提取并执行合约调用时发出。

```solidity
event WithdrawnAndCalled(address indexed to, address indexed token, uint256 amount, bytes data);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`to`|`address`|接收代币的地址。|
|`token`|`address`|ERC20 代币的地址。|
|`amount`|`uint256`|提取的代币数量。|
|`data`|`bytes`|传递给合约调用的调用数据。|

#### WithdrawnAndReverted
当代币被提取并执行可回滚合约调用时发出。

```solidity
event WithdrawnAndReverted(
    address indexed to, address indexed token, uint256 amount, bytes data, RevertContext revertContext
);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`to`|`address`|接收代币的地址。|
|`token`|`address`|ERC20 代币的地址。|
|`amount`|`uint256`|提取的代币数量。|
|`data`|`bytes`|传递给合约调用的调用数据。|
|`revertContext`|`RevertContext`|传递给 onRevert 的回滚上下文。|

#### Whitelisted
当 ERC20 代币被加入白名单时发出。

```solidity
event Whitelisted(address indexed token);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`token`|`address`|ERC20 代币的地址。|

#### Unwhitelisted
当 ERC20 代币被移出白名单时发出。

```solidity
event Unwhitelisted(address indexed token);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`token`|`address`|ERC20 代币的地址。|

#### Deposited
在旧版存款方法中发出。

```solidity
event Deposited(bytes recipient, IERC20 indexed asset, uint256 amount, bytes message);
```

#### UpdatedCustodyTSSAddress
当 TSS 地址更新时发出。

```solidity
event UpdatedCustodyTSSAddress(address oldTSSAddress, address newTSSAddress);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`oldTSSAddress`|`address`|旧的 TSS 地址。|
|`newTSSAddress`|`address`|新的 TSS 地址。|

## Callable

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IGatewayEVM.sol)

接收认证调用的合约所实现的接口。

### 函数
#### onCall

```solidity
function onCall(MessageContext calldata context, bytes calldata message) external payable returns (bytes memory);
```

## IGatewayEVM

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IGatewayEVM.sol)

GatewayEVM 合约的接口。

### 函数

#### executeWithERC20

使用 ERC20 代币执行对合约的调用。

```solidity
function executeWithERC20(
    MessageContext calldata messageContext,
    address token,
    address to,
    uint256 amount,
    bytes calldata data
)
    external;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `messageContext` | `MessageContext` | 包含发送者和任意调用标志的消息上下文。 |
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 要调用的合约地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `data` | `bytes` | 传递给合约调用的调用数据。 |

#### executeRevert

将 `msg.value` 转移至目标合约并执行其 `onRevert` 函数。

*此函数只能由 TSS 地址调用，并且是可支付函数。*

```solidity
function executeRevert(
    address destination,
    bytes calldata data,
    RevertContext calldata revertContext
)
    external
    payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `destination` | `address` | 要调用的地址。 |
| `data` | `bytes` | 传递给调用的调用数据。 |
| `revertContext` | `RevertContext` | 传递给 `onRevert` 的回滚上下文。 |

#### execute

在没有 ERC20 代币的情况下执行对目标地址的调用。

*此函数只能由 TSS 地址调用，并且是可支付函数。*

```solidity
function execute(
    MessageContext calldata messageContext,
    address destination,
    bytes calldata data
)
    external
    payable
    returns (bytes memory);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `messageContext` | `MessageContext` | 包含发送者和任意调用标志的消息上下文。 |
| `destination` | `address` | 要调用的地址。 |
| `data` | `bytes` | 传递给调用的调用数据。 |

**返回值**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<无>` | `bytes` | 调用的结果。 |

#### revertWithERC20

使用 ERC20 代币执行一个可回滚的合约调用。

```solidity
function revertWithERC20(
    address token,
    address to,
    uint256 amount,
    bytes calldata data,
    RevertContext calldata revertContext
)
    external;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 要调用的合约地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `data` | `bytes` | 传递给合约调用的调用数据。 |
| `revertContext` | `RevertContext` | 传递给 `onRevert` 的回滚上下文。 |

#### deposit

向 TSS 地址存入 ETH。

```solidity
function deposit(address receiver, RevertOptions calldata revertOptions) external payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `revertOptions` | `RevertOptions` | 回滚选项。 |

#### deposit

向 TSS 地址存入指定数量的 ETH。

```solidity
function deposit(address receiver, uint256 amount, RevertOptions calldata revertOptions) external payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的 ETH 数量。 |
| `revertOptions` | `RevertOptions` | 回滚选项。 |

#### deposit

向托管或连接器合约存入 ERC20 代币。

```solidity
function deposit(
    address receiver,
    uint256 amount,
    address asset,
    RevertOptions calldata revertOptions
)
    external
    payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的代币数量。 |
| `asset` | `address` | ERC20 代币的地址。 |
| `revertOptions` | `RevertOptions` | 回滚选项。 |

#### depositAndCall

向 TSS 地址存入 ETH 并调用全链智能合约。

```solidity
function depositAndCall(
    address receiver,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    external
    payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `payload` | `bytes` | 传递给调用的调用数据。 |
| `revertOptions` | `RevertOptions` | 回滚选项。 |

#### depositAndCall

向 TSS 地址存入指定数量的 ETH 并调用全链智能合约。

```solidity
function depositAndCall(
    address receiver,
    uint256 amount,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    external
    payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的 ETH 数量。 |
| `payload` | `bytes` | 传递给调用的调用数据。 |
| `revertOptions` | `RevertOptions` | 回滚选项。 |

#### depositAndCall

向托管或连接器合约存入 ERC20 代币并调用全链智能合约。

```solidity
function depositAndCall(
    address receiver,
    uint256 amount,
    address asset,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    external
    payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 要存入的代币数量。 |
| `asset` | `address` | ERC20 代币的地址。 |
| `payload` | `bytes` | 传递给调用的调用数据。 |
| `revertOptions` | `RevertOptions` | 回滚选项。 |

#### call

在没有资产转移的情况下调用全链智能合约。

```solidity
function call(address receiver, bytes calldata payload, RevertOptions calldata revertOptions) external payable;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `address` | 接收者地址。 |
| `payload` | `bytes` | 传递给调用的调用数据。 |
| `revertOptions` | `RevertOptions` | 回滚选项。 |

## IGatewayEVMErrors

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IGatewayEVM.sol)

GatewayEVM 合约中使用的错误的接口。

### 错误
#### ExecutionFailed
执行失败时的错误。

```solidity
error ExecutionFailed();
```

#### DepositFailed
存款失败时的错误。

```solidity
error DepositFailed();
```

#### InsufficientEVMAmount
代币数量不足时的错误。

```solidity
error InsufficientEVMAmount();
```

#### ZeroAddress
输入为零地址时的错误。

```solidity
error ZeroAddress();
```

#### ApprovalFailed
代币授权失败时的错误。

```solidity
error ApprovalFailed(address token, address spender);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`token`|`address`|授权失败的代币地址。|
|`spender`|`address`|本应被授权花费代币的地址。|

#### CustodyInitialized
托管已初始化时的错误。

```solidity
error CustodyInitialized();
```

#### ConnectorInitialized
连接器已初始化时的错误。

```solidity
error ConnectorInitialized();
```

#### NotWhitelistedInCustody
尝试向托管转移非白名单代币时的错误。

```solidity
error NotWhitelistedInCustody(address token);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`token`|`address`|未在托管中白名单的代币地址。|

#### NotAllowedToCallOnCall
尝试通过任意调用调用 onCall 方法时的错误。

```solidity
error NotAllowedToCallOnCall();
```

#### NotAllowedToCallOnRevert
尝试通过任意调用调用 onRevert 方法时的错误。

```solidity
error NotAllowedToCallOnRevert();
```

#### PayloadSizeExceeded
外部函数中载荷大小超限时的错误。

```solidity
error PayloadSizeExceeded(uint256 provided, uint256 maximum);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`provided`|`uint256`|提供的载荷大小。|
|`maximum`|`uint256`|允许的最大载荷大小。|

#### FeeTransferFailed
向 TSS 地址转账费用失败时抛出的错误。

*此错误在底层调用转账费用失败时发生。*

```solidity
error FeeTransferFailed();
```

#### InsufficientFee
为附加操作提供的费用不足时抛出的错误。

```solidity
error InsufficientFee(uint256 required, uint256 provided);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`required`|`uint256`|操作所需的费用金额。|
|`provided`|`uint256`|调用者实际提供的费用金额。|

#### ExcessETHProvided
为非 ETH 操作发送过量 ETH 时抛出的错误。

```solidity
error ExcessETHProvided(uint256 required, uint256 provided);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`required`|`uint256`|操作所需的费用金额。|
|`provided`|`uint256`|调用者实际提供的 ETH 金额。|

#### AdditionalActionDisabled
附加操作功能被禁用（费用设置为 0）时抛出的错误。

```solidity
error AdditionalActionDisabled();
```

#### IncorrectValueProvided
msg.value 与预期金额加费用不匹配时抛出的错误。

```solidity
error IncorrectValueProvided(uint256 expected, uint256 provided);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`expected`|`uint256`|预期值（金额 + 费用）。|
|`provided`|`uint256`|实际提供的 msg.value。|

## IGatewayEVMEvents

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IGatewayEVM.sol)

GatewayEVM 合约发出的事件接口。

### 事件
#### Executed
当合约调用被执行时发出。

```solidity
event Executed(address indexed destination, uint256 value, bytes data);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `destination` | `address` | 被调用合约的地址。 |
| `value` | `uint256` | 调用时发送的 ETH 数量。 |
| `data` | `bytes` | 传递给合约调用的 calldata。 |

#### Reverted
当合约调用被回退时发出。

```solidity
event Reverted(address indexed to, address indexed token, uint256 amount, bytes data, RevertContext revertContext);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `to` | `address` | 被调用合约的地址。 |
| `token` | `address` | ERC20 代币的地址，如果是 gas 代币则为空 |
| `amount` | `uint256` | 调用时发送的 ETH 数量。 |
| `data` | `bytes` | 传递给合约调用的 calldata。 |
| `revertContext` | `RevertContext` | 要传递给 onRevert 的回退上下文。 |

#### ExecutedWithERC20
当使用 ERC20 代币的合约调用被执行时发出。

```solidity
event ExecutedWithERC20(address indexed token, address indexed to, uint256 amount, bytes data);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `token` | `address` | ERC20 代币的地址。 |
| `to` | `address` | 被调用合约的地址。 |
| `amount` | `uint256` | 转移的代币数量。 |
| `data` | `bytes` | 传递给合约调用的 calldata。 |

#### Deposited
当进行存款操作时发出。

```solidity
event Deposited(
    address indexed sender,
    address indexed receiver,
    uint256 amount,
    address asset,
    bytes payload,
    RevertOptions revertOptions
);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `sender` | `address` | 发送者地址。 |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 存入的 ETH 或代币数量。 |
| `asset` | `address` | ERC20 代币的地址（如果是 ETH 则为零地址）。 |
| `payload` | `bytes` | 随存款传递的 calldata。不再使用。为保持兼容性而保留。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### DepositedAndCalled
当进行存款并调用操作时发出。

```solidity
event DepositedAndCalled(
    address indexed sender,
    address indexed receiver,
    uint256 amount,
    address asset,
    bytes payload,
    RevertOptions revertOptions
);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `sender` | `address` | 发送者地址。 |
| `receiver` | `address` | 接收者地址。 |
| `amount` | `uint256` | 存入的 ETH 或代币数量。 |
| `asset` | `address` | ERC20 代币的地址（如果是 ETH 则为零地址）。 |
| `payload` | `bytes` | 随存款传递的 calldata。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### Called
当进行无资产转移的全链智能合约调用时发出。

```solidity
event Called(address indexed sender, address indexed receiver, bytes payload, RevertOptions revertOptions);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `sender` | `address` | 发送者地址。 |
| `receiver` | `address` | 接收者地址。 |
| `payload` | `bytes` | 传递给调用的 calldata。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### UpdatedGatewayTSSAddress
当 tss 地址更新时发出。

```solidity
event UpdatedGatewayTSSAddress(address oldTSSAddress, address newTSSAddress);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `oldTSSAddress` | `address` | 旧的 tss 地址 |
| `newTSSAddress` | `address` | 新的 tss 地址 |

#### UpdatedAdditionalActionFee

```solidity
event UpdatedAdditionalActionFee(uint256 oldFeeWei, uint256 newFeeWei);
```

## MessageContext

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IGatewayEVM.sol)

传递给 execute 函数的消息上下文。

```solidity
struct MessageContext {
    address sender;
}
```

**属性**

| 名称     | 类型      | 描述                         |
|----------|-----------|------------------------------|
| `sender` | `address` | 来自 omnichain 合约的发送者。 |

## IRegistry

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IRegistry.sol)

### 结构体

#### ChainMetadataEntry

用于引导过程中的元数据条目结构

```solidity
struct ChainMetadataEntry {
    uint256 chainId;
    string key;
    bytes value;
}
```

#### ContractConfigEntry

用于引导过程中的合约配置条目结构

```solidity
struct ContractConfigEntry {
    uint256 chainId;
    string contractType;
    string key;
    bytes value;
}
```

## IZetaConnectorEvents

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IZetaConnector.sol)

ZetaConnector 合约发出的事件的接口。

### 事件

#### Withdrawn
当代币被提取时发出。

```solidity
event Withdrawn(address indexed to, uint256 amount);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `to` | `address` | 代币被提取到的地址。 |
| `amount` | `uint256` | 提取的代币数量。 |

#### WithdrawnAndCalled
当代币被提取并调用合约时发出。

```solidity
event WithdrawnAndCalled(address indexed to, uint256 amount, bytes data);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `to` | `address` | 代币被提取到的地址。 |
| `amount` | `uint256` | 提取的代币数量。 |
| `data` | `bytes` | 传递给合约调用的调用数据。 |

#### WithdrawnAndReverted
当代币被提取并调用合约且带有回退回调时发出。

```solidity
event WithdrawnAndReverted(address indexed to, uint256 amount, bytes data, RevertContext revertContext);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `to` | `address` | 代币被提取到的地址。 |
| `amount` | `uint256` | 提取的代币数量。 |
| `data` | `bytes` | 传递给合约调用的调用数据。 |
| `revertContext` | `RevertContext` | 传递给 onRevert 的回退上下文。 |

#### UpdatedZetaConnectorTSSAddress
当 TSS 地址更新时发出。

```solidity
event UpdatedZetaConnectorTSSAddress(address oldTSSAddress, address newTSSAddress);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `oldTSSAddress` | `address` | 旧的 TSS 地址。 |
| `newTSSAddress` | `address` | 新的 TSS 地址。 |

## IZetaNonEthNew

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/interfaces/IZetaNonEthNew.sol)

IZetaNonEthNew 是 IERC20 的可铸造/可销毁版本。

### 函数
#### burnFrom

从指定账户销毁指定数量的代币。

*触发一个 {Transfer} 事件，其中 `to` 设置为零地址。*

```solidity
function burnFrom(address account, uint256 amount) external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`account`|`address`|从中销毁代币的账户地址。|
|`amount`|`uint256`|要销毁的代币数量。|

#### mint

向指定账户铸造指定数量的代币。

*触发一个 {Transfer} 事件，其中 `from` 设置为零地址。*

```solidity
function mint(address mintee, uint256 value, bytes32 internalSendHash) external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`mintee`|`address`|接收铸造代币的账户地址。|
|`value`|`uint256`|要铸造的代币数量。|
|`internalSendHash`|`bytes32`|用于内部跟踪铸造交易的哈希值。|

## ConnectorErrors

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ConnectorErrors.sol)

*连接器自定义错误的接口*

### 错误
#### CallerIsNotPauser

```solidity
error CallerIsNotPauser(address caller);
```

#### CallerIsNotTss

```solidity
error CallerIsNotTss(address caller);
```

#### CallerIsNotTssUpdater

```solidity
error CallerIsNotTssUpdater(address caller);
```

#### CallerIsNotTssOrUpdater

```solidity
error CallerIsNotTssOrUpdater(address caller);
```

#### ZetaTransferError

```solidity
error ZetaTransferError();
```

#### ExceedsMaxSupply

```solidity
error ExceedsMaxSupply(uint256 maxSupply);
```

## IZetaNonEthInterface

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/IZetaNonEthInterface.sol)

*IZetaNonEthInterface.sol 是 IERC20 的一个可铸造 / 可销毁版本。*


### 函数
#### burnFrom


```solidity
function burnFrom(address account, uint256 amount) external;
```

#### mint


```solidity
function mint(address mintee, uint256 value, bytes32 internalSendHash) external;
```

## ZetaConnectorBase

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaConnector.base.sol)

*ZetaConnector 的主要抽象。该合约管理 TSS 与不同链之间的交互。在 ZetaChain 支持的每个链上都有此合约的一个实例。*

### 状态变量
#### zetaToken

```solidity
address public immutable zetaToken;
```

#### pauserAddress
*用于暂停传入交易的多签合约。暂停传出交易的责任留给协议以提供更多灵活性。*

```solidity
address public pauserAddress;
```

#### tssAddress
*由 ZetaChain 验证者集体持有。*

```solidity
address public tssAddress;
```

#### tssAddressUpdater
*此地址最初将指向一个多签合约，随后将变更为 TSS 地址本身。*

```solidity
address public tssAddressUpdater;
```

### 函数
#### constructor

*构造函数需要初始地址。zetaToken 地址是唯一不可变的，而其他地址可以更新。*

```solidity
constructor(address zetaToken_, address tssAddress_, address tssAddressUpdater_, address pauserAddress_);
```

#### onlyPauser

*修饰符，限制仅允许 pauser 地址执行操作。*

```solidity
modifier onlyPauser();
```

#### onlyTssAddress

*修饰符，限制仅允许 TSS 地址执行操作。*

```solidity
modifier onlyTssAddress();
```

#### onlyTssUpdater

*修饰符，限制仅允许 TSS 更新者地址执行操作。*

```solidity
modifier onlyTssUpdater();
```

#### updatePauserAddress

*更新 pauser 地址。唯一允许执行此操作的地址是当前的 pauser。*

```solidity
function updatePauserAddress(address pauserAddress_) external onlyPauser;
```

#### updateTssAddress

*更新 TSS 地址。此地址可由 TSS 更新者或 TSS 地址本身更新。*

```solidity
function updateTssAddress(address tssAddress_) external;
```

#### renounceTssAddressUpdater

*将 tssAddressUpdater 的所有权变更为由 ZetaChain TSS 签名节点持有。*

```solidity
function renounceTssAddressUpdater() external onlyTssUpdater;
```

#### pause

*暂停输入（发送）交易。*

```solidity
function pause() external onlyPauser;
```

#### unpause

*取消暂停合约以重新允许交易。*

```solidity
function unpause() external onlyPauser;
```

#### send

*通过 ZetaChain 发送数据和价值的入口点。*

```solidity
function send(ZetaInterfaces.SendInput calldata input) external virtual;
```

#### onReceive

*接收来自其他链数据的处理程序。此方法仅可由 TSS 调用。访问验证在实现中处理。*

```solidity
function onReceive(
    bytes calldata zetaTxSenderAddress,
    uint256 sourceChainId,
    address destinationAddress,
    uint256 zetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    virtual;
```

#### onRevert

*接收来自其他链错误的处理程序。此方法仅可由 TSS 调用。访问验证在实现中处理。*

```solidity
function onRevert(
    address zetaTxSenderAddress,
    uint256 sourceChainId,
    bytes calldata destinationAddress,
    uint256 destinationChainId,
    uint256 remainingZetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    virtual;
```

### 事件
#### ZetaSent

```solidity
event ZetaSent(
    address sourceTxOriginAddress,
    address indexed zetaTxSenderAddress,
    uint256 indexed destinationChainId,
    bytes destinationAddress,
    uint256 zetaValueAndGas,
    uint256 destinationGasLimit,
    bytes message,
    bytes zetaParams
);
```

#### ZetaReceived

```solidity
event ZetaReceived(
    bytes zetaTxSenderAddress,
    uint256 indexed sourceChainId,
    address indexed destinationAddress,
    uint256 zetaValue,
    bytes message,
    bytes32 indexed internalSendHash
);
```

#### ZetaReverted

```solidity
event ZetaReverted(
    address zetaTxSenderAddress,
    uint256 sourceChainId,
    uint256 indexed destinationChainId,
    bytes destinationAddress,
    uint256 remainingZetaValue,
    bytes message,
    bytes32 indexed internalSendHash
);
```

#### TSSAddressUpdated

```solidity
event TSSAddressUpdated(address callerAddress, address newTssAddress);
```

#### TSSAddressUpdaterUpdated

```solidity
event TSSAddressUpdaterUpdated(address callerAddress, address newTssUpdaterAddress);
```

#### PauserAddressUpdated

```solidity
event PauserAddressUpdated(address callerAddress, address newTssAddress);
```

## ZetaConnectorEth

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaConnector.eth.sol)

*ZetaConnector 的 ETH 实现。此合约管理 TSS 与不同链之间的交互。此版本仅适用于以太坊网络，因为在其他链上我们进行铸造和销毁，而在此链上我们进行锁定和解锁。*

### 函数
#### constructor

```solidity
constructor(
    address zetaToken_,
    address tssAddress_,
    address tssAddressUpdater_,
    address pauserAddress_
)
    ZetaConnectorBase(zetaToken_, tssAddress_, tssAddressUpdater_, pauserAddress_);
```

#### getLockedAmount

```solidity
function getLockedAmount() external view returns (uint256);
```

#### send

*通过 ZetaChain 发送数据的入口点。此调用将代币锁定在合约上，并发出包含协议所需所有数据的事件。*

```solidity
function send(ZetaInterfaces.SendInput calldata input) external override whenNotPaused;
```

#### onReceive

*从其他链接收数据的处理程序。此方法只能由 TSS 调用。将 Zeta 代币转移到目的地，并在需要时调用 onZetaMessage。*

```solidity
function onReceive(
    bytes calldata zetaTxSenderAddress,
    uint256 sourceChainId,
    address destinationAddress,
    uint256 zetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    override
    onlyTssAddress;
```

#### onRevert

*从其他链接收错误的处理程序。此方法只能由 TSS 调用。将 Zeta 代币转移到目的地，并在需要时调用 onZetaRevert。*

```solidity
function onRevert(
    address zetaTxSenderAddress,
    uint256 sourceChainId,
    bytes calldata destinationAddress,
    uint256 destinationChainId,
    uint256 remainingZetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    override
    whenNotPaused
    onlyTssAddress;
```

## ZetaConnectorNonEth

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaConnector.non-eth.sol)

*ZetaConnector 的非 ETH 实现。此合约管理 TSS 与不同链之间的交互。此版本适用于除以太坊网络外的所有链，因为在其他链上我们进行铸币和销毁，而在以太坊上我们进行锁定和解锁。*

### 状态变量
#### maxSupply

```solidity
uint256 public maxSupply = 2 ** 256 - 1;
```

### 函数
#### constructor

```solidity
constructor(
    address zetaTokenAddress_,
    address tssAddress_,
    address tssAddressUpdater_,
    address pauserAddress_
)
    ZetaConnectorBase(zetaTokenAddress_, tssAddress_, tssAddressUpdater_, pauserAddress_);
```

#### getLockedAmount

```solidity
function getLockedAmount() external view returns (uint256);
```

#### setMaxSupply

```solidity
function setMaxSupply(uint256 maxSupply_) external onlyTssAddress;
```

#### send

*发送数据到协议的入口点。此调用会销毁代币并发出一个事件，包含协议所需的所有数据。*

```solidity
function send(ZetaInterfaces.SendInput calldata input) external override whenNotPaused;
```

#### onReceive

*从其他链接收数据的处理程序。此方法只能由 TSS 调用。将 Zeta 代币转移到目标地址，并在需要时调用 onZetaMessage。为了执行转移，会铸造新代币，首先验证当前链允许的最大供应量。*

```solidity
function onReceive(
    bytes calldata zetaTxSenderAddress,
    uint256 sourceChainId,
    address destinationAddress,
    uint256 zetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    override
    onlyTssAddress;
```

#### onRevert

*从其他链接收错误的处理程序。此方法只能由 TSS 调用。将 Zeta 代币转移到目标地址，并在需要时调用 onZetaRevert。为了执行转移，会铸造新代币，首先验证当前链允许的最大供应量。*

```solidity
function onRevert(
    address zetaTxSenderAddress,
    uint256 sourceChainId,
    bytes calldata destinationAddress,
    uint256 destinationChainId,
    uint256 remainingZetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    override
    whenNotPaused
    onlyTssAddress;
```

### 事件
#### MaxSupplyUpdated

```solidity
event MaxSupplyUpdated(address callerAddress, uint256 newMaxSupply);
```

## ZetaErrors

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaErrors.sol)

*常见自定义错误*

### 错误
#### CallerIsNotTss

```solidity
error CallerIsNotTss(address caller);
```

#### CallerIsNotConnector

```solidity
error CallerIsNotConnector(address caller);
```

#### CallerIsNotTssUpdater

```solidity
error CallerIsNotTssUpdater(address caller);
```

#### CallerIsNotTssOrUpdater

```solidity
error CallerIsNotTssOrUpdater(address caller);
```

#### InvalidAddress

```solidity
error InvalidAddress();
```

#### ZetaTransferError

```solidity
error ZetaTransferError();
```

## ZetaEth

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaEth.sol)

以太坊是 ZETA 代币部署的起源和原生链（原生）

*ZetaEth.sol 是 OpenZeppelin ERC20 的一个实现*

### 函数
#### 构造函数

```solidity
constructor(address creator, uint256 initialSupply);
```

## ZetaCommonErrors

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaInterfaces.sol)

### 错误

#### InvalidAddress

```solidity
error InvalidAddress();
```

## ZetaConnector

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaInterfaces.sol)

### 函数
#### send

*只需调用 `connector.send(SendInput)` 即可轻松实现跨链发送数值和数据*

```solidity
function send(ZetaInterfaces.SendInput calldata input) external;
```

## ZetaInterfaces

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaInterfaces.sol)

### 结构体

#### SendInput
*使用 SendInput 与连接器交互：connector.send(SendInput)*

```solidity
struct SendInput {
    uint256 destinationChainId;
    bytes destinationAddress;
    uint256 destinationGasLimit;
    bytes message;
    uint256 zetaValueAndGas;
    bytes zetaParams;
}
```

#### ZetaMessage
*我们的连接器使用此结构体作为参数调用 onZetaMessage*

```solidity
struct ZetaMessage {
    bytes zetaTxSenderAddress;
    uint256 sourceChainId;
    address destinationAddress;
    uint256 zetaValue;
    bytes message;
}
```

#### ZetaRevert
*我们的连接器使用此结构体作为参数调用 onZetaRevert*

```solidity
struct ZetaRevert {
    address zetaTxSenderAddress;
    uint256 sourceChainId;
    bytes destinationAddress;
    uint256 destinationChainId;
    uint256 remainingZetaValue;
    bytes message;
}
```

## ZetaReceiver

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaInterfaces.sol)

### 函数
#### onZetaMessage

*当跨链消息到达合约时，会调用 onZetaMessage*

```solidity
function onZetaMessage(ZetaInterfaces.ZetaMessage calldata zetaMessage) external;
```

#### onZetaRevert

*当跨链消息回退时，会调用 onZetaRevert。它对于回滚到原始状态非常有用*

```solidity
function onZetaRevert(ZetaInterfaces.ZetaRevert calldata zetaRevert) external;
```

## ZetaTokenConsumer

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaInterfaces.sol)

*ZetaTokenConsumer 让以下场景的处理变得更加简单：
- 使用原生币获取 Zeta（在使用 `connector.send` 时用于支付目标链 gas 费用）
- 使用代币获取 Zeta（在使用 `connector.send` 时用于支付目标链 gas 费用）
- 使用 Zeta 获取原生币（在执行 `onZetaRevert` 时返还未使用的目标链 gas）
- 使用 Zeta 获取代币（在执行 `onZetaRevert` 时返还未使用的目标链 gas）*

*该接口可以通过不同的策略来实现，例如 UniswapV2、UniswapV3 等*

### 函数
#### getZetaFromEth

```solidity
function getZetaFromEth(address destinationAddress, uint256 minAmountOut) external payable returns (uint256);
```

#### getZetaFromToken

```solidity
function getZetaFromToken(
    address destinationAddress,
    uint256 minAmountOut,
    address inputToken,
    uint256 inputTokenAmount
)
    external
    returns (uint256);
```

#### getEthFromZeta

```solidity
function getEthFromZeta(
    address destinationAddress,
    uint256 minAmountOut,
    uint256 zetaTokenAmount
)
    external
    returns (uint256);
```

#### getTokenFromZeta

```solidity
function getTokenFromZeta(
    address destinationAddress,
    uint256 minAmountOut,
    address outputToken,
    uint256 zetaTokenAmount
)
    external
    returns (uint256);
```

#### hasZetaLiquidity

```solidity
function hasZetaLiquidity() external view returns (bool);
```

### 事件
#### EthExchangedForZeta

```solidity
event EthExchangedForZeta(uint256 amountIn, uint256 amountOut);
```

#### TokenExchangedForZeta

```solidity
event TokenExchangedForZeta(address token, uint256 amountIn, uint256 amountOut);
```

#### ZetaExchangedForEth

```solidity
event ZetaExchangedForEth(uint256 amountIn, uint256 amountOut);
```

#### ZetaExchangedForToken

```solidity
event ZetaExchangedForToken(address token, uint256 amountIn, uint256 amountOut);
```

## ZetaNonEth

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/legacy/ZetaNonEth.sol)

在非原生（非 Ethereum）链上，ZETA 代币在初始部署于 Ethereum 后被铸造和销毁。

### 状态变量
#### connectorAddress

```solidity
address public connectorAddress;
```

#### tssAddress
*由 Zeta 区块链验证者集体持有*

```solidity
address public tssAddress;
```

#### tssAddressUpdater
*最初是一个多签地址，最终由 Zeta 区块链验证者持有（通过 renounceTssAddressUpdater）*

```solidity
address public tssAddressUpdater;
```

### 函数
#### constructor

```solidity
constructor(address tssAddress_, address tssAddressUpdater_) ERC20("Zeta", "ZETA");
```

#### updateTssAndConnectorAddresses

```solidity
function updateTssAndConnectorAddresses(address tssAddress_, address connectorAddress_) external;
```

#### renounceTssAddressUpdater
*将 tssAddressUpdater 设置为 tssAddress*

```solidity
function renounceTssAddressUpdater() external;
```

#### mint

```solidity
function mint(address mintee, uint256 value, bytes32 internalSendHash) external override;
```

#### burnFrom

```solidity
function burnFrom(address account, uint256 amount) public override(IZetaNonEthInterface, ERC20Burnable);
```

### 事件
#### Minted

```solidity
event Minted(address indexed mintee, uint256 amount, bytes32 indexed internalSendHash);
```

#### Burnt

```solidity
event Burnt(address indexed burnee, uint256 amount);
```

#### TSSAddressUpdated

```solidity
event TSSAddressUpdated(address callerAddress, address newTssAddress);
```

#### TSSAddressUpdaterUpdated

```solidity
event TSSAddressUpdaterUpdated(address callerAddress, address newTssUpdaterAddress);
```

#### ConnectorAddressUpdated

```solidity
event ConnectorAddressUpdated(address callerAddress, address newConnectorAddress);
```

## GatewayEVMValidations

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/libraries/GatewayEVMValidations.sol)

包含 GatewayEVM 合约验证函数的库。

*该库提供在 GatewayEVM 合约中使用的通用验证逻辑。*

### 状态变量
#### MAX_PAYLOAD_SIZE
最大载荷大小常量。

```solidity
uint256 internal constant MAX_PAYLOAD_SIZE = 2880;
```

### 函数
#### validateNonZeroAddress

*验证地址不为零。*

```solidity
function validateNonZeroAddress(address addr) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`addr`|`address`|要验证的地址。|

#### validateAmount

*验证金额不为零。*

```solidity
function validateAmount(uint256 amount) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`amount`|`uint256`|要验证的金额。|

#### validatePayloadSize

*验证载荷大小约束。*

```solidity
function validatePayloadSize(uint256 payloadLength, uint256 revertMessageLength) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`payloadLength`|`uint256`|主载荷的长度。|
|`revertMessageLength`|`uint256`|回滚消息的长度。|

#### validateGasLimitRevertOptions

*验证回滚燃料限制。*

```solidity
function validateGasLimitRevertOptions(RevertOptions calldata revertOptions) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`revertOptions`|`RevertOptions`|要验证的回滚选项。|

#### validateRevertMessageLength

*验证回滚消息长度。*

```solidity
function validateRevertMessageLength(RevertOptions calldata revertOptions) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`revertOptions`|`RevertOptions`|要验证的回滚选项。|

#### validateCallRevertOptions

*验证调用操作的回滚选项（包括 callOnRevert 检查）。*

```solidity
function validateCallRevertOptions(RevertOptions calldata revertOptions) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`revertOptions`|`RevertOptions`|要验证的回滚选项。|

#### validateDepositParams

*验证标准存款参数。*

```solidity
function validateDepositParams(address receiver, uint256 amount, RevertOptions calldata revertOptions) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`receiver`|`address`|接收者地址。|
|`amount`|`uint256`|要存款的金额。|
|`revertOptions`|`RevertOptions`|回滚选项。|

#### validateDepositAndCallParams

*验证存款和调用参数。*

```solidity
function validateDepositAndCallParams(
    address receiver,
    uint256 amount,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    internal
    pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`receiver`|`address`|接收者地址。|
|`amount`|`uint256`|要存款的金额。|
|`payload`|`bytes`|要发送的载荷。|
|`revertOptions`|`RevertOptions`|回滚选项。|

#### validateCallParams

*验证调用参数。*

```solidity
function validateCallParams(
    address receiver,
    bytes calldata payload,
    RevertOptions calldata revertOptions
)
    internal
    pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`receiver`|`address`|接收者地址。|
|`payload`|`bytes`|要发送的载荷。|
|`revertOptions`|`RevertOptions`|回滚选项。|

## Registry

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/Registry.sol)

用于连接链的卫星注册表合约，从 CoreRegistry 接收更新。

*该合约部署在每个连接链上，并维护注册表的同步视图。*

### 状态变量

#### GATEWAY_ROLE
网关角色的标识符

```solidity
bytes32 public constant GATEWAY_ROLE = keccak256("GATEWAY_ROLE");
```

#### gatewayEVM
将从 CoreRegistry 接收消息并调用此合约的 GatewayEVM 合约

```solidity
IGatewayEVM public gatewayEVM;
```

#### coreRegistry
代表 ZetaChain 上 CoreRegistry 合约的地址

```solidity
address public coreRegistry;
```

### 函数

#### onlyRegistry

限制函数调用仅能由本合约自身发起

*仅允许注册表地址的修饰符。*

*这用于确保接收跨链消息的函数只能通过 onCall 函数使用自调用模式调用，防止直接外部调用这些函数*

```solidity
modifier onlyRegistry();
```

#### initialize

初始化 Registry 合约

```solidity
function initialize(
    address admin_,
    address registryManager_,
    address gatewayEVM_,
    address coreRegistry_
)
    public
    initializer;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `admin_` | `address` | 具有 DEFAULT_ADMIN_ROLE 的地址，授权执行升级和暂停操作 |
| `registryManager_` | `address` | 具有 REGISTRY_MANAGER_ROLE 的地址，授权执行所有注册表写入操作 |
| `gatewayEVM_` | `address` | 用于跨链消息传递的 GatewayEVM 合约地址 |
| `coreRegistry_` | `address` | 部署在 ZetaChain 上的 CoreRegistry 合约地址 |

#### onCall

当接收到跨链消息时，由 GatewayEVM 调用 onCall 函数

```solidity
function onCall(
    MessageContext calldata context,
    bytes calldata data
)
    external
    onlyRole(GATEWAY_ROLE)
    whenNotPaused
    returns (bytes memory);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `context` | `MessageContext` | 关于跨链消息的信息 |
| `data` | `bytes` | 要执行的编码函数调用 |

#### changeChainStatus

将链的状态更改为激活/停用

*仅可通过来自 CoreRegistry 的 onCall 调用*

```solidity
function changeChainStatus(
    uint256 chainId,
    address gasZRC20,
    bytes calldata registry,
    bool activation
)
    external
    onlyRegistry
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `chainId` | `uint256` | 被激活/停用的链 ID |
| `gasZRC20` | `address` | 代表该链 gas 代币的 ZRC20 代币地址 |
| `registry` | `bytes` | 连接链上 Registry 合约的地址 |
| `activation` | `bool` | 是否激活该链 |

#### updateChainMetadata

更新链元数据，仅适用于活跃链

*仅可通过来自 CoreRegistry 的 onCall 调用*

```solidity
function updateChainMetadata(
    uint256 chainId,
    string calldata key,
    bytes calldata value
)
    external
    onlyRegistry
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `chainId` | `uint256` | 链 ID |
| `key` | `string` | 要更新的元数据键 |
| `value` | `bytes` | 元数据的新值 |

#### registerContract

为特定链注册新的合约地址

*仅可通过来自 CoreRegistry 的 onCall 调用*

```solidity
function registerContract(
    uint256 chainId,
    string calldata contractType,
    bytes calldata addressBytes
)
    external
    onlyRegistry
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `chainId` | `uint256` | 合约部署所在链的 ID |
| `contractType` | `string` | 合约类型（例如 "connector"、"gateway"） |
| `addressBytes` | `bytes` | 合约地址 |

#### updateContractConfiguration

更新合约配置

*仅可通过来自 CoreRegistry 的 onCall 调用*

```solidity
function updateContractConfiguration(
    uint256 chainId,
    string calldata contractType,
    string calldata key,
    bytes calldata value
)
    external
    onlyRegistry
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `chainId` | `uint256` | 合约部署所在链的 ID |
| `contractType` | `string` | 合约类型 |
| `key` | `string` | 要更新的配置键 |
| `value` | `bytes` | 配置的新值 |

#### setContractActive

设置合约的活跃状态

*仅可通过来自 CoreRegistry 的 onCall 调用*

```solidity
function setContractActive(uint256 chainId, string calldata contractType, bool active) external onlyRegistry;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `chainId` | `uint256` | 合约部署所在链的 ID |
| `contractType` | `string` | 合约类型 |
| `active` | `bool` | 合约是否应处于活跃状态 |

#### registerZRC20Token

在注册表中注册新的 ZRC20 代币

*仅可通过来自 CoreRegistry 的 onCall 调用*

```solidity
function registerZRC20Token(
    address address_,
    string calldata symbol,
    uint256 originChainId,
    bytes calldata originAddress,
    string calldata coinType,
    uint8 decimals
)
    external
    onlyRegistry
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `address_` | `address` | ZetaChain 上 ZRC20 代币的地址 |
| `symbol` | `string` | 代币符号 |
| `originChainId` | `uint256` | 原始资产所在外部链的 ID |
| `originAddress` | `bytes` | 资产在其原生链上的地址或标识符 |
| `coinType` | `string` | 原始代币类型 |
| `decimals` | `uint8` | 代币使用的小数位数 |

#### setZRC20TokenActive

更新 ZRC20 代币的活跃状态

*仅可通过来自 CoreRegistry 的 onCall 调用*

```solidity
function setZRC20TokenActive(address address_, bool active) external onlyRegistry whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `address_` | `address` | ZRC20 代币地址 |
| `active` | `bool` | 代币是否应处于活跃状态 |

#### bootstrapChains

使用链数据引导注册表

*此函数只能由具有 REGISTRY_MANAGER_ROLE 的地址调用*

```solidity
function bootstrapChains(
    ChainInfoDTO[] calldata chains,
    ChainMetadataEntry[] calldata metadataEntries
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `chains` | `ChainInfoDTO[]` | 要引导的链数据结构数组 |
| `metadataEntries` | `ChainMetadataEntry[]` | 链元数据条目数组 |

#### bootstrapContracts

使用合约数据引导注册表

*此函数只能由具有 REGISTRY_MANAGER_ROLE 的地址调用*

```solidity
function bootstrapContracts(
    ContractInfoDTO[] calldata contracts,
    ContractConfigEntry[] calldata configEntries
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `contracts` | `ContractInfoDTO[]` | 要引导的合约数据结构数组 |
| `configEntries` | `ContractConfigEntry[]` | 合约配置条目数组 |

#### bootstrapZRC20Tokens

使用 ZRC20 代币数据引导注册表

*此函数只能由具有 REGISTRY_MANAGER_ROLE 的地址调用*

```solidity
function bootstrapZRC20Tokens(ZRC20Info[] calldata tokens) external onlyRole(REGISTRY_MANAGER_ROLE) whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `tokens` | `ZRC20Info[]` | 要引导的 ZRC20 代币数据结构数组 |

## ZetaConnectorBase

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/ZetaConnectorBase.sol)

ZetaConnector 的抽象基础合约。

*该合约实现了处理代币和与 Gateway 合约交互的基本功能。*

### 状态变量
#### gateway
用于执行跨链调用的 Gateway 合约。

```solidity
IGatewayEVM public gateway;
```

#### zetaToken
Zeta 代币的地址。

```solidity
address public zetaToken;
```

#### tssAddress
TSS（阈值签名方案）合约的地址。

```solidity
address public tssAddress;
```

#### WITHDRAWER_ROLE
取款者角色的新角色标识符。

```solidity
bytes32 public constant WITHDRAWER_ROLE = keccak256("WITHDRAWER_ROLE");
```

#### PAUSER_ROLE
暂停者角色的新角色标识符。

```solidity
bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```

#### TSS_ROLE
tss 角色的新角色标识符。

```solidity
bytes32 public constant TSS_ROLE = keccak256("TSS_ROLE");
```

### 函数
#### constructor

**注意：** oz-upgrades-unsafe-allow: constructor

```solidity
constructor();
```

#### initialize

ZetaConnectors 的初始化器。

*将 admin 设置为默认管理员和暂停者，并将 tssAddress 设置为 tss 角色。*

```solidity
function initialize(
    address gateway_,
    address zetaToken_,
    address tssAddress_,
    address admin_
)
    public
    virtual
    onlyInitializing;
```

#### _authorizeUpgrade

*授权合约升级，发送者必须拥有所有者权限。*

```solidity
function _authorizeUpgrade(address newImplementation) internal override onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`newImplementation`|`address`|新实现的地址。|

#### updateTSSAddress

更新 tss 地址。

```solidity
function updateTSSAddress(address newTSSAddress) external onlyRole(DEFAULT_ADMIN_ROLE);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`newTSSAddress`|`address`|新的 tss 地址。|

#### pause

暂停合约。

```solidity
function pause() external onlyRole(PAUSER_ROLE);
```

#### unpause

取消暂停合约。

```solidity
function unpause() external onlyRole(PAUSER_ROLE);
```

#### deposit

处理接收到的代币。

```solidity
function deposit(uint256 amount) external virtual;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`amount`|`uint256`|接收到的代币数量。|

### 错误
#### ZeroAddress
表示提供了零地址的错误。

```solidity
error ZeroAddress();
```

## ZetaConnectorNative

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/ZetaConnectorNative.sol)

ZetaConnectorBase 的实现，用于原生代币处理。

*该合约直接转移 Zeta 代币并与 Gateway 合约交互。*

### 函数
#### initialize

ZetaConnectorNative 的初始化器。

```solidity
function initialize(
    address gateway_,
    address zetaToken_,
    address tssAddress_,
    address admin_
)
    public
    override
    initializer;
```

#### withdraw

提取代币到指定地址。

*此函数只能由 TSS 地址调用。*

```solidity
function withdraw(address to, uint256 amount) external nonReentrant onlyRole(WITHDRAWER_ROLE) whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `to` | `address` | 提取代币的目标地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |

#### withdrawAndCall

提取代币并通过 Gateway 调用合约。

*此函数只能由 TSS 地址调用。*

```solidity
function withdrawAndCall(
    MessageContext calldata messageContext,
    address to,
    uint256 amount,
    bytes calldata data
)
    external
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `messageContext` | `MessageContext` | 包含发送者的消息上下文。 |
| `to` | `address` | 提取代币的目标地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `data` | `bytes` | 传递给合约调用的 calldata。 |

#### withdrawAndRevert

提取代币并通过 Gateway 调用合约，附带回退回调。

*此函数只能由 TSS 地址调用。*

```solidity
function withdrawAndRevert(
    address to,
    uint256 amount,
    bytes calldata data,
    RevertContext calldata revertContext
)
    external
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `to` | `address` | 提取代币的目标地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `data` | `bytes` | 传递给合约调用的 calldata。 |
| `revertContext` | `RevertContext` | 传递给 onRevert 的回退上下文。 |

#### deposit

处理接收到的代币。

```solidity
function deposit(uint256 amount) external override whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `amount` | `uint256` | 接收到的代币数量。 |

## ZetaConnectorNonNative

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/evm/ZetaConnectorNonNative.sol)

用于处理非原生代币的 ZetaConnectorBase 实现。

*此合约铸造和销毁 Zeta 代币，并与 Gateway 合约交互。*

### 状态变量
#### maxSupply
铸造的最大供应量。

```solidity
uint256 public maxSupply;
```

### 函数
#### initialize

ZetaConnectorNonNative 的初始化函数。

```solidity
function initialize(
    address gateway_,
    address zetaToken_,
    address tssAddress_,
    address admin_
)
    public
    override
    initializer;
```

#### setMaxSupply

设置铸造的最大供应量。

*此函数只能由 TSS 地址调用。*

```solidity
function setMaxSupply(uint256 maxSupply_) external onlyRole(TSS_ROLE) whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `maxSupply_` | `uint256` | 新的最大供应量。 |

#### withdraw

将代币提取到指定地址。

*此函数只能由 TSS 地址调用。*

```solidity
function withdraw(
    address to,
    uint256 amount,
    bytes32 internalSendHash
)
    external
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `to` | `address` | 接收提取代币的地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `internalSendHash` | `bytes32` | 用于内部跟踪交易记录的哈希值。 |

#### withdrawAndCall

提取代币并通过 Gateway 调用合约。

*此函数只能由 TSS 地址调用，并且在未达到供应量上限时会进行铸造。*

```solidity
function withdrawAndCall(
    MessageContext calldata messageContext,
    address to,
    uint256 amount,
    bytes calldata data,
    bytes32 internalSendHash
)
    external
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `messageContext` | `MessageContext` | 包含发送者信息的消息上下文。 |
| `to` | `address` | 接收提取代币的地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `data` | `bytes` | 传递给合约调用的调用数据。 |
| `internalSendHash` | `bytes32` | 用于内部跟踪交易记录的哈希值。 |

#### withdrawAndRevert

提取代币并通过 Gateway 调用合约，附带一个 revert 回调。

*此函数只能由 TSS 地址调用，并且在未达到供应量上限时会进行铸造。*

```solidity
function withdrawAndRevert(
    address to,
    uint256 amount,
    bytes calldata data,
    bytes32 internalSendHash,
    RevertContext calldata revertContext
)
    external
    nonReentrant
    onlyRole(WITHDRAWER_ROLE)
    whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `to` | `address` | 接收提取代币的地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `data` | `bytes` | 传递给合约调用的调用数据。 |
| `internalSendHash` | `bytes32` | 用于内部跟踪交易记录的哈希值。 |
| `revertContext` | `RevertContext` | 传递给 `onRevert` 的 revert 上下文。 |

#### deposit

处理接收到的代币并将其销毁。

```solidity
function deposit(uint256 amount) external override whenNotPaused;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `amount` | `uint256` | 接收到的代币数量。 |

#### _mintTo

*铸造代币到指定账户，并检查是否会超过总供应量*

```solidity
function _mintTo(address to, uint256 amount, bytes32 internalSendHash) private;
```

### 事件
#### MaxSupplyUpdated
当最大供应量更新时触发的事件。

```solidity
event MaxSupplyUpdated(uint256 maxSupply);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `maxSupply` | `uint256` | 新的最大供应量。 |

### 错误
#### ExceedsMaxSupply

```solidity
error ExceedsMaxSupply();
```

## BaseRegistry

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/BaseRegistry.sol)

### 状态变量

#### PAUSER_ROLE
暂停者角色的新角色标识符。

```solidity
bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```

#### REGISTRY_MANAGER_ROLE
注册表管理器角色的新角色标识符。

```solidity
bytes32 public constant REGISTRY_MANAGER_ROLE = keccak256("REGISTRY_MANAGER_ROLE");
```

#### admin
具有 `DEFAULT_ADMIN_ROLE` 的地址，被授权进行升级和暂停操作。

```solidity
address public admin;
```

#### registryManager
具有 `REGISTRY_MANAGER_ROLE` 的地址，被授权执行所有注册表写入操作。

```solidity
address public registryManager;
```

#### _activeChains
注册表中的活跃链。

```solidity
uint256[] internal _activeChains;
```

#### _allChains
注册表中所有链 ID 的数组（包括活跃和非活跃链）。

```solidity
uint256[] internal _allChains;
```

#### _allContracts
用于存储所有合约的数组，以链 ID 和合约类型对的形式。

```solidity
ContractIdentifier[] internal _allContracts;
```

#### _allZRC20Addresses
所有 ZRC20 代币地址的数组。

```solidity
address[] internal _allZRC20Addresses;
```

#### _chains
将链 ID 映射到其信息。

```solidity
mapping(uint256 => ChainInfo) internal _chains;
```

#### _contracts
映射关系：链 ID -> 合约类型 -> ContractInfo

```solidity
mapping(uint256 => mapping(string => ContractInfo)) internal _contracts;
```

#### _zrc20Tokens
将 ZRC20 代币地址映射到其信息。

```solidity
mapping(address => ZRC20Info) internal _zrc20Tokens;
```

#### _zrc20SymbolToAddress
将代币符号映射到 ZRC20 地址。

```solidity
mapping(string => address) internal _zrc20SymbolToAddress;
```

#### _originAssetToZRC20
将原始链 ID 和原始地址映射到 ZRC20 代币地址。

```solidity
mapping(uint256 => mapping(bytes => address)) internal _originAssetToZRC20;
```

### 函数

#### constructor

**注意：**
oz-upgrades-unsafe-allow: constructor

```solidity
constructor();
```

#### _authorizeUpgrade

*授权合约升级，发送者必须为管理员。*

```solidity
function _authorizeUpgrade(address newImplementation) internal override onlyRole(DEFAULT_ADMIN_ROLE);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `newImplementation` | `address` | 新实现的地址。 |

#### pause

暂停合约。

```solidity
function pause() external onlyRole(PAUSER_ROLE);
```

#### unpause

取消暂停合约。

```solidity
function unpause() external onlyRole(DEFAULT_ADMIN_ROLE);
```

#### changeAdmin

更改管理员地址并转移 `DEFAULT_ADMIN_ROLE` 和 `PAUSER_ROLE`。

*仅可由当前管理员调用。*

```solidity
function changeAdmin(address newAdmin) external onlyRole(DEFAULT_ADMIN_ROLE);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `newAdmin` | `address` | 新管理员的地址。 |

#### changeRegistryManager

更改注册表管理器地址并转移 `REGISTRY_MANAGER_ROLE` 和 `PAUSER_ROLE`。

*仅可由管理员调用。*

```solidity
function changeRegistryManager(address newRegistryManager) external onlyRole(DEFAULT_ADMIN_ROLE);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `newRegistryManager` | `address` | 新注册表管理器的地址。 |

#### _changeChainStatus

更改链的状态为激活/停用。

```solidity
function _changeChainStatus(uint256 chainId, address gasZRC20, bytes calldata registry, bool activation) internal;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 要激活的链的 ID。 |
| `gasZRC20` | `address` | 代表该链 gas 代币的 ZRC20 代币地址。 |
| `registry` | `bytes` | 连接链上 Registry 合约的地址。 |
| `activation` | `bool` | 是否激活该链。 |

#### _updateChainMetadata

更新链元数据，仅针对活跃链。

```solidity
function _updateChainMetadata(uint256 chainId, string calldata key, bytes calldata value) internal;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 链的 ID。 |
| `key` | `string` | 要更新的元数据键。 |
| `value` | `bytes` | 元数据的新值。 |

#### _registerContract

为特定链注册新合约地址。

```solidity
function _registerContract(uint256 chainId, string calldata contractType, bytes calldata addressBytes) internal;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在链的 ID。 |
| `contractType` | `string` | 合约的类型（例如 "connector"、"gateway"）。 |
| `addressBytes` | `bytes` | 非 EVM 地址的字节表示。 |

#### _updateContractConfiguration

更新合约配置。

```solidity
function _updateContractConfiguration(
    uint256 chainId,
    string calldata contractType,
    string calldata key,
    bytes calldata value
)
    internal;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在链的 ID。 |
| `contractType` | `string` | 合约的类型。 |
| `key` | `string` | 要更新的配置键。 |
| `value` | `bytes` | 配置的新值。 |

#### _setContractActive

设置合约的活跃状态。

```solidity
function _setContractActive(uint256 chainId, string calldata contractType, bool active) internal;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在链的 ID。 |
| `contractType` | `string` | 合约的类型。 |
| `active` | `bool` | 合约是否应处于活跃状态。 |

#### _registerZRC20Token

在注册表中注册新的 ZRC20 代币。

```solidity
function _registerZRC20Token(
    address address_,
    string calldata symbol,
    uint256 originChainId,
    bytes calldata originAddress,
    string calldata coinType,
    uint8 decimals
)
    internal;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `address_` | `address` | ZRC20 代币在 ZetaChain 上的地址。 |
| `symbol` | `string` | 代币的符号。 |
| `originChainId` | `uint256` | 原始资产所在外部链的 ID。 |
| `originAddress` | `bytes` | 资产在其原生链上的地址或标识符。 |
| `coinType` | `string` | 原始代币的类型。 |
| `decimals` | `uint8` | 代币使用的小数位数。 |

#### _setZRC20TokenActive

更新 ZRC20 代币的活跃状态。

```solidity
function _setZRC20TokenActive(address address_, bool active) internal;
```

#### getChainInfo

获取特定链的信息。

```solidity
function getChainInfo(uint256 chainId) external view returns (address gasZRC20, bytes memory registry);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 链的 ID。 |

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `gasZRC20` | `address` | 代表该链 gas 代币的 ZRC20 代币地址。 |
| `registry` | `bytes` | 部署在该链上的注册表地址。 |

#### getChainMetadata

获取链特定元数据。

```solidity
function getChainMetadata(uint256 chainId, string calldata key) external view returns (bytes memory);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 链的 ID。 |
| `key` | `string` | 要检索的元数据键。 |

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `bytes` | 请求的元数据值。 |

#### getContractInfo

获取特定合约的信息。

```solidity
function getContractInfo(
    uint256 chainId,
    string calldata contractType
)
    external
    view
    returns (bool active, bytes memory addressBytes);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在链的 ID。 |
| `contractType` | `string` | 合约的类型。 |

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `active` | `bool` | 合约是否活跃。 |
| `addressBytes` | `bytes` | 合约的地址。 |

#### getContractConfiguration

获取合约特定配置。

```solidity
function getContractConfiguration(
    uint256 chainId,
    string calldata contractType,
    string calldata key
)
    external
    view
    returns (bytes memory);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在链的 ID。 |
| `contractType` | `string` | 合约的类型。 |
| `key` | `string` | 要检索的配置键。 |

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `bytes` | 请求的配置值。 |

#### getZRC20TokenInfo

获取特定 ZRC20 代币的信息。

```solidity
function getZRC20TokenInfo(address address_)
    external
    view
    returns (
        bool active,
        string memory symbol,
        uint256 originChainId,
        bytes memory originAddress,
        string memory coinType,
        uint8 decimals
    );
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `address_` | `address` | ZRC20 代币的地址。 |

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `active` | `bool` | 代币是否活跃。 |
| `symbol` | `string` | 代币的符号。 |
| `originChainId` | `uint256` | 原始资产所在外部链的 ID。 |
| `originAddress` | `bytes` | 资产在其原生链上的地址或标识符。 |
| `coinType` | `string` | 原始代币的类型。 |
| `decimals` | `uint8` | 代币使用的小数位数。 |

#### getZRC20AddressByForeignAsset

获取外部链上特定资产对应的 ZRC20 代币地址。

```solidity
function getZRC20AddressByForeignAsset(
    uint256 originChainId,
    bytes calldata originAddress
)
    external
    view
    returns (address);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `originChainId` | `uint256` | 外部链的 ID。 |
| `originAddress` | `bytes` | 资产在其原生链上的地址或标识符。 |

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `address` | ZetaChain 上对应 ZRC20 代币的地址。 |

#### getActiveChains

获取注册表中所有活跃链。

```solidity
function getActiveChains() external view returns (uint256[] memory);
```

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `<none>` | `uint256[]` | 所有活跃链的链 ID 数组。 |

#### getAllChains

返回注册表中所有链（活跃和非活跃）的信息。

```solidity
function getAllChains() external view returns (ChainInfoDTO[] memory chainsInfo);
```

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainsInfo` | `ChainInfoDTO[]` | 包含所有链信息的 ChainInfoDTO 结构体数组。 |

#### getAllContracts

返回注册表中所有合约的信息。

```solidity
function getAllContracts() external view returns (ContractInfoDTO[] memory contractsInfo);
```

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `contractsInfo` | `ContractInfoDTO[]` | 包含所有合约信息的 ContractInfoDTO 结构体数组。 |

#### getAllZRC20Tokens

返回注册表中所有 ZRC20 代币的信息。

```solidity
function getAllZRC20Tokens() external view returns (ZRC20Info[] memory tokensInfo);
```

**返回**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `tokensInfo` | `ZRC20Info[]` | 包含所有 ZRC20 代币信息的 ZRC20Info 结构体数组。 |

#### _removeFromActiveChains

从活跃链数组中移除一个链 ID。

```solidity
function _removeFromActiveChains(uint256 chainId) private;
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 要移除的链的 ID。 |

## IBaseRegistry

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

BaseRegistry 合约的接口。

### 函数
#### changeChainStatus

将链的状态更改为激活/未激活。

```solidity
function changeChainStatus(uint256 chainId, address gasZRC20, bytes calldata registry, bool activation) external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|要激活的链的 ID。|
|`gasZRC20`|`address`|代表该链 gas 代币的 ZRC20 代币地址。|
|`registry`|`bytes`||
|`activation`|`bool`|是否激活或停用链|


#### updateChainMetadata

更新链元数据。

```solidity
function updateChainMetadata(uint256 chainId, string calldata key, bytes calldata value) external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|链的 ID。|
|`key`|`string`|要更新的元数据键。|
|`value`|`bytes`|元数据的新值。|


#### registerContract

为特定链注册新的合约地址。

```solidity
function registerContract(uint256 chainId, string calldata contractType, bytes calldata addressBytes) external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|合约部署所在链的 ID。|
|`contractType`|`string`|合约类型（例如 "connector"、"gateway"）。|
|`addressBytes`|`bytes`|非 EVM 地址的字节表示。|


#### updateContractConfiguration

更新合约配置。

```solidity
function updateContractConfiguration(
    uint256 chainId,
    string calldata contractType,
    string calldata key,
    bytes calldata value
)
    external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|合约部署所在链的 ID。|
|`contractType`|`string`|合约类型。|
|`key`|`string`|要更新的配置键。|
|`value`|`bytes`|配置的新值。|


#### setContractActive

```solidity
function setContractActive(uint256 chainId, string calldata contractType, bool active) external;
```

#### registerZRC20Token

在注册表中注册新的 ZRC20 代币。

```solidity
function registerZRC20Token(
    address address_,
    string calldata symbol,
    uint256 originChainId,
    bytes calldata originAddress,
    string calldata coinType,
    uint8 decimals
)
    external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`address_`|`address`|ZetaChain 上 ZRC20 代币的地址。|
|`symbol`|`string`|代币符号。|
|`originChainId`|`uint256`|原始资产所在外部链的 ID。|
|`originAddress`|`bytes`|资产在其原生链上的地址或标识符。|
|`coinType`|`string`||
|`decimals`|`uint8`||


#### setZRC20TokenActive

更新 ZRC20 代币信息。

```solidity
function setZRC20TokenActive(address address_, bool active) external;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`address_`|`address`|ZRC20 代币的地址。|
|`active`|`bool`|代币是否应处于激活状态。|


#### getChainInfo

获取特定链的信息。

```solidity
function getChainInfo(uint256 chainId) external view returns (address gasZRC20, bytes memory registry);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|链的 ID。|

**返回**

|名称|类型|描述|
|----|----|-----------|
|`gasZRC20`|`address`|代表该链 gas 代币的 ZRC20 代币地址。|
|`registry`|`bytes`|部署在该链上的注册表地址。|


#### getChainMetadata

获取链特定元数据。

```solidity
function getChainMetadata(uint256 chainId, string calldata key) external view returns (bytes memory);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|链的 ID。|
|`key`|`string`|要检索的元数据键。|

**返回**

|名称|类型|描述|
|----|----|-----------|
|`<none>`|`bytes`|请求的元数据值。|


#### getContractInfo

获取特定合约的信息。

```solidity
function getContractInfo(
    uint256 chainId,
    string calldata contractType
)
    external
    view
    returns (bool active, bytes memory addressBytes);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|合约部署所在链的 ID。|
|`contractType`|`string`|合约类型。|

**返回**

|名称|类型|描述|
|----|----|-----------|
|`active`|`bool`|合约是否处于激活状态。|
|`addressBytes`|`bytes`|合约的地址。|


#### getContractConfiguration

获取合约特定配置。

```solidity
function getContractConfiguration(
    uint256 chainId,
    string calldata contractType,
    string calldata key
)
    external
    view
    returns (bytes memory);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainId`|`uint256`|合约部署所在链的 ID。|
|`contractType`|`string`|合约类型。|
|`key`|`string`|要检索的配置键。|

**返回**

|名称|类型|描述|
|----|----|-----------|
|`<none>`|`bytes`|请求的配置值。|


#### getZRC20TokenInfo

获取特定 ZRC20 代币的信息。

```solidity
function getZRC20TokenInfo(address address_)
    external
    view
    returns (
        bool active,
        string memory symbol,
        uint256 originChainId,
        bytes memory originAddress,
        string memory coinType,
        uint8 decimals
    );
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`address_`|`address`|ZRC20 代币的地址。|

**返回**

|名称|类型|描述|
|----|----|-----------|
|`active`|`bool`|代币是否处于激活状态。|
|`symbol`|`string`|代币符号|
|`originChainId`|`uint256`|原始资产所在外部链的 ID。|
|`originAddress`|`bytes`|资产在其原生链上的地址或标识符。|
|`coinType`|`string`|原始代币的类型。|
|`decimals`|`uint8`|代币使用的小数位数。|


#### getZRC20AddressByForeignAsset

获取外部链上特定资产对应的 ZRC20 代币地址。

```solidity
function getZRC20AddressByForeignAsset(
    uint256 originChainId,
    bytes calldata originAddress
)
    external
    view
    returns (address);
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`originChainId`|`uint256`|外部链的 ID。|
|`originAddress`|`bytes`|资产在其原生链上的地址或标识符。|

**返回**

|名称|类型|描述|
|----|----|-----------|
|`<none>`|`address`|ZetaChain 上对应的 ZRC20 代币地址。|


#### getActiveChains

获取注册表中所有激活的链。

```solidity
function getActiveChains() external view returns (uint256[] memory);
```
**返回**

|名称|类型|描述|
|----|----|-----------|
|`<none>`|`uint256[]`|所有激活链的链 ID 数组。|


#### getAllChains

返回注册表中所有链（激活和未激活）的信息。

```solidity
function getAllChains() external view returns (ChainInfoDTO[] memory);
```
**返回**

|名称|类型|描述|
|----|----|-----------|
|`<none>`|`ChainInfoDTO[]`|chainsInfo 包含所有链信息的 ChainInfoDTO 结构体数组。|


#### getAllContracts

返回注册表中所有合约的信息。

```solidity
function getAllContracts() external view returns (ContractInfoDTO[] memory);
```
**返回**

|名称|类型|描述|
|----|----|-----------|
|`<none>`|`ContractInfoDTO[]`|contractsInfo 包含所有合约信息的 ContractInfoDTO 结构体数组。|


#### getAllZRC20Tokens

获取注册表中所有激活的链。

```solidity
function getAllZRC20Tokens() external view returns (ZRC20Info[] memory);
```
**返回**

|名称|类型|描述|
|----|----|-----------|
|`<none>`|`ZRC20Info[]`|tokensInfo 包含所有 ZRC20 代币信息的 ZRC20Info 结构体数组。|

## IBaseRegistryErrors

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

BaseRegistry 合约所使用的错误接口。

### 错误

#### ZeroAddress
当需要非零地址时提供了零地址时抛出错误。

```solidity
error ZeroAddress();
```

#### InvalidSender
当发送方无效时抛出错误。

```solidity
error InvalidSender();
```

#### TransferFailed
当 ZRC20 代币转账失败时抛出错误。

```solidity
error TransferFailed();
```

#### ChainActive
当链已处于激活状态时抛出错误。

```solidity
error ChainActive(uint256 chainId);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `chainId` | `uint256` | 已处于激活状态的链 ID。 |

#### ChainNonActive
当链未处于激活状态时抛出错误。

```solidity
error ChainNonActive(uint256 chainId);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `chainId` | `uint256` | 未处于激活状态的链 ID。 |

#### InvalidContractType
当合约类型无效时抛出错误。

```solidity
error InvalidContractType(string message);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `message` | `string` | 描述错误发生的原因。 |

#### ContractAlreadyRegistered
当合约已被注册时抛出错误。

```solidity
error ContractAlreadyRegistered(uint256 chainId, string contractType, bytes addressBytes);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `chainId` | `uint256` | 链 ID。 |
| `contractType` | `string` | 合约类型。 |
| `addressBytes` | `bytes` | 合约地址。 |

#### ContractNotFound
当在注册表中未找到合约时抛出错误。

```solidity
error ContractNotFound(uint256 chainId, string contractType);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `chainId` | `uint256` | 链 ID。 |
| `contractType` | `string` | 合约类型。 |

#### ZRC20AlreadyRegistered
当 ZRC20 代币已被注册时抛出错误。

```solidity
error ZRC20AlreadyRegistered(address address_);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `address_` | `address` | ZRC20 代币的地址。 |

#### ZRC20SymbolAlreadyInUse
当 ZRC20 代币符号已被使用时抛出错误。

```solidity
error ZRC20SymbolAlreadyInUse(string symbol);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `symbol` | `string` | 已被使用的代币符号。 |

## IBaseRegistryEvents

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

`BaseRegistry` 合约所发出事件的接口。

### 事件
#### ChainStatusChanged
当链状态发生变更时触发。

```solidity
event ChainStatusChanged(uint256 indexed chainId, bool newStatus);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `chainId` | `uint256` | 链的 ID。 |
| `newStatus` | `bool` | 新的链状态（是否激活）。 |

#### ChainMetadataUpdated
当设置链元数据时触发。

```solidity
event ChainMetadataUpdated(uint256 indexed chainId, string key, bytes value);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `chainId` | `uint256` | 链的 ID。 |
| `key` | `string` | 要更新的元数据键。 |
| `value` | `bytes` | 元数据的新值。 |

#### ContractRegistered
当注册新合约时触发。

```solidity
event ContractRegistered(uint256 indexed chainId, string indexed contractType, bytes addressBytes);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `chainId` | `uint256` | 合约部署所在的链 ID。 |
| `contractType` | `string` | 合约的类型（例如 "connector"、"gateway"、"tss"）。 |
| `addressBytes` | `bytes` | 以字节表示的合约地址。 |

#### ContractStatusChanged
当合约状态发生变更时触发。

```solidity
event ContractStatusChanged(bytes addressBytes);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `addressBytes` | `bytes` | 以字节表示的合约地址。 |

#### ContractConfigurationUpdated
当合约配置更新时触发。

```solidity
event ContractConfigurationUpdated(uint256 indexed chainId, string contractType, string key, bytes value);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `chainId` | `uint256` | 合约部署所在的链 ID。 |
| `contractType` | `string` | 合约的类型。 |
| `key` | `string` | 要更新的配置键。 |
| `value` | `bytes` | 配置的新值。 |

#### ZRC20TokenRegistered
当注册 ZRC20 代币时触发。

```solidity
event ZRC20TokenRegistered(
    bytes indexed originAddress, address indexed address_, uint8 decimals, uint256 originChainId, string symbol
);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `originAddress` | `bytes` | 资产在其原生链上的地址。 |
| `address_` | `address` | ZRC20 代币在 ZetaChain 上的地址。 |
| `decimals` | `uint8` | 代币使用的小数位数。 |
| `originChainId` | `uint256` | 原始资产所在的外部链 ID。 |
| `symbol` | `string` | 代币的符号。 |

#### ZRC20TokenUpdated
当更新 ZRC20 代币时触发。

```solidity
event ZRC20TokenUpdated(address address_, bool active);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `address_` | `address` | ZRC20 代币的地址。 |
| `active` | `bool` | 代币是否应处于激活状态。 |

#### AdminChanged
当管理员地址变更时触发。

```solidity
event AdminChanged(address oldAdmin, address newAdmin);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `oldAdmin` | `address` | 旧的管理员地址。 |
| `newAdmin` | `address` | 新的管理员地址。 |

#### RegistryManagerChanged
当注册表管理器地址变更时触发。

```solidity
event RegistryManagerChanged(address oldRegistryManager, address newRegistryManager);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|-------------|
| `oldRegistryManager` | `address` | 旧的注册表管理器地址。 |
| `newRegistryManager` | `address` | 新的注册表管理器地址。 |

## 链信息

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

一个包含链信息的结构体。

```solidity
struct ChainInfo {
    bool active;
    uint256 chainId;
    address gasZRC20;
    bytes registry;
    mapping(string => bytes) metadata;
}
```

## ChainInfoDTO

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

包含链信息的结构体，用于数据检索。

```solidity
struct ChainInfoDTO {
    bool active;
    uint256 chainId;
    address gasZRC20;
    bytes registry;
}
```

## ContractIdentifier

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

每个条目包含：链 ID（uint256）和合约类型（string）

```solidity
struct ContractIdentifier {
    uint256 chainId;
    string contractType;
}
```

## ContractInfo

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

包含系统中注册合约信息的结构。

```solidity
struct ContractInfo {
    bool active;
    bytes addressBytes;
    string contractType;
    mapping(string => bytes) configuration;
}
```

## ContractInfoDTO

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

一个包含系统中注册合约信息的结构，用于数据检索。

```solidity
struct ContractInfoDTO {
    bool active;
    bytes addressBytes;
    string contractType;
    uint256 chainId;
}
```

## ZRC20Info

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/helpers/interfaces/IBaseRegistry.sol)

包含 ZRC20 代币信息的结构体。

```solidity
struct ZRC20Info {
    bool active;
    address address_;
    bytes originAddress;
    uint256 originChainId;
    string symbol;
    string coinType;
    uint8 decimals;
}
```

## 常量

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Revert.sol)

#### MAX_REVERT_GAS_LIMIT

```solidity
uint256 constant MAX_REVERT_GAS_LIMIT = 2_000_000;
```

## RevertGasLimitExceeded

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Revert.sol)

错误表示回滚操作的燃料限制超过了最大允许值。

```solidity
error RevertGasLimitExceeded(uint256 provided, uint256 maximum);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`provided`|`uint256`|为回滚操作提供的燃料限制。|
|`maximum`|`uint256`|回滚操作允许的最大燃料限制。|

## 可中止

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Revert.sol)

支持可中止调用的合约的接口。

### 函数
#### onAbort

当可恢复调用被中止时调用。

```solidity
function onAbort(AbortContext calldata abortContext) external;
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`abortContext`|`AbortContext`|传递给 onAbort 的中止上下文。|

## Revertable

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Revert.sol)

支持可回滚调用的合约接口。

### 函数
#### onRevert

当进行可回滚调用时调用。

```solidity
function onRevert(RevertContext calldata revertContext) external payable;
```

**参数**

| 名称 | 类型 | 描述 |
|----|----|-----------|
| `revertContext` | `RevertContext` | 传递给 onRevert 的回滚上下文。 |

## AbortContext

[Git 源码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Revert.sol)

包含传递给 onAbort 的中止上下文的结构体。

```solidity
struct AbortContext {
    bytes sender;
    address asset;
    uint256 amount;
    bool outgoing;
    uint256 chainID;
    bytes revertMessage;
}
```

**属性**

| 名称 | 类型 | 描述 |
|----|----|-----------|
| `sender` | `bytes` | 发起智能合约调用的账户地址。使用 bytes 是因为跨链交易可能从非 EVM 链发起。 |
| `asset` | `address` | 资产地址。在连接链上，它包含可替代代币地址，如果是 gas 代币则为空。在 ZetaChain 上，它包含 ZRC20 的地址。 |
| `amount` | `uint256` | 交易中指定的数量。 |
| `outgoing` | `bool` | 指示跨链交易是否为出站：从 ZetaChain 到连接链。如果为 false，则交易为入站：从连接链到 ZetaChain。 |
| `chainID` | `uint256` | 连接链的链 ID。 |
| `revertMessage` | `bytes` | 发起跨链交易时在 RevertOptions 对象中指定的任意数据。 |

## RevertContext

[Git 源码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Revert.sol)

包含传递给 onRevert 的 revert context 的结构体。

```solidity
struct RevertContext {
    address sender;
    address asset;
    uint256 amount;
    bytes revertMessage;
}
```

**属性**

| 名称 | 类型 | 描述 |
|----|----|-----------|
| `sender` | `address` | 发起智能合约调用的账户地址。 |
| `asset` | `address` | 资产地址。在连接链上，它包含可替代代币地址或为空（如果是 gas 代币）。在 ZetaChain 上，它包含 ZRC20 的地址。 |
| `amount` | `uint256` | 交易中指定的金额。 |
| `revertMessage` | `bytes` | 在 onRevert 中发送回的任意数据。 |

## RevertOptions

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/Revert.sol)

包含回退选项的结构体

```solidity
struct RevertOptions {
    address revertAddress;
    bool callOnRevert;
    address abortAddress;
    bytes revertMessage;
    uint256 onRevertGasLimit;
}
```

**属性**

| 名称 | 类型 | 描述 |
|----|----|-----------|
| `revertAddress` | `address` | 接收回退的地址。 |
| `callOnRevert` | `bool` | 标志是否应调用 onRevert 钩子。 |
| `abortAddress` | `address` | 如果中止，接收资金的地址。 |
| `revertMessage` | `bytes` | 在 onRevert 中发送回的任意数据。 |
| `onRevertGasLimit` | `uint256` | 回退交易的 gas 限制，在 GatewayZEVM 方法中未使用。 |

## CoreRegistry

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/CoreRegistry.sol)

ZetaChain 的核心注册表，用于管理所有链的链信息、ZRC20 数据和合约地址。

*该合约不持有任何资金，且绝不应有活跃的授权额度。*

### 状态变量
#### CROSS_CHAIN_GAS_LIMIT
跨链消息的 gas 限制

```solidity
uint256 public constant CROSS_CHAIN_GAS_LIMIT = 500_000;
```

#### gatewayZEVM
用于跨链通信的 GatewayZEVM 合约实例

```solidity
IGatewayZEVM public gatewayZEVM;
```

### 函数
#### initialize

初始化 CoreRegistry 合约。

```solidity
function initialize(address admin_, address registryManager_, address gatewayZEVM_) public initializer;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `admin_` | `address` | 拥有 DEFAULT_ADMIN_ROLE 的地址，被授权执行升级和暂停操作。 |
| `registryManager_` | `address` | 拥有 REGISTRY_MANAGER_ROLE 的地址，被授权执行所有注册表写入操作。 |
| `gatewayZEVM_` | `address` | 用于跨链消息传递的 GatewayZEVM 合约地址。 |

#### changeChainStatus

更改链的激活/停用状态。

```solidity
function changeChainStatus(
    uint256 chainId,
    address gasZRC20,
    bytes calldata registry,
    bool activation
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 要激活的链的 ID。 |
| `gasZRC20` | `address` | 代表该链燃料代币的 ZRC20 代币地址。 |
| `registry` | `bytes` | 所连接链上的 Registry 合约地址。 |
| `activation` | `bool` | 是激活还是停用该链。 |

#### updateChainMetadata

更新链的元数据，仅适用于活跃链。

```solidity
function updateChainMetadata(
    uint256 chainId,
    string calldata key,
    bytes calldata value
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 链的 ID。 |
| `key` | `string` | 要更新的元数据键。 |
| `value` | `bytes` | 元数据的新值。 |

#### registerContract

为特定链注册一个新的合约地址。

```solidity
function registerContract(
    uint256 chainId,
    string calldata contractType,
    bytes calldata addressBytes
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在的链的 ID。 |
| `contractType` | `string` | 合约的类型（例如 "connector"、"gateway"）。 |
| `addressBytes` | `bytes` | 非 EVM 地址的字节表示形式。 |

#### updateContractConfiguration

更新合约配置。

```solidity
function updateContractConfiguration(
    uint256 chainId,
    string calldata contractType,
    string calldata key,
    bytes calldata value
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在的链的 ID。 |
| `contractType` | `string` | 合约的类型。 |
| `key` | `string` | 要更新的配置键。 |
| `value` | `bytes` | 配置的新值。 |

#### setContractActive

设置合约的活跃状态。

```solidity
function setContractActive(
    uint256 chainId,
    string calldata contractType,
    bool active
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在的链的 ID。 |
| `contractType` | `string` | 合约的类型。 |
| `active` | `bool` | 合约是否应处于活跃状态。 |

#### registerZRC20Token

在注册表中注册一个新的 ZRC20 代币。

```solidity
function registerZRC20Token(
    address address_,
    string calldata symbol,
    uint256 originChainId,
    bytes calldata originAddress,
    string calldata coinType,
    uint8 decimals
)
    external
    onlyRole(REGISTRY_MANAGER_ROLE)
    whenNotPaused;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `address_` | `address` | ZetaChain 上 ZRC20 代币的地址。 |
| `symbol` | `string` | 代币的符号。 |
| `originChainId` | `uint256` | 原始资产所在的外部链的 ID。 |
| `originAddress` | `bytes` | 资产在其原生链上的地址或标识符。 |
| `coinType` | `string` | 原始代币的类型。 |
| `decimals` | `uint8` | 代币使用的小数位数。 |

#### setZRC20TokenActive

更新 ZRC20 代币的活跃状态。

```solidity
function setZRC20TokenActive(address address_, bool active) external onlyRole(REGISTRY_MANAGER_ROLE) whenNotPaused;
```

#### _broadcastChainActivation

向所有卫星注册表广播链激活更新。

```solidity
function _broadcastChainActivation(
    uint256 chainId,
    address gasZRC20,
    bytes calldata registry,
    bool activation
)
    internal;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 正在被激活/停用的链的 ID。 |
| `gasZRC20` | `address` | 代表该链燃料代币的 ZRC20 代币地址。 |
| `registry` | `bytes` | 所连接链上的 Registry 合约地址。 |
| `activation` | `bool` | 是激活还是停用该链。 |

#### _broadcastChainMetadataUpdate

向所有卫星注册表广播链元数据。

```solidity
function _broadcastChainMetadataUpdate(uint256 chainId, string calldata key, bytes calldata value) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 元数据正在被更新的链的 ID。 |
| `key` | `string` | 正在被更新的元数据键。 |
| `value` | `bytes` | 元数据的新值。 |

#### _broadcastContractRegistration

向所有卫星注册表广播合约注册。

contractType 合约的类型

addressBytes 非 EVM 地址的字节表示形式

```solidity
function _broadcastContractRegistration(
    uint256 chainId,
    string calldata contractType,
    bytes calldata addressBytes
)
    private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在的链的 ID。 |
| `contractType` | `string` | |
| `addressBytes` | `bytes` | |

#### _broadcastContractConfigUpdate

向所有卫星注册表广播合约配置更新。

contractType 合约的类型

key 正在被更新的配置键

value 配置的新值

```solidity
function _broadcastContractConfigUpdate(
    uint256 chainId,
    string calldata contractType,
    string calldata key,
    bytes calldata value
)
    private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在的链的 ID。 |
| `contractType` | `string` | |
| `key` | `string` | |
| `value` | `bytes` | |

#### _broadcastContractStatusUpdate

向所有卫星注册表广播合约状态更新。

contractType 合约的类型

active 合约是否应处于活跃状态

```solidity
function _broadcastContractStatusUpdate(uint256 chainId, string calldata contractType, bool active) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `chainId` | `uint256` | 合约部署所在的链的 ID。 |
| `contractType` | `string` | |
| `active` | `bool` | |

#### _broadcastZRC20Registration

向所有卫星注册表广播 ZRC20 代币注册。

```solidity
function _broadcastZRC20Registration(
    address address_,
    string calldata symbol,
    uint256 originChainId,
    bytes calldata originAddress,
    string calldata coinType,
    uint8 decimals
)
    private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `address_` | `address` | ZetaChain 上 ZRC20 代币的地址。 |
| `symbol` | `string` | 代币的符号。 |
| `originChainId` | `uint256` | 原始资产所在的外部链的 ID。 |
| `originAddress` | `bytes` | 资产在其原生链上的地址或标识符。 |
| `coinType` | `string` | 原始代币的类型。 |
| `decimals` | `uint8` | 代币使用的小数位数。 |

#### _broadcastZRC20Update

向所有卫星注册表广播 ZRC20 代币更新。

```solidity
function _broadcastZRC20Update(address address_, bool active) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `address_` | `address` | ZRC20 代币的地址。 |
| `active` | `bool` | 代币是否应处于活跃状态。 |

#### _broadcastToAllChains

向所有卫星注册表广播编码消息的通用函数。

```solidity
function _broadcastToAllChains(bytes memory encodedMessage) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `encodedMessage` | `bytes` | 要广播的完整编码函数调用。 |

#### _sendCrossChainMessage

向目标链上的 Registry 合约发送跨链消息。

```solidity
function _sendCrossChainMessage(uint256 targetChainId, bytes memory message) private;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `targetChainId` | `uint256` | 要发送消息到的链的 ID。 |
| `message` | `bytes` | 要在目标链上执行的编码函数调用。 |

## ICoreRegistry

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/ICoreRegistry.sol)

### 函数
#### gatewayZEVM

```solidity
function gatewayZEVM() external returns (address);
```

## IGatewayZEVM

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IGatewayZEVM.sol)

GatewayZEVM 合约的接口。

*定义跨链交互和代币处理的函数。*

### 函数
#### withdraw

将 ZRC20 代币提取到外部链。

```solidity
function withdraw(
    bytes memory receiver,
    uint256 amount,
    address zrc20,
    RevertOptions calldata revertOptions
)
    external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### withdraw

将 ZETA 代币提取到外部链。

```solidity
function withdraw(bytes memory receiver, uint256 chainId, RevertOptions calldata revertOptions) external payable;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `chainId` | `uint256` | |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### withdrawAndCall

提取 ZRC20 代币并调用外部链上的智能合约。

```solidity
function withdrawAndCall(
    bytes memory receiver,
    uint256 amount,
    address zrc20,
    bytes calldata message,
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions
)
    external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `amount` | `uint256` | 要提取的代币数量。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |
| `callOptions` | `CallOptions` | 调用选项，包括 gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### withdrawAndCall

提取 ZETA 代币并调用外部链上的智能合约。

```solidity
function withdrawAndCall(
    bytes memory receiver,
    uint256 chainId,
    bytes calldata message,
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions
)
    external
    payable;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `chainId` | `uint256` | 外部链的链 ID。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |
| `callOptions` | `CallOptions` | 调用选项，包括 gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### call

在不进行资产转移的情况下调用外部链上的智能合约。

```solidity
function call(
    bytes memory receiver,
    address zrc20,
    bytes calldata message,
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions
)
    external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `zrc20` | `address` | 用于支付费用的 zrc20 地址。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |
| `callOptions` | `CallOptions` | 调用选项，包括 gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### deposit

将外部代币存入 ZRC20。

```solidity
function deposit(address zrc20, uint256 amount, address target) external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要存入的代币数量。 |
| `target` | `address` | 接收存入代币的目标地址。 |

#### deposit

存入原生 ZETA。

```solidity
function deposit(address target) external payable;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `target` | `address` | 接收 ZETA 的目标地址。 |

#### execute

在 ZEVM 上执行用户指定的合约。

```solidity
function execute(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    address target,
    bytes calldata message
)
    external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `context` | `MessageContext` | 跨链调用的上下文。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `target` | `address` | 要调用的目标合约。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |

#### depositAndCall

将外部代币存入 ZRC20 并调用 ZEVM 上用户指定的合约。

```solidity
function depositAndCall(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    address target,
    bytes calldata message
)
    external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `context` | `MessageContext` | 跨链调用的上下文。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要转移的代币数量。 |
| `target` | `address` | 要调用的目标合约。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |

#### depositAndCall

存入原生 ZETA 并调用 ZEVM 上用户指定的合约。

```solidity
function depositAndCall(MessageContext calldata context, address target, bytes calldata message) external payable;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `context` | `MessageContext` | 跨链调用的上下文。 |
| `target` | `address` | 要调用的目标合约。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |

#### executeRevert

在 ZEVM 上回退用户指定的合约。

```solidity
function executeRevert(address target, RevertContext calldata revertContext) external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `target` | `address` | 要调用的目标合约。 |
| `revertContext` | `RevertContext` | 传递给 onRevert 的回退上下文。 |

#### depositAndRevert

将外部代币存入 ZRC20 并回退 ZEVM 上用户指定的合约。

```solidity
function depositAndRevert(
    address zrc20,
    uint256 amount,
    address target,
    RevertContext calldata revertContext
)
    external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `amount` | `uint256` | 要回退的代币数量。 |
| `target` | `address` | 要调用的目标合约。 |
| `revertContext` | `RevertContext` | 传递给 onRevert 的回退上下文。 |

## IGatewayZEVMErrors

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IGatewayZEVM.sol)

GatewayZEVM 合约中使用的错误接口。

### 错误

#### WithdrawalFailed
表示提款失败的错误。

```solidity
error WithdrawalFailed(address token, address recipient, uint256 amount);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `token` | `address` | 未能成功提款的代币地址。 |
| `recipient` | `address` | 本应接收代币的地址。 |
| `amount` | `uint256` | 未能成功提款的代币数量。 |

#### InsufficientAmount
表示代币数量不足的错误。

```solidity
error InsufficientAmount();
```

#### ZRC20BurnFailed
表示销毁 ZRC20 代币失败的错误。

```solidity
error ZRC20BurnFailed(address zrc20, uint256 amount);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `zrc20` | `address` | 未能成功销毁的 ZRC20 代币地址。 |
| `amount` | `uint256` | 未能成功销毁的代币数量。 |

#### ZRC20TransferFailed
表示转移 ZRC20 代币失败的错误。

```solidity
error ZRC20TransferFailed(address zrc20, address from, address to, uint256 amount);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `zrc20` | `address` | 未能成功转移的 ZRC20 代币地址。 |
| `from` | `address` | 发送代币的地址。 |
| `to` | `address` | 接收代币的地址。 |
| `amount` | `uint256` | 未能成功转移的代币数量。 |

#### ZRC20DepositFailed
表示存入 ZRC20 代币失败的错误。

```solidity
error ZRC20DepositFailed(address zrc20, address to, uint256 amount);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `zrc20` | `address` | 未能成功存入的 ZRC20 代币地址。 |
| `to` | `address` | 本应接收存款的地址。 |
| `amount` | `uint256` | 未能成功存入的代币数量。 |

#### GasFeeTransferFailed
表示 Gas 费转移失败的错误。

```solidity
error GasFeeTransferFailed(address token, address to, uint256 amount);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `token` | `address` | 用于支付 Gas 费的代币地址。 |
| `to` | `address` | 本应接收 Gas 费的地址。 |
| `amount` | `uint256` | 未能成功转移的 Gas 费数量。 |

#### CallerIsNotProtocol
表示调用者并非协议账户的错误。

```solidity
error CallerIsNotProtocol();
```

#### InvalidTarget
表示目标地址无效的错误。

```solidity
error InvalidTarget();
```

#### FailedZetaSent
表示发送 ZETA 代币失败的错误。

```solidity
error FailedZetaSent(address recipient, uint256 amount);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `recipient` | `address` | 本应接收 ZETA 代币的地址。 |
| `amount` | `uint256` | 未能成功发送的 ZETA 代币数量。 |

#### OnlyWZETAOrProtocol
表示仅允许 WZETA 或协议地址调用该函数的错误。

```solidity
error OnlyWZETAOrProtocol();
```

#### InsufficientGasLimit
表示 Gas 限制不足的错误。

```solidity
error InsufficientGasLimit();
```

#### MessageSizeExceeded
表示外部函数中消息大小超限的错误。

```solidity
error MessageSizeExceeded(uint256 provided, uint256 maximum);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `provided` | `uint256` | 提供的消息大小。 |
| `maximum` | `uint256` | 允许的最大消息大小。 |

#### ZeroGasPrice
表示 Gas 价格无效的错误。

```solidity
error ZeroGasPrice();
```

## IGatewayZEVMEvents

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IGatewayZEVM.sol)

`GatewayZEVM` 合约发出的事件的接口。

### 事件

#### Called
当进行跨链调用时发出。

```solidity
event Called(
    address indexed sender,
    address indexed zrc20,
    bytes receiver,
    bytes message,
    CallOptions callOptions,
    RevertOptions revertOptions
);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `sender` | `address` | 发送者的地址。 |
| `zrc20` | `address` | 用于支付费用的 ZRC20 地址。 |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |
| `callOptions` | `CallOptions` | 调用选项，包括 gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### Withdrawn
当进行提现时发出。

```solidity
event Withdrawn(
    address indexed sender,
    uint256 indexed chainId,
    bytes receiver,
    address zrc20,
    uint256 value,
    uint256 gasfee,
    uint256 protocolFlatFee,
    bytes message,
    CallOptions callOptions,
    RevertOptions revertOptions
);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `sender` | `address` | 提现来源的地址。 |
| `chainId` | `uint256` | 外部链的链 ID。 |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `value` | `uint256` | 提现的代币数量。 |
| `gasfee` | `uint256` | 提现的 gas 费用。 |
| `protocolFlatFee` | `uint256` | 提现的协议固定费用。 |
| `message` | `bytes` | 随提现传递的调用数据。不再使用。保留以保持兼容性。 |
| `callOptions` | `CallOptions` | 调用选项，包括 gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

#### WithdrawnAndCalled
当进行提现并调用时发出。

```solidity
event WithdrawnAndCalled(
    address indexed sender,
    uint256 indexed chainId,
    bytes receiver,
    address zrc20,
    uint256 value,
    uint256 gasfee,
    uint256 protocolFlatFee,
    bytes message,
    CallOptions callOptions,
    RevertOptions revertOptions
);
```

**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ---- |
| `sender` | `address` | 提现来源的地址。 |
| `chainId` | `uint256` | 外部链的链 ID。 |
| `receiver` | `bytes` | 外部链上的接收者地址。 |
| `zrc20` | `address` | ZRC20 代币的地址。 |
| `value` | `uint256` | 提现的代币数量。 |
| `gasfee` | `uint256` | 提现的 gas 费用。 |
| `protocolFlatFee` | `uint256` | 提现的协议固定费用。 |
| `message` | `bytes` | 传递给合约调用的调用数据。 |
| `callOptions` | `CallOptions` | 调用选项，包括 gas 限制和任意调用标志。 |
| `revertOptions` | `RevertOptions` | 回退选项。 |

## CallOptions

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IGatewayZEVM.sol)

CallOptions 结构体传递给 call 和 withdrawAndCall 函数。

```solidity
struct CallOptions {
    uint256 gasLimit;
    bool isArbitraryCall;
}
```

**属性**

|名称|类型|描述|
|----|----|-----------|
|`gasLimit`|`uint256`|Gas 限制。|
|`isArbitraryCall`|`bool`|指示调用是否应为任意或认证的。|

## ISystem

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/ISystem.sol)

System 合约的接口。

*定义了可由 fungible 模块调用的系统合约函数。*

### 函数

#### FUNGIBLE_MODULE_ADDRESS

```solidity
function FUNGIBLE_MODULE_ADDRESS() external view returns (address);
```

#### wZetaContractAddress

```solidity
function wZetaContractAddress() external view returns (address);
```

#### uniswapv2FactoryAddress

```solidity
function uniswapv2FactoryAddress() external view returns (address);
```

#### gasPriceByChainId

```solidity
function gasPriceByChainId(uint256 chainID) external view returns (uint256);
```

#### gasCoinZRC20ByChainId

```solidity
function gasCoinZRC20ByChainId(uint256 chainID) external view returns (address);
```

#### gasZetaPoolByChainId

```solidity
function gasZetaPoolByChainId(uint256 chainID) external view returns (address);
```

## IWETH9

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IWZETA.sol)

Weth9 合约的接口。

### 函数

#### totalSupply

```solidity
function totalSupply() external view returns (uint256);
```

#### balanceOf

```solidity
function balanceOf(address owner) external view returns (uint256);
```

#### allowance

```solidity
function allowance(address owner, address spender) external view returns (uint256);
```

#### approve

```solidity
function approve(address spender, uint256 wad) external returns (bool);
```

#### transfer

```solidity
function transfer(address to, uint256 wad) external returns (bool);
```

#### transferFrom

```solidity
function transferFrom(address from, address to, uint256 wad) external returns (bool);
```

#### deposit

```solidity
function deposit() external payable;
```

#### withdraw

```solidity
function withdraw(uint256 wad) external;
```

### 事件

#### Approval

```solidity
event Approval(address indexed owner, address indexed spender, uint256 value);
```

#### Transfer

```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```

#### Deposit

```solidity
event Deposit(address indexed dst, uint256 wad);
```

#### Withdrawal

```solidity
event Withdrawal(address indexed src, uint256 wad);
```

## 币种类型

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IZRC20.sol)

*ZRC20 的币种类型。Zeta 值不应被使用。*

```solidity
enum CoinType {
    Zeta,
    Gas,
    ERC20
}
```

## IZRC20

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IZRC20.sol)

ZRC20 代币合约的接口。

### 函数

#### totalSupply

```solidity
function totalSupply() external view returns (uint256);
```

#### balanceOf

```solidity
function balanceOf(address account) external view returns (uint256);
```

#### transfer

```solidity
function transfer(address recipient, uint256 amount) external returns (bool);
```

#### allowance

```solidity
function allowance(address owner, address spender) external view returns (uint256);
```

#### approve

```solidity
function approve(address spender, uint256 amount) external returns (bool);
```

#### transferFrom

```solidity
function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);
```

#### deposit

```solidity
function deposit(address to, uint256 amount) external returns (bool);
```

#### burn

```solidity
function burn(uint256 amount) external returns (bool);
```

#### withdraw

```solidity
function withdraw(bytes memory to, uint256 amount) external returns (bool);
```

#### withdrawGasFee

```solidity
function withdrawGasFee() external view returns (address, uint256);
```

#### withdrawGasFeeWithGasLimit

```solidity
function withdrawGasFeeWithGasLimit(uint256 gasLimit) external view returns (address, uint256);
```

#### PROTOCOL_FLAT_FEE

*名称使用大写以保持与 ZRC20.sol v1 的兼容性*

```solidity
function PROTOCOL_FLAT_FEE() external view returns (uint256);
```

#### GAS_LIMIT

*名称使用大写以保持与 ZRC20.sol v1 的兼容性*

```solidity
function GAS_LIMIT() external view returns (uint256);
```

#### SYSTEM_CONTRACT_ADDRESS

*名称使用大写以保持与 ZRC20.sol v1 的兼容性*

```solidity
function SYSTEM_CONTRACT_ADDRESS() external view returns (address);
```

#### setName

```solidity
function setName(string memory newName) external;
```

#### setSymbol

```solidity
function setSymbol(string memory newSymbol) external;
```

## IZRC20Metadata

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IZRC20.sol)

ZRC20 元数据的接口。

### 函数
#### name

```solidity
function name() external view returns (string memory);
```

#### symbol

```solidity
function symbol() external view returns (string memory);
```

#### decimals

```solidity
function decimals() external view returns (uint8);
```

## ZRC20 事件

[Git 源文件](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/IZRC20.sol)

ZRC20 事件接口。

### 事件
#### Transfer

```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```

#### Approval

```solidity
event Approval(address indexed owner, address indexed spender, uint256 value);
```

#### Deposit

```solidity
event Deposit(bytes from, address indexed to, uint256 value);
```

#### Withdrawal

```solidity
event Withdrawal(address indexed from, bytes to, uint256 value, uint256 gasFee, uint256 protocolFlatFee);
```

#### UpdatedSystemContract

```solidity
event UpdatedSystemContract(address systemContract);
```

#### UpdatedGateway

```solidity
event UpdatedGateway(address gateway);
```

#### UpdatedGasLimit

```solidity
event UpdatedGasLimit(uint256 gasLimit);
```

#### UpdatedProtocolFlatFee

```solidity
event UpdatedProtocolFlatFee(uint256 protocolFlatFee);
```

## UniversalContract

[Git 源码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/UniversalContract.sol)

用于在 ZetaChain 上接收跨链调用的抽象合约。

*继承此抽象合约的合约可以处理传入的跨链消息，并根据提供的上下文、代币和消息负载执行逻辑。*

### 状态变量
#### registry
对 ZetaChain Registry 合约的引用

```solidity
ICoreRegistry public constant registry = ICoreRegistry(0x7CCE3Eb018bf23e1FE2a32692f2C77592D110394);
```

#### gateway
对 ZetaChain Gateway 合约的引用

```solidity
IGatewayZEVM public immutable gateway;
```

### 函数
#### onlyGateway
限制函数访问，仅允许网关合约调用

*用于处理跨链消息的函数，以确保它们仅通过 Gateway 调用，消息验证在此处进行。对于处理传入跨链操作的函数（如 `onCall()` 和 `onRevert()`）的安全性至关重要。*

```solidity
modifier onlyGateway();
```

#### constructor
通过从注册表中检索网关地址来初始化合约

*从注册表中获取当前链的网关合约地址。如果网关未激活或未找到，网关将保持未初始化状态（address(0)）。*

```solidity
constructor();
```

#### onCall
用于处理带有原生 ZETA 转账的跨链调用的函数

```solidity
function onCall(MessageContext calldata context, bytes calldata message) external payable virtual;
```

#### onCall
用于处理带有 ZRC20 代币转账的跨链调用的函数

```solidity
function onCall(
    MessageContext calldata context,
    address zrc20,
    uint256 amount,
    bytes calldata message
)
    external
    virtual;
```

### 错误
#### Unauthorized
当函数被未授权地址调用时抛出的错误

```solidity
error Unauthorized();
```

## zContract

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/UniversalContract.sol)

**注意：**  
已弃用：一旦 v2 SystemContract 不再使用，就应该移除。应该使用 UniversalContract。

### 函数
#### onCrossChainCall

```solidity
function onCrossChainCall(zContext calldata context, address zrc20, uint256 amount, bytes calldata message) external;
```

## 消息上下文

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/UniversalContract.sol)

提供在 ZetaChain 上执行跨链调用时的上下文信息。

*此结构体有助于在不同区块链环境中识别消息的发送者。*

```solidity
struct MessageContext {
    bytes sender;
    address senderEVM;
    uint256 chainID;
}
```

## zContext

[Git 源](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/interfaces/UniversalContract.sol)

**注意：**  
已弃用：一旦 v2 SystemContract 不再被使用，就应该被移除。应该使用 MessageContext。

```solidity
struct zContext {
    bytes origin;
    address sender;
    uint256 chainID;
}
```

## ZetaConnectorZEVM

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/legacy/ZetaConnectorZEVM.sol)

### 状态变量
#### wzeta
WZETA 代币地址。

```solidity
address public wzeta;
```

#### FUNGIBLE_MODULE_ADDRESS
可互换模块地址。

```solidity
address public constant FUNGIBLE_MODULE_ADDRESS = payable(0x735b14BB79463307AAcBED86DAf3322B1e6226aB);
```

### 函数
#### onlyFungibleModule
*修饰符，用于将操作限制为可互换模块。*

```solidity
modifier onlyFungibleModule();
```

#### constructor

```solidity
constructor(address wzeta_);
```

#### receive
*接收函数，用于从 WETH9.withdraw() 接收 ZETA。*

```solidity
receive() external payable;
```

#### setWzetaAddress

```solidity
function setWzetaAddress(address wzeta_) external onlyFungibleModule;
```

#### send
*发送 ZETA 和字节消息（以执行它）跨链。*

```solidity
function send(ZetaInterfaces.SendInput calldata input) external;
```
**参数**

| 名称 | 类型 | 描述 |
| ---- | ---- | ----------- |
| `input` | `ZetaInterfaces.SendInput` | |

#### onReceive
*处理程序，用于接收来自其他链的数据。
此方法只能由可互换模块调用。
将 Zeta 代币转移到目标地址，并在需要时调用 onZetaMessage。
要执行转移，请包装新代币。*

```solidity
function onReceive(
    bytes calldata zetaTxSenderAddress,
    uint256 sourceChainId,
    address destinationAddress,
    uint256 zetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    payable
    onlyFungibleModule;
```

#### onRevert
*处理程序，用于接收来自其他链的错误。
此方法只能由可互换模块调用。
将 Zeta 代币转移到目标地址，并在需要时调用 onZetaRevert。*

```solidity
function onRevert(
    address zetaTxSenderAddress,
    uint256 sourceChainId,
    bytes calldata destinationAddress,
    uint256 destinationChainId,
    uint256 remainingZetaValue,
    bytes calldata message,
    bytes32 internalSendHash
)
    external
    payable
    onlyFungibleModule;
```

### 事件
#### SetWZETA

```solidity
event SetWZETA(address wzeta_);
```

#### ZetaSent

```solidity
event ZetaSent(
    address sourceTxOriginAddress,
    address indexed zetaTxSenderAddress,
    uint256 indexed destinationChainId,
    bytes destinationAddress,
    uint256 zetaValueAndGas,
    uint256 destinationGasLimit,
    bytes message,
    bytes zetaParams
);
```

#### ZetaReceived

```solidity
event ZetaReceived(
    bytes zetaTxSenderAddress,
    uint256 indexed sourceChainId,
    address indexed destinationAddress,
    uint256 zetaValue,
    bytes message,
    bytes32 indexed internalSendHash
);
```

#### ZetaReverted

```solidity
event ZetaReverted(
    address zetaTxSenderAddress,
    uint256 sourceChainId,
    uint256 indexed destinationChainId,
    bytes destinationAddress,
    uint256 remainingZetaValue,
    bytes message,
    bytes32 indexed internalSendHash
);
```

### 错误
#### OnlyWZETAOrFungible
合约自定义错误。

```solidity
error OnlyWZETAOrFungible();
```

#### WZETATransferFailed

```solidity
error WZETATransferFailed();
```

#### OnlyFungibleModule

```solidity
error OnlyFungibleModule();
```

#### FailedZetaSent

```solidity
error FailedZetaSent();
```

#### WrongValue

```solidity
error WrongValue();
```

## ZetaInterfaces

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/legacy/ZetaConnectorZEVM.sol)

### 结构体

#### SendInput
*使用 SendInput 与连接器交互：connector.send(SendInput)*

```solidity
struct SendInput {
    uint256 destinationChainId;
    bytes destinationAddress;
    uint256 destinationGasLimit;
    bytes message;
    uint256 zetaValueAndGas;
    bytes zetaParams;
}
```

#### ZetaMessage
*我们的连接器使用此结构体作为参数调用 onZetaMessage*

```solidity
struct ZetaMessage {
    bytes zetaTxSenderAddress;
    uint256 sourceChainId;
    address destinationAddress;
    uint256 zetaValue;
    bytes message;
}
```

#### ZetaRevert
*我们的连接器使用此结构体作为参数调用 onZetaRevert*

```solidity
struct ZetaRevert {
    address zetaTxSenderAddress;
    uint256 sourceChainId;
    bytes destinationAddress;
    uint256 destinationChainId;
    uint256 remainingZetaValue;
    bytes message;
}
```

## ZetaReceiver

[Git 源代码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/legacy/ZetaConnectorZEVM.sol)

### 函数
#### onZetaMessage

*当跨链消息到达合约时，会调用 onZetaMessage。*

```solidity
function onZetaMessage(ZetaInterfaces.ZetaMessage calldata zetaMessage) external;
```

#### onZetaRevert

*当跨链消息回退时，会调用 onZetaRevert。它可用于回滚到原始状态。*

```solidity
function onZetaRevert(ZetaInterfaces.ZetaRevert calldata zetaRevert) external;
```

## GatewayZEVMValidations

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/libraries/GatewayZEVMValidations.sol)

包含 GatewayZEVM 合约验证函数的库

*该库提供在 GatewayZEVM 合约中使用的通用验证逻辑*

### 状态变量
#### MAX_MESSAGE_SIZE
最大消息大小常量

```solidity
uint256 internal constant MAX_MESSAGE_SIZE = 2880;
```

#### MIN_GAS_LIMIT
最小 gas 限制常量

```solidity
uint256 internal constant MIN_GAS_LIMIT = 100_000;
```

### 函数
#### validateNonZeroAddress

*验证地址不为零*

```solidity
function validateNonZeroAddress(address addr) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`addr`|`address`|要验证的地址|

#### validateReceiver

*验证接收者字节不为空*

```solidity
function validateReceiver(bytes memory receiver) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`receiver`|`bytes`|要验证的接收者字节|

#### validateAmount

*验证金额不为零*

```solidity
function validateAmount(uint256 amount) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`amount`|`uint256`|要验证的金额|

#### validateGasLimit

*验证 gas 限制满足最低要求*

```solidity
function validateGasLimit(uint256 gasLimit) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`gasLimit`|`uint256`|要验证的 gas 限制|

#### validateTarget

*验证目标地址不受限制*

```solidity
function validateTarget(address target, address protocolAddress, address contractAddress) private pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`target`|`address`|要验证的目标地址|
|`protocolAddress`|`address`|用于检查的协议地址|
|`contractAddress`|`address`|用于检查的合约地址|

#### validateMessageSize

*验证消息大小约束*

```solidity
function validateMessageSize(uint256 messageLength, uint256 revertMessageLength) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`messageLength`|`uint256`|主消息的长度|
|`revertMessageLength`|`uint256`|回退消息的长度|

#### validateRevertOptions

*验证回退选项*

```solidity
function validateRevertOptions(RevertOptions calldata revertOptions) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`revertOptions`|`RevertOptions`|要验证的回退选项|

#### validateCallAndRevertOptions

*同时验证调用选项和回退选项*

```solidity
function validateCallAndRevertOptions(
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions,
    uint256 messageLength
)
    internal
    pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`callOptions`|`CallOptions`|要验证的调用选项|
|`revertOptions`|`RevertOptions`|要验证的回退选项|
|`messageLength`|`uint256`|消息的长度|

#### validateWithdrawalParams

*验证标准提款参数*

```solidity
function validateWithdrawalParams(
    bytes memory receiver,
    uint256 amount,
    RevertOptions calldata revertOptions
)
    internal
    pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`receiver`|`bytes`|接收者地址|
|`amount`|`uint256`|要提款的金额|
|`revertOptions`|`RevertOptions`|回退选项|

#### validateWithdrawalAndCallParams

*验证提款和调用参数*

```solidity
function validateWithdrawalAndCallParams(
    bytes memory receiver,
    uint256 amount,
    bytes calldata message,
    CallOptions calldata callOptions,
    RevertOptions calldata revertOptions
)
    internal
    pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`receiver`|`bytes`|接收者地址|
|`amount`|`uint256`|要提款的金额|
|`message`|`bytes`|要发送的消息|
|`callOptions`|`CallOptions`|调用选项|
|`revertOptions`|`RevertOptions`|回退选项|

#### validateDepositParams

*验证存款参数*

```solidity
function validateDepositParams(
    address zrc20,
    uint256 amount,
    address target,
    address protocolAddress,
    address contractAddress
)
    internal
    pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`zrc20`|`address`|ZRC20 代币地址|
|`amount`|`uint256`|要存款的金额|
|`target`|`address`|目标地址|
|`protocolAddress`|`address`|协议地址|
|`contractAddress`|`address`|合约地址|

#### validateExecuteParams

*验证执行参数*

```solidity
function validateExecuteParams(address zrc20, address target) internal pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`zrc20`|`address`|ZRC20 代币地址|
|`target`|`address`|目标地址|

#### validateZetaDepositParams

*验证 ZETA 存款和调用参数*

```solidity
function validateZetaDepositParams(
    uint256 amount,
    address target,
    address protocolAddress,
    address contractAddress
)
    internal
    pure;
```
**参数**

|名称|类型|描述|
|----|----|-----------|
|`amount`|`uint256`|要存款的金额|
|`target`|`address`|目标地址|
|`protocolAddress`|`address`|协议地址|
|`contractAddress`|`address`|合约地址|

### 错误
#### EmptyAddress
表示提供了空地址的错误。

```solidity
error EmptyAddress();
```

## SystemContract

[Git 源码](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/SystemContract.sol)

*系统合约由协议调用以与区块链交互。还包括许多工具，使与 ZetaChain 的交互更加容易。*

### 状态变量

#### gasPriceByChainId
映射，用于根据链 ID 获取每个链的 gas 价格。

```solidity
mapping(uint256 => uint256) public gasPriceByChainId;
```

#### gasCoinZRC20ByChainId
映射，用于根据链 ID 获取代币的 ZRC20 地址，例如 zETH、zBNB 等。

```solidity
mapping(uint256 => address) public gasCoinZRC20ByChainId;
```

#### gasZetaPoolByChainId

```solidity
mapping(uint256 => address) public gasZetaPoolByChainId;
```

#### FUNGIBLE_MODULE_ADDRESS
可互换模块地址始终相同，它在协议级别。

```solidity
address public constant FUNGIBLE_MODULE_ADDRESS = 0x735b14BB79463307AAcBED86DAf3322B1e6226aB;
```

#### uniswapv2FactoryAddress
Uniswap V2 地址。

```solidity
address public immutable uniswapv2FactoryAddress;
```

#### uniswapv2Router02Address

```solidity
address public immutable uniswapv2Router02Address;
```

#### wZetaContractAddress
用于与 Uniswap V2 交互的包装 ZETA 地址。

```solidity
address public wZetaContractAddress;
```

#### zetaConnectorZEVMAddress
ZEVM Zeta 连接器地址。

```solidity
address public zetaConnectorZEVMAddress;
```

### 函数

#### constructor

*只有可互换模块可以部署系统合约。*

```solidity
constructor(address wzeta_, address uniswapv2Factory_, address uniswapv2Router02_);
```

#### depositAndCall

*将外部代币存入 ZRC20 并调用用户在 zEVM 上指定的合约。*

```solidity
function depositAndCall(
    zContext calldata context,
    address zrc20,
    uint256 amount,
    address target,
    bytes calldata message
)
    external;
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`context`|`zContext`||
|`zrc20`|`address`||
|`amount`|`uint256`||
|`target`|`address`||
|`message`|`bytes`||

#### sortTokens

*按字典序排序代币地址。用于处理按顺序排序的交易对返回值。*

```solidity
function sortTokens(address tokenA, address tokenB) internal pure returns (address token0, address token1);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`tokenA`|`address`||
|`tokenB`|`address`||

**返回值**

|名称|类型|描述|
|----|----|-----------|
|`token0`|`address`|token1，返回排序后的代币地址。|
|`token1`|`address`||

#### uniswapv2PairFor

*计算交易对的 CREATE2 地址，无需进行任何外部调用。*

```solidity
function uniswapv2PairFor(address factory, address tokenA, address tokenB) public pure returns (address pair);
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`factory`|`address`||
|`tokenA`|`address`||
|`tokenB`|`address`||

**返回值**

|名称|类型|描述|
|----|----|-----------|
|`pair`|`address`|代币交易对地址。|

#### setGasPrice

*可互换模块定期更新 gas 价格预言机。*

```solidity
function setGasPrice(uint256 chainID, uint256 price) external;
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainID`|`uint256`||
|`price`|`uint256`||

#### setGasCoinZRC20

*gasCoinZRC20ByChainId 映射的设置器。*

```solidity
function setGasCoinZRC20(uint256 chainID, address zrc20) external;
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainID`|`uint256`||
|`zrc20`|`address`||

#### setGasZetaPool

*设置 wzeta/erc20 交易对地址。*

```solidity
function setGasZetaPool(uint256 chainID, address erc20) external;
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`chainID`|`uint256`||
|`erc20`|`address`||

#### setWZETAContractAddress

*包装 ZETA 地址的设置器。*

```solidity
function setWZETAContractAddress(address addr) external;
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`addr`|`address`||

#### setConnectorZEVMAddress

*zetaConnector ZEVM 地址的设置器*

```solidity
function setConnectorZEVMAddress(address addr) external;
```

**参数**

|名称|类型|描述|
|----|----|-----------|
|`addr`|`address`||

### 事件

#### SystemContractDeployed
自定义 SystemContract 错误。

```solidity
event SystemContractDeployed();
```

#### SetGasPrice

```solidity
event SetGasPrice(uint256, uint256);
```

#### SetGasCoin

```solidity
event SetGasCoin(uint256, address);
```

#### SetGasZetaPool

```solidity
event SetGasZetaPool(uint256, address);
```

#### SetWZeta

```solidity
event SetWZeta(address);
```

#### SetConnectorZEVM

```solidity
event SetConnectorZEVM(address);
```

## SystemContractErrors

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/SystemContract.sol)

*SystemContract 的自定义错误*

### 错误
#### CallerIsNotFungibleModule

```solidity
error CallerIsNotFungibleModule();
```

#### InvalidTarget

```solidity
error InvalidTarget();
```

#### CantBeIdenticalAddresses

```solidity
error CantBeIdenticalAddresses();
```

#### CantBeZeroAddress

```solidity
error CantBeZeroAddress();
```

#### ZeroAddress

```solidity
error ZeroAddress();
```

## WETH9

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/WZETA.sol)

### 状态变量

#### name

```solidity
string public name = "Wrapped Ether";
```

#### symbol

```solidity
string public symbol = "WETH";
```

#### decimals

```solidity
uint8 public decimals = 18;
```

#### balanceOf

```solidity
mapping(address => uint256) public balanceOf;
```

#### allowance

```solidity
mapping(address => mapping(address => uint256)) public allowance;
```

### 函数

#### receive

```solidity
receive() external payable;
```

#### deposit

```solidity
function deposit() public payable;
```

#### withdraw

```solidity
function withdraw(uint256 wad) public;
```

#### totalSupply

```solidity
function totalSupply() public view returns (uint256);
```

#### approve

```solidity
function approve(address guy, uint256 wad) public returns (bool);
```

#### transfer

```solidity
function transfer(address dst, uint256 wad) public returns (bool);
```

#### transferFrom

```solidity
function transferFrom(address src, address dst, uint256 wad) public returns (bool);
```

### 事件

#### Approval

```solidity
event Approval(address indexed src, address indexed guy, uint256 wad);
```

#### Transfer

```solidity
event Transfer(address indexed src, address indexed dst, uint256 wad);
```

#### Deposit

```solidity
event Deposit(address indexed dst, uint256 wad);
```

#### Withdrawal

```solidity
event Withdrawal(address indexed src, uint256 wad);
```

## ZRC20

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/ZRC20.sol)

### 状态变量

#### FUNGIBLE_MODULE_ADDRESS
同质化模块地址始终相同，在协议级别维护。

```solidity
address public constant FUNGIBLE_MODULE_ADDRESS = 0x735b14BB79463307AAcBED86DAf3322B1e6226aB;
```

#### CHAIN_ID
链 ID。

```solidity
uint256 public immutable CHAIN_ID;
```

#### COIN_TYPE
代币类型，请查看 `Interfaces.sol`。

```solidity
CoinType public immutable COIN_TYPE;
```

#### SYSTEM_CONTRACT_ADDRESS
系统合约地址。

*变量名使用大写以保持与 ZRC20.sol v1 的兼容性*

```solidity
address public SYSTEM_CONTRACT_ADDRESS;
```

#### GAS_LIMIT
Gas 限制。

*变量名使用大写以保持与 ZRC20.sol v1 的兼容性*

```solidity
uint256 public GAS_LIMIT;
```

#### PROTOCOL_FLAT_FEE
协议固定费用。

*变量名使用大写以保持与 ZRC20.sol v1 的兼容性*

```solidity
uint256 public override PROTOCOL_FLAT_FEE;
```

#### _balances

```solidity
mapping(address => uint256) private _balances;
```

#### _allowances

```solidity
mapping(address => mapping(address => uint256)) private _allowances;
```

#### _totalSupply

```solidity
uint256 private _totalSupply;
```

#### _name

```solidity
string private _name;
```

#### _symbol

```solidity
string private _symbol;
```

#### _decimals

```solidity
uint8 private _decimals;
```

#### gatewayAddress
网关合约地址。

*此变量添加在最后位置以保持与 ZRC20.sol v1 的存储布局兼容*

```solidity
address public gatewayAddress;
```

### 函数

#### _msgSender

```solidity
function _msgSender() internal view virtual returns (address);
```

#### onlyFungible

*仅限同质化模块修饰符。*

```solidity
modifier onlyFungible();
```

#### constructor

*唯一允许部署新 ZRC20 的是同质化模块地址。*

```solidity
constructor(
    string memory name_,
    string memory symbol_,
    uint8 decimals_,
    uint256 chainid_,
    CoinType coinType_,
    uint256 gasLimit_,
    address systemContractAddress_,
    address gatewayAddress_
);
```

#### name

*ZRC20 名称*

```solidity
function name() public view virtual override returns (string memory);
```

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `string` | 名称字符串 |

#### setName

*名称可由同质化模块账户更新。*

```solidity
function setName(string memory newName) external override onlyFungible;
```

#### setSymbol

*符号可由同质化模块账户更新。*

```solidity
function setSymbol(string memory newSymbol) external override onlyFungible;
```

#### symbol

*ZRC20 符号。*

```solidity
function symbol() public view virtual override returns (string memory);
```

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `string` | 符号字符串 |

#### decimals

*ZRC20 小数位数。*

```solidity
function decimals() public view virtual override returns (uint8);
```

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `uint8` | 返回 uint8 小数位数 |

#### totalSupply

*ZRC20 总供应量。*

```solidity
function totalSupply() public view virtual override returns (uint256);
```

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `uint256` | 返回 uint256 总供应量 |

#### balanceOf

*返回账户的 ZRC20 余额。*

```solidity
function balanceOf(address account) public view virtual override returns (uint256);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `account` | `address` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `uint256` | uint256 账户余额 |

#### transfer

*转移 ZRC20 代币到接收者。*

```solidity
function transfer(address recipient, uint256 amount) public virtual override returns (bool);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `recipient` | `address` |  |
| `amount` | `uint256` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `bool` | 成功/失败返回 true/false |

#### allowance

*返回从所有者到支出者的代币授权额度。*

```solidity
function allowance(address owner, address spender) public view virtual override returns (uint256);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `owner` | `address` |  |
| `spender` | `address` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `uint256` | uint256 授权额度 |

#### approve

*批准支出者使用指定金额的 transferFrom。*

```solidity
function approve(address spender, uint256 amount) public virtual override returns (bool);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `spender` | `address` |  |
| `amount` | `uint256` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `bool` | 成功/失败返回 true/false |

#### transferFrom

*从发送者向接收者转移代币。*

```solidity
function transferFrom(address sender, address recipient, uint256 amount) public virtual override returns (bool);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `sender` | `address` |  |
| `recipient` | `address` |  |
| `amount` | `uint256` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `bool` | 成功/失败返回 true/false |

#### burn

*销毁指定数量的代币。*

```solidity
function burn(uint256 amount) external override returns (bool);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `amount` | `uint256` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `bool` | 成功/失败返回 true/false |

#### _transfer

```solidity
function _transfer(address sender, address recipient, uint256 amount) internal virtual;
```

#### _mint

```solidity
function _mint(address account, uint256 amount) internal virtual;
```

#### _burn

```solidity
function _burn(address account, uint256 amount) internal virtual;
```

#### _approve

```solidity
function _approve(address owner, address spender, uint256 amount) internal virtual;
```

#### deposit

*从外部链存入相应代币，仅可由同质化模块调用。*

```solidity
function deposit(address to, uint256 amount) external override returns (bool);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `to` | `address` |  |
| `amount` | `uint256` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `bool` | 成功/失败返回 true/false |

#### withdrawGasFee

*提取 Gas 费用。*

```solidity
function withdrawGasFee() public view override returns (address, uint256);
```

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `address` | 返回此 ZRC20 同链的 Gas ZRC20 地址，并计算 withdraw() 的 Gas 费用 |
| `<none>` | `uint256` |  |

#### withdrawGasFeeWithGasLimit

*使用指定 gasLimit 提取 Gas 费用*

```solidity
function withdrawGasFeeWithGasLimit(uint256 gasLimit) public view override returns (address, uint256);
```

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `address` | 返回此 ZRC20 同链的 Gas ZRC20 地址，并计算 withdraw() 的 Gas 费用 |
| `<none>` | `uint256` |  |

#### withdraw

*将 ZRC20 代币提取到外部链，此函数会触发 cctx 模块向出链发送出站交易
此合约应被授予足够的 Gas ZRC20 授权额度以支付出站交易 Gas 费用。*

```solidity
function withdraw(bytes memory to, uint256 amount) external override returns (bool);
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `to` | `bytes` |  |
| `amount` | `uint256` |  |

**返回值**

| 名称 | 类型 | 描述 |
|------|------|------|
| `<none>` | `bool` | 成功/失败返回 true/false |

#### updateSystemContractAddress

*更新系统合约地址。仅可由同质化模块更新。*

```solidity
function updateSystemContractAddress(address addr) external onlyFungible;
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `addr` | `address` |  |

#### updateGatewayAddress

*更新网关合约地址。仅可由同质化模块更新。*

```solidity
function updateGatewayAddress(address addr) external onlyFungible;
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `addr` | `address` |  |

#### updateGasLimit

*更新 Gas 限制。仅可由同质化模块更新。*

```solidity
function updateGasLimit(uint256 gasLimit_) external onlyFungible;
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `gasLimit_` | `uint256` |  |

#### updateProtocolFlatFee

*更新协议固定费用。仅可由同质化模块更新。*

```solidity
function updateProtocolFlatFee(uint256 protocolFlatFee_) external onlyFungible;
```

**参数**

| 名称 | 类型 | 描述 |
|------|------|------|
| `protocolFlatFee_` | `uint256` |  |

## ZRC20Errors

[Git Source](https://github.com/zeta-chain/protocol-contracts/blob/main/contracts/zevm/ZRC20.sol)

*ZRC20 自定义错误*

### 错误列表
#### CallerIsNotFungibleModule

```solidity
error CallerIsNotFungibleModule();
```

#### InvalidSender

```solidity
error InvalidSender();
```

#### GasFeeTransferFailed

```solidity
error GasFeeTransferFailed();
```

#### ZeroGasCoin

```solidity
error ZeroGasCoin();
```

#### ZeroGasPrice

```solidity
error ZeroGasPrice();
```

#### LowAllowance

```solidity
error LowAllowance();
```

#### LowBalance

```solidity
error LowBalance();
```

#### ZeroAddress

```solidity
error ZeroAddress();
```