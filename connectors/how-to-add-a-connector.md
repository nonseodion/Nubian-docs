# How to add a connector

How to add a new connector

You can create a new pull request \(PR\) to add a new connector. Your PR has to meet some requirements to get merged. We explain them here.

## A new connector should follow the current directory structure

Files common to all connectors are in the `contracts/common` directory.

* `math.sol` has methods for mathematical operations \(`DSMath`\)
* `interfaces.sol` contains the common interfaces
  * `TokenInterface` for ERC-20 interface including WETH
* `stores.sol` contains the global constants as well as methods `getId` & `setId` \(`Stores`\)
* `basic.sol` inherits `DSMath` & `Stores` contracts. This contains few details explained below
  * Wrapping & unwrapping ETH \(`convertEthToWeth` & `convertWethToEth`\)
  * Getting token & ETH balance of DSA

Connectors are under the `contracts/connectors` directory and should be formatted as follows:

* Connector events should be in a separate contract: `events.sol`
* Define interfaces in a separate file: `interface.sol`
* If the connector has helper methods & constants \(including interface instances\), this should be defined in a separate file: `helpers.sol`
  * `Helpers` contract should inherit `Basic` contract from the common directory
  * If the connector doesn't have any helper methods, the main contract should inherit the `Basic` contract.
* The main logic of the contract should be under `main.sol`, and the contract should inherit `Helpers` \(if it exists, otherwise `Basic`\) and `Events` contracts.

Few things to consider while writing the connector:

* The connector should have a public string `name`. It should be the name of the connector and should be versioned. Ex: `Venus-v1`
* User interacting methods \(`external` methods\) will not be emitting events. They will return two variables:
  * `_eventName` of `string` type: This will be the event signture defined in the `Events` contract. Ex: `LogDeposit(address,address,uint256,uint256,uint256)`
  * `_eventParam` of `bytes` type: This will be the abi encoded event parameters
* The contracts should not have `selfdestruct()`
* The contracts should not have `delegatecall()`
* Use `uint(-1)` for maximum amount everywhere
* Use `ethAddr` \(declared in `Stores`\) to denote Ethereum \(non-ERC20\)
* Use `address(this)` instead of `msg.sender` for fetching balance on-chain, etc
* Only `approve()` limited amount while giving ERC20 allowance, which strictly needs to be 0 by the end of the spell.
* Use `getUint()` \(declared in `Stores`\) for getting value that saved from previous spell
* Use `setUint()` \(declared in `Stores`\) for setting value to save for the future spell

## Support

