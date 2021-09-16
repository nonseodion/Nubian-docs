---
sidebar_position: 1
label: Introduction
---

# DeFi Smart Account \(DSA\)

A Decentralized Finance \(DeFi\) Smart Account \(DSA\) is a smart contract account that enables users to interact with the DeFi ecosystem with ease. The Nubian Finance Ecosystem is built for developers and users to leverage the full potential of the ecosystem using smart accounts. The upgradability and extensibility of smart accounts allow them to support new protocols. It makes use of account extensions to give the smart accounts additional features and capabilities. These extensions are added to improve the smart account's core functionalities like adding and removing owners, perform complex DeFi operations, interact with DeFi protocols or do almost anything.

## How DSA works

The main contract of the DSA is a proxy contract that uses a fallback to receive all the calls. The DSA executes each account interaction in this order:

* Intercepts the call with a `fallback` that sends the `msg.sig` to the implementations contract.
* The implementations contract receives the `msg.sig` and returns the address of the account extension called. It stores a mapping of function signatures and the extension implementing them.
* The remaining execution is delegated to the returned address using solidity's `delegate` function.

From the above execution, the smart account consists of a proxy, implementations contract and various account extensions listed in the implementations contract.

[Connectors](../connectors/) are a core part of the Nubian ecosystem an account extension allows the smart account to interact with them.

