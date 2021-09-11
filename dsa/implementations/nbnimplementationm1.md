# NbnImplementationM1

Adds the [connectors](../../connectors/connector) functionality to the DSA. This extension is used to interact with connectors. Connectors allow DSAs to interact with DeFi protocols. All function calls to connectors are called spells and this extension routes the spell to the right connector. These spells can be combined together to perform complex to simple behaviours in a single transaction. To integrate with a new DeFi protocol simply requires a connector for that protocol to be added. We encourage developers to build connectors or request for the addition of new connectors. Check [how to add a connector](../../connectors/how-to-add-a-connector.md) for more information.

## Address

Autofarm connector is deployed on [mainnet](https://bscscan.com/address/0xd29aFdfBCad1C249b0c69Eb2785b08353029282B).

## Events

### LogCast <a id="LogCast"></a>

```text
event LogCast(
    address indexed origin,
    address indexed sender,
    uint256 value,
    string[] targetsNames,
    address[] targets,
    string[] eventNames,
    bytes[] eventParams
);
```

Emitted when spells are cast i.e when [cast](nbnimplementationm1.md#Cast) is called. It combines all the events from each connector and emits them once. This saves gas cost and allows for a single point of reference.

## Code

[implementation\_m1.sol](https://github.com/Open-Currency-Collective/nubian-dsa-contracts/blob/master/contracts/v2/accounts/Implementation_m1.sol)

## Read-only methods

### nbnIndex

```text
address internal immutable nbnIndex;
```

Returns the address of NbnIndex. NbnIndex can cast a spell during smart account creation using this extension.

### ConnectorsM1

```text
address public immutable connectorsM1;
```

Returns the address of the connectors contract, this contract has a record of all the connectors and is used to add and remove connectors.

### DecodeEvent

```text
function decodeEvent(bytes memory response) internal pure returns (string memory _eventCode, bytes memory _eventParams)
```

Used to retrieve an event's name and parameters from an abi encoded response. Spells return their events in an abi encoded format.

|  |
| :--- |


#### Parameter

| Parameter | Type | Description |
| :--- | :--- | :--- |
| response | `bytes` | Abi encoded return value from a spell.  |

## State-changing methods

### Spell <a id="Spell"></a>

```text
function spell(address _target, bytes memory _data) internal returns (bytes memory response);
```

Used to cast an individual spell by delegating to _\_target_ and passing the parameters. It does this using assembly code.

#### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| target | `address` | The address of the connector to be called. |
| \_data | `bytes` | Abi encoded parameters to be passed to target. |

### Cast <a id="Cast"></a>

```text
function cast(
    string[] calldata _targetNames,
    bytes[] calldata _datas,
    address _origin
)
external
payable
returns (bytes32)
```

It casts all the spells it receives using [spell](nbnimplementationm1.md#Spell) and logs their events once using [LogCast](nbnimplementationm1.md#LogCast).

#### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| \_targetNames | `string[]` | Names of all connectors to be used in casting the spells. |
| \_datas | `bytes[]` | Abi encoded parameters to be passed to the corresponding \_targetNames connector. |
| \_origin | `address` | The address to track the origin of transaction. Used for analytics and affiliates. |

