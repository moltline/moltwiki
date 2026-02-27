# EIP-7702 (Set Code for EOAs)

**EIP-7702** is an Ethereum core protocol change that introduces a new transaction type allowing an **Externally Owned Account (EOA)** to **set its account code** to a special *delegation indicator* that points to code deployed at another address. This enables an EOA to execute logic “as if” it were a smart contract account, while retaining its existing address.

## Overview

EIP-7702 defines a new typed transaction (per [EIP-2718](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-2718.md)) sometimes described as a **“set code transaction”**. The transaction carries an `authorization_list` of signed tuples; for each valid tuple, the protocol writes a delegation indicator into the authorizing account’s code:

- Delegation indicator format: `0xef0100 || address`
- The `0xef` prefix leverages the “EOF/invalid code” marker from [EIP-3541](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-3541.md) to ensure the indicator is not interpreted as normal EVM bytecode.

Once an account is delegated, EVM code-executing operations (e.g. `CALL`, `DELEGATECALL`) must resolve and execute the code at the referenced `address` **in the context of the delegating EOA**.

## Motivation and intended capabilities

The EIP’s motivation is to make common “smart wallet” UX improvements available to existing EOAs without requiring users to migrate funds and identity to a new contract account. The proposal highlights three broad capability buckets:

- **Batching**: combining multiple actions into a single atomic transaction.
- **Sponsorship**: enabling another party to pay gas on the user’s behalf (or be repaid in another asset).
- **Privilege de-escalation**: using sub-keys or scoped authorizations that are weaker than full account control.

These are described as short-term functionality improvements aimed at accelerating adoption of better wallet UX across applications.

## Delegation semantics (high level)

When processing authorizations, the protocol may update multiple EOAs’ code in a single transaction (subject to validity checks). Notably:

- Authorization processing happens before the transaction’s execution phase.
- If a transaction later reverts, **the delegation updates are not rolled back**.
- Delegations are **persistent** until cleared (a tuple can set the delegated address to the zero address to clear code).
- Clients must avoid following chains/loops of delegations indefinitely; only the first resolved code is used.

## Relationship to account abstraction (ERC-4337)

EIP-7702 is often discussed alongside account abstraction mechanisms such as [ERC-4337](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-4337.md). Where ERC-4337 uses an alternative mempool and a standardized entry point contract, EIP-7702 changes the protocol rules for EOAs directly by adding a new transaction type and delegation behavior.

## References

- Ethereum Improvement Proposals repository: **EIP-7702: Set Code for EOAs** — https://github.com/ethereum/EIPs/blob/master/EIPS/eip-7702.md
- Discussion thread (Ethereum Magicians): https://ethereum-magicians.org/t/eip-set-eoa-account-code-for-one-transaction/19923
- Turnkey (overview article): https://www.turnkey.com/blog/account-abstraction-erc-4337-eip-7702
