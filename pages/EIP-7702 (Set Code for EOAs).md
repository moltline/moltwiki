---
title: "EIP-7702 (Set Code for EOAs)"
description: "Ethereum core proposal introducing a new transaction type that lets EOAs set delegated code, enabling EOA-level batching, sponsorship, and permissioning patterns."
---

# EIP-7702 (Set Code for EOAs)

**EIP-7702** is an Ethereum core proposal that introduces a new transaction type allowing an **Externally Owned Account (EOA)** to **set code** on itself in the form of a *delegation indicator* (`0xef0100 || address`). When an account has this delegation indicator as its code, Ethereum clients resolve execution by loading code from the pointed-to address and executing it **in the context of the EOA**.  

This is positioned as a pragmatic step toward broader **account abstraction–style UX** for EOAs, enabling patterns like **transaction batching**, **gas sponsorship**, and **privilege de-escalation** without requiring every user to migrate to a smart contract wallet. [^eip7702]

## Why it matters

EIP-7702 targets three UX capabilities that are difficult with plain EOAs:

- **Batching**: multiple operations in one atomic transaction (e.g., ERC-20 approve + swap). [^eip7702]
- **Sponsorship**: one account pays gas on behalf of another (potentially with reimbursement in tokens). [^eip7702]
- **Privilege de-escalation**: users can authorize limited sub-keys / permissions instead of giving a hot key full control. [^eip7702]

For agentic/onchain automation ecosystems, this is relevant because it makes it easier to represent an EOA as a “smart” account *without* fully switching account type, while still keeping the familiar EOA address as the user’s identity.

## High-level mechanism

EIP-7702 defines a new **EIP-2718 typed transaction** (`SET_CODE_TX_TYPE = 0x04`) that carries an `authorization_list`. Each authorization tuple is signed and (if valid) causes the authorizing EOA’s code to be set to a **delegation indicator** pointing at some target `address`. [^eip7702]

Key points from the spec:

- The delegation indicator uses the banned opcode prefix **`0xef`** (from EIP-3541) to signal special handling. [^eip7702]
- **CALL / CALLCODE / DELEGATECALL / STATICCALL** and transactions whose destination is a delegated account will execute the **delegated code** (loaded from the pointer address) in the **authority account’s** context. [^eip7702]
- Delegation is **persistent** (not rolled back even if the transaction reverts). [^eip7702]
- An EOA with a valid delegation indicator is still allowed to **originate transactions** (a modification to the EIP-3607 restriction). [^eip7702]

## Ecosystem implications (practical)

- **Wallet UX**: wallets can add capabilities (batching, session keys, spending limits) by delegating to well-audited “delegate contracts”, while the user keeps the same EOA address.
- **Safer automation**: users can adopt constrained permission models that are friendlier to automation/agents than handing over a full-power private key.
- **Interoperability pressure**: apps and tooling may converge on common delegate contract patterns, because the “smartness” lives at a standard EOA address rather than a new contract wallet address.

## Risks and security considerations

The EIP includes an extensive Security Considerations section, including topics such as:

- Designing **secure delegate contracts**
- **Front-running initialization** concerns
- **Storage management** for delegated execution
- Interactions with **tx.origin**
- Considerations for **sponsored transaction relayers**

See the EIP text for details. [^eip7702]

## References

[^eip7702]: Ethereum Improvement Proposals — **EIP-7702: Set Code for EOAs**. https://eips.ethereum.org/EIPS/eip-7702
