# NbnDefaultImplementation

Used to add and remove authorities, owners of a DeFi Smart Account \(DSA\). It is used by NbnIndex to add the new owner when a DSA is created.

## Address

NbnDefaultImplementation is deployed on [mainnet](https://bscscan.com/address/0xc9Fc01064Ad33ACaa4534dA4604Fd6602CEF873d).

## Code

[implementation\_default.sol](https://github.com/Open-Currency-Collective/nubian-dsa-contracts/blob/master/contracts/v2/accounts/implementation_default.sol)

## Events

### LogEnableUser

```text
event LogEnableUser(address indexed user);
```

Emitted when a new authority is added to a DSA.

### LogDisableUser

```text
event LogDisableUser(address indexed user);
```

Emitted when an authority is removed.

## Read-only methods

### ImplementationVersion

```text
uint public constant implementationVersion = 1;
```

Returns the implementation version.

### NbnIndex

```text
address public immutable nbnIndex;
```

Returns the address of the nbnIndex. NbnIndex is used to create smart accounts and assigns the first owner.

### Version

```text
uint public constant version = 2;
```

Returns the version of the DSA contract.

### IsAuth

```text
function isAuth(address user) public view returns (bool);
```

Used to check if user has control over a DSA. It returns a boolean value, true if it is an authority false if otherwise.

#### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| user | `address` | The address to be checked. |

## State-changing methods

### Enable

```text
function enable(address user) public;
```

Adds an address as a new authority. _user_ must not already be an authority else the transaction reverts. This gives _user_ complete control over a DSA.

#### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| user | `address` | The new authority. |

### disable

```text
function disable(address user) public;
```

Removes an address from the authorities of a smart account. The address must already be an authority, or else the transaction is reverted. This removes all rights over a smart account from _user_.

#### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| user | `address` | The authority to remove. |

