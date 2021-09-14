# NbnList

Used to manage DeFi Smart Accounts \(DSAs\) and their owners or authorities. It is called by NbnIndex when setting up a new DSA and used by a DSA authority to remove or add other authorities.

## Address

NbnList is deployed on [mainnet](https://bscscan.com/address/0x58f4D59E4D4A97758d56487Dbbe5e083Af89cf9D).

## Code

[list.sol](https://github.com/Open-Currency-Collective/nubian-dsa-contracts/blob/master/contracts/registry/list.sol)

## State-Changing Methods

### Init

```text
function init(address  _account) external
```

Gives a DSA its initial configuration.

#### Parameter

| Parameter | Type | Description |
| :--- | :--- | :--- |
| \_account | `address` | The DSA address. |

### AddAuth

```text
function addAuth(address _owner) external;
```

Adds `_owner` as an authority over the DSA that calls it. `_owner` must not already be an authority.

#### Parameter

| Parameter | Type | Description |
| :--- | :--- | :--- |
| \_owner | `address` | The new authority. |

### RemoveAuth

```text
function removeAuth(address _owner) external;
```

Removes `_owner` as an authority over the DSA that calls it. `_owner` must already be an authority.

#### Parameter

| Parameter | Type | Description |
| :--- | :--- | :--- |
| \_owner | `address` | The old authority. |

