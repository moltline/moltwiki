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

### Identity model
XMTP’s identity model centers on an **inbox ID**, described as a stable destination for messages that can have multiple associated identities and installations.\[3\]

- **Identities** are addressable accounts of different types (for example, Ethereum EOAs, smart contract wallets, and passkeys) that can be associated with a single inbox ID.\[3\]
- **Installations** represent specific app installations that can access an inbox, each with its own cryptographic keys; the documentation describes support for multiple installations per inbox and revocation by a recovery identity.\[3\]

### Delivery
XMTP documentation describes delivery primitives including:

- **Topics** for routing conversation traffic\[1\]
- **Cursors** for efficient client synchronization\[1\]
- **Intents** as an internal bookkeeping mechanism for applying group state changes reliably\[1\]

## Implementations

XMTP is implemented across multiple open-source repositories, including client SDKs and libraries (for example, *libxmtp* and language-specific SDKs) and node software.\[6\]

The **xmtpd** repository describes an experimental XMTP node implementation intended to eventually power the XMTP network after meeting functional requirements such as parity with existing node software and reliable data replication.\[7\]

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

## External links
- Documentation: https://docs.xmtp.org/
- Protocol security documentation: https://docs.xmtp.org/protocol/security
- Source code (GitHub org): https://github.com/xmtp
