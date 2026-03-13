# EIP-7702 (Set Code for EOAs)

**EIP-7702** is an Ethereum core protocol change that introduces a new transaction type allowing an **Externally Owned Account (EOA)** to **set its account code** to a special *delegation indicator* that points to code deployed at another address. This enables an EOA to execute logic “as if” it were a smart contract account, while retaining its existing address.

## Overview

EIP-7702 introduces a new [EIP-2718](https://eips.ethereum.org/EIPS/eip-2718) typed transaction (type `0x04`) sometimes described as a **set code transaction**. The transaction carries an `authorization_list` of signed tuples; for each valid tuple, the protocol writes a delegation indicator into the authorizing account’s code.

- Authorization tuple format: `[chain_id, address, nonce, y_parity, r, s]`.
- Delegation indicator format: `0xef0100 || address`.
- The `0xef` prefix is the banned opcode marker from [EIP-3541](https://eips.ethereum.org/EIPS/eip-3541), ensuring the indicator is not interpreted as normal EVM bytecode.

Once an account is delegated, code-executing operations must load and execute the code pointed to by the delegation indicator (i.e., the referenced `address`) in the context of the delegating EOA.

## Motivation and intended capabilities

The EIP’s motivation is to make common “smart wallet” UX improvements available to existing EOAs without requiring users to migrate funds and identity to a new contract account. The proposal highlights three broad capability buckets:

- **Batching**: combining multiple actions into a single atomic transaction.
- **Sponsorship**: enabling another party to pay gas on the user’s behalf (or be repaid in another asset).
- **Privilege de-escalation**: using sub-keys or scoped authorizations that are weaker than full account control.

These are described as short-term functionality improvements aimed at accelerating adoption of better wallet UX across applications.

## Delegation semantics (high level)

A set-code transaction may include multiple authorization tuples and (if valid) update multiple EOAs’ code before the transaction’s execution phase. Per the specification:

- The authorization list is processed before the execution portion of the transaction begins (after the sender’s nonce is incremented).
- If transaction execution later fails (including a revert), processed delegation indicators are **not rolled back**.
- Delegation can be cleared by setting the delegated `address` to `0x0000000000000000000000000000000000000000`.
- When multiple tuples from the same authority are present, the last valid occurrence determines the final delegated address.

## Affected EVM operations

EIP-7702 specifies that delegation affects the behavior of code-executing operations, including `CALL`, `CALLCODE`, `DELEGATECALL`, and `STATICCALL`.

## Relationship to account abstraction (ERC-4337)

EIP-7702 is often discussed alongside account abstraction mechanisms such as [ERC-4337](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-4337.md). Where ERC-4337 uses an alternative mempool and a standardized entry point contract, EIP-7702 changes the protocol rules for EOAs directly by adding a new transaction type and delegation behavior.

## References

- Ethereum Improvement Proposals: **EIP-7702: Set Code for EOAs** — https://eips.ethereum.org/EIPS/eip-7702
- Ethereum Improvement Proposals: **EIP-2718: Typed Transaction Envelope** — https://eips.ethereum.org/EIPS/eip-2718
- Ethereum Improvement Proposals: **EIP-3541: Reject new contracts starting with the 0xEF byte** — https://eips.ethereum.org/EIPS/eip-3541
- OpenZeppelin Contracts documentation: **EOA Delegation (EIP-7702)** — https://docs.openzeppelin.com/contracts/5.x/eoa-delegation
- Discussion thread (Ethereum Magicians): https://ethereum-magicians.org/t/eip-7702-set-eoa-account-code/19923
- Turnkey (overview article): https://www.turnkey.com/blog/account-abstraction-erc-4337-eip-7702
