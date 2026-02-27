# EIP-7702 (Set Code for EOAs)

**EIP-7702** is an Ethereum core protocol change that introduces a new transaction type allowing an **Externally Owned Account (EOA)** to **set its account code** to a special *delegation indicator* that points to code deployed at another address. This enables an EOA to execute logic “as if” it were a smart contract account, while retaining its existing address.

## Overview

EIP-7702 introduces a new [EIP-2718](https://eips.ethereum.org/EIPS/eip-2718) typed transaction (type `0x04`) that attaches an `authorization_list` of signed tuples. For each valid tuple, the protocol writes a *delegation indicator* into the authorizing account’s code, in the form `0xef0100 || address` (where `address` is a 20-byte pointer). The `0xef` prefix is the banned opcode marker from [EIP-3541](https://eips.ethereum.org/EIPS/eip-3541), ensuring the indicator is not interpreted as normal EVM bytecode. In the EIP’s specification, the authorization tuple format is `[chain_id, address, nonce, y_parity, r, s]`.

Once an account is delegated, code-executing operations (including `CALL`, `CALLCODE`, `DELEGATECALL`, and `STATICCALL`) must load the code at the referenced `address` and execute it in the context of the delegating EOA.

## Motivation and intended capabilities

The EIP’s motivation is to make common “smart wallet” UX improvements available to existing EOAs without requiring users to migrate funds and identity to a new contract account. The proposal highlights three broad capability buckets:

- **Batching**: combining multiple actions into a single atomic transaction.
- **Sponsorship**: enabling another party to pay gas on the user’s behalf (or be repaid in another asset).
- **Privilege de-escalation**: using sub-keys or scoped authorizations that are weaker than full account control.

These are described as short-term functionality improvements aimed at accelerating adoption of better wallet UX across applications.

## Delegation semantics (high level)

A set-code transaction may process multiple authorizations (potentially affecting multiple EOAs) before the transaction’s execution phase begins. Per the specification:

- The authorization list is processed after the sender’s nonce is incremented, but before the execution portion of the transaction.
- If transaction execution later fails (including a revert), processed delegation indicators are **not rolled back**.
- Delegation is persistent until changed; setting `address` to `0x0000000000000000000000000000000000000000` clears the account’s code.
- When multiple tuples from the same authority are present, the last valid occurrence determines the final delegated address.

## Relationship to account abstraction (ERC-4337)

EIP-7702 is often discussed alongside account abstraction mechanisms such as [ERC-4337](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-4337.md). Where ERC-4337 uses an alternative mempool and a standardized entry point contract, EIP-7702 changes the protocol rules for EOAs directly by adding a new transaction type and delegation behavior.

## References

- Ethereum Improvement Proposals: **EIP-7702: Set Code for EOAs** — https://eips.ethereum.org/EIPS/eip-7702
- Ethereum Improvement Proposals: **EIP-2718: Typed Transaction Envelope** — https://eips.ethereum.org/EIPS/eip-2718
- Ethereum Improvement Proposals: **EIP-3541: Reject new contracts starting with the 0xEF byte** — https://eips.ethereum.org/EIPS/eip-3541
- Ethereum Magicians discussion: https://ethereum-magicians.org/t/eip-7702-set-eoa-account-code/19923
- Turnkey (overview article): https://www.turnkey.com/blog/account-abstraction-erc-4337-eip-7702
