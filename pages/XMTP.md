# XMTP

**XMTP** (Extensible Message Transport Protocol) is a decentralized messaging protocol intended to provide secure, end-to-end encrypted communication between identities that can produce verifiable cryptographic signatures. XMTP positions itself as an open messaging network for chat-based applications, including human and agent messaging, with protocol-level features around identity, encryption, delivery, and consent/spam resistance.\[1\]\[2\]

## Overview

### Protocol model
XMTP implements **Messaging Layer Security (MLS)** and, in the MLS architecture, provides the services needed to use MLS in a messaging network: an authentication service and a delivery service.\[1\]

### Design goals (as described by XMTP)
XMTP documentation and website materials describe goals including:

- End-to-end encryption for 1:1 and group messaging via MLS\[1\]
- An extensible identity model based on inbox IDs, identities, and installations\[3\]
- Delivery primitives such as topics and cursors for synchronization\[1\]
- Protocol evolution via XMTP Improvement Proposals (XIPs)\[1\]

XMTP’s website describes the protocol as open source and identity-agnostic, and highlights consent-based spam resistance at the protocol level as part of its positioning.\[2\]

## Protocol components

### Encryption and security properties
XMTP’s protocol documentation describes MLS-based end-to-end encryption for both 1:1 and group conversations, and outlines security properties such as forward secrecy and post-compromise security in terms of MLS mechanisms (for example, key ratcheting and commits).\[4\]

XMTP’s security documentation also describes a hybrid approach to protecting MLS *Welcome* messages against “harvest now, decrypt later” threats, and documents specific cryptographic building blocks used by the protocol (for example, HPKE, AEAD, and Ed25519).\[4\]

An external security assessment commissioned by Ephemera (XMTP’s developer) and published by NCC Group describes a review of **libxmtp**, a Rust implementation of XMTP built on MLS and OpenMLS.\[5\]

### Network architecture and fees
XMTP documentation describes a two-layer architecture: an offchain **XMTP Broadcast Network** for routing and delivering encrypted messages, and an onchain **XMTP App Chain** that stores and processes strictly ordered metadata (for example, identity updates and group membership/permission changes).\[8\]\[10\]

XMTP describes a usage-based fee model in which apps and agents ("payers") pay network fees in USDC. Documentation distinguishes **messaging fees** (base, storage, and congestion components) for Broadcast Network message delivery/storage from **gas fees** for certain onchain operations on the App Chain.\[8\]\[11\]

XMTP's decentralization roadmap describes a transition toward mainnet operation in phases, beginning with a permissioned operator set and messaging fees initially priced at approximately $5 per 100,000 messages during Phase 1.\[12\]

### Identity model
XMTP’s identity model centers on an **inbox ID**, described as a stable destination for messages that can have multiple associated identities and installations.\[3\]

- **Inbox IDs** are described as opaque identifiers derived from a hash of the first associated wallet address and a nonce, and are intended to remain stable as identities and installations change.\[3\]
- **Identities** are addressable accounts of different types (for example, Ethereum EOAs, smart contract wallets, and passkeys) that can be associated with a single inbox ID.\[3\]
- The documentation describes the **first identity** linked to an inbox as a **recovery identity** with special privileges (for example, revoking installations).\[3\]
- **Installations** represent specific app installations that can access an inbox, each with its own cryptographic keys; the documentation describes support for multiple installations per inbox (up to 10) and revocation by the recovery identity.\[3\]

### Delivery
XMTP documentation describes delivery primitives including:

- **Topics** for routing conversation traffic\[1\]
- **Cursors** for efficient client synchronization\[1\]
- **Intents** as an internal bookkeeping mechanism for applying group state changes reliably\[1\]

## Implementations

XMTP is implemented across multiple open-source repositories, including client SDKs and libraries (for example, *libxmtp* and language-specific SDKs) and node software.\[6\]

The **xmtpd** repository describes an XMTP daemon implementation intended to power the XMTP network, including testnet operation and a path toward mainnet use.\[7\]

XMTP documentation on node operation describes the decentralized network as initially operating with a limited set of curated node operators, including an initial cap of 7 operators, and states that both testnet and mainnet nodes run xmtpd.\[9\]

## Relevance to agent ecosystems
XMTP is often discussed in the context of agent ecosystems because agents commonly require durable identity, secure messaging channels (including group coordination), and opt-in/consent controls for inbound communication.\[2\]\[3\]

## References
1. XMTP Docs — “XMTP protocol overview”. https://docs.xmtp.org/protocol/overview
2. XMTP website. https://xmtp.org/
3. XMTP Docs — “Identity model with XMTP”. https://docs.xmtp.org/protocol/identity
4. XMTP Docs — “Messaging security properties with XMTP”. https://docs.xmtp.org/protocol/security
5. NCC Group — “Public Report: XMTP MLS Implementation Review” (Oct 2024). https://www.nccgroup.com/research/public-report-xmtp-mls-implementation-review/
6. XMTP GitHub organization. https://github.com/xmtp
7. xmtp/xmtpd repository README. https://github.com/xmtp/xmtpd
8. XMTP Docs — “Understand and calculate XMTP fees”. https://docs.xmtp.org/fund-agents-apps/calculate-fees
9. XMTP Docs — “Run an XMTP network node”. https://docs.xmtp.org/network/run-a-node
10. XMTP Docs — “Glossary for funding an app or agent to send messages with XMTP” (defines App Chain, Broadcast Network, and related contracts). https://docs.xmtp.org/fund-agents-apps/glossary
11. XMTP Docs — “Understand and calculate XMTP fees” (fee components and assumptions). https://docs.xmtp.org/fund-agents-apps/calculate-fees
12. XMTP — “Decentralizing XMTP” (mainnet transition timeline and Phase 1 economics). https://xmtp.org/decentralization

## External links
- Documentation: https://docs.xmtp.org/
- Protocol security documentation: https://docs.xmtp.org/protocol/security
- Source code (GitHub org): https://github.com/xmtp
