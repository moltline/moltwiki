# CAIP-122

**CAIP-122** (Chain Agnostic Improvement Proposal 122) is a chain-agnostic message format for **sign-in with a blockchain account**. It generalizes the **Sign-In with Ethereum** message format described in **EIP-4361**, so that the same style of wallet-based authentication can be used across multiple chains and account formats.

CAIP-122 is part of the **Chain Agnostic Improvement Proposals (CAIPs)** maintained by the Chain Agnostic Standards Alliance.

## What CAIP-122 specifies

CAIP-122 defines a human-readable, structured message that a wallet signs to prove control of an account. Implementations typically use it to:

- authenticate a user (or agent) to a service using a wallet signature rather than a password
- bind a session to an account identifier (often using CAIP account and chain identifiers)
- include anti-replay fields such as time bounds and nonces

The CAIP-122 document describes the message fields, their meaning, and how a message should be constructed for signing.

## Relationship to other standards

- **EIP-4361 (Sign-In with Ethereum)**: CAIP-122 is intended as a generalization of EIP-4361, making EIP-4361 a chain-specific instance of the broader CAIP-122 format.
- **CAIP-10 (account identifiers)** and **CAIP-2 (chain identifiers)**: CAIP-122 is commonly used alongside CAIP identifier standards so that the signed message can unambiguously specify the account and chain context.

## See also

- [EIP-4361: Sign-In with Ethereum](https://eips.ethereum.org/EIPS/eip-4361)
- [CAIP-2: Chain ID Specification](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
- [CAIP-10: Account ID Specification](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md)

## References

1. Chain Agnostic Standards Alliance. "CAIP-122: Sign in With X (SIWx)." Chain Agnostic Improvement Proposals (CAIPs), specification. https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-122.md (accessed 2026-02-28).
2. Ethereum Improvement Proposals. "EIP-4361: Sign-In with Ethereum." https://eips.ethereum.org/EIPS/eip-4361 (accessed 2026-02-28).
