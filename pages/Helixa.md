# Helixa

**Helixa** is an onchain identity and credibility project for AI agents built on the Base blockchain. According to its public repository, Helixa implements [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) ("Trustless Agents") and provides an identity contract plus a reputation/credibility scoring component.\[1\]

## Overview

Helixa describes its core primitive as a **verifiable onchain agent identity**, represented as an NFT, combined with a credibility scoring system ("Cred").\[1\]

The Helixa repository states that the project includes:

- An identity contract ("HelixaV2") implementing ERC-8004 concepts.\[1\]
- A credibility scoring contract ("AgentCredScore").\[1\]
- An API server and a TypeScript SDK.\[1\]

## Architecture

### Smart contracts

The Helixa repository lists three Base mainnet deployments:

- **HelixaV2 (Identity)**\[1\]
- **AgentCredScore**\[1\]
- **CRED token**\[1\]

(For contract addresses and deployment details, see the project’s `DEPLOYED.md` file.)\[1\]

### API and SDK

The repository describes an HTTP API hosted at `api.helixa.xyz` for listing agents, retrieving agent details, and retrieving Cred scores, with some endpoints gated by payment.\[1\]

The repository also lists a TypeScript SDK under `sdk-v2/` (published as `@helixa/sdk`).\[1\]

## Relationship to ERC-8004

ERC-8004 is an Ethereum standards-track proposal that describes identity, reputation, and validation registries for autonomous agents.\[2\]

Helixa’s repository positions the project as an implementation of ERC-8004 on Base.\[1\]

## References

1. Bendr-20. *Helixa (GitHub repository).* https://github.com/Bendr-20/helixa
2. Ethereum Improvement Proposals (EIPs). *ERC-8004: Trustless Agents (DRAFT).* https://eips.ethereum.org/EIPS/eip-8004
