---
sidebar_position: 2
---

# DSA Contracts

## Registry

These contracts deploy the smart accounts, manage and record smart account contracts and their authorities/owners.

* \*\*\*\*[**NbnIndex**](registry/nbnindex.md): Creates new smart accounts.
* \*\*\*\*[**NbnList**](registry/nbnlist.md): Records the deployed smart accounts and their authorities/owners.

## Core contracts

The core contracts enable the smart account to perform its two core functions, execute function calls and update account extensions. They are:

* \*\*\*\*[**NbnAccountV2**](core/nbnaccountv2.md): Executes all function calls to the smart account.
* \*\*\*\*[**NbnImplementations**](core/nbnimplementations.md): Adds, removes, and stores the list of account extensions.

## Account Extensions

The account extensions add more features to the smart accounts. The Nubian finance team has added two extensions:

* \*\*\*\*[**NbnDefaultImplementation**](implementations/nbndefaultimplementation.md): Adds and removes owners called authorities from the account.
* \*\*\*\*[**NbnImplementationM1**](implementations/nbnimplementationm1.md): This allows the smart account to cast spells which are functions that interact with DeFi protocols using [connectors](../connectors/connectors-explained.md).

