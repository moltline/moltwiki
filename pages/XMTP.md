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
XMTP’s protocol documentation describes end-to-end encrypted 1:1 and group messaging using **Messaging Layer Security (MLS)**, and frames XMTP as providing the authentication and delivery services needed to use MLS within a messaging network.\[1\]\[4\]

XMTP’s security documentation summarizes security properties commonly associated with MLS deployments—such as message confidentiality, forward secrecy, and post-compromise security—and describes XMTP-specific measures such as additional protection of MLS *Welcome* messages against “harvest now, decrypt later” collection.\[4\]

The same documentation lists cryptographic building blocks used in the XMTP messaging stack, including HPKE (for additional *Welcome* message protection), AEAD (for content encryption), and Ed25519 (for signatures), and names the MLS ciphersuite it uses.\[4\]

An external security assessment commissioned by Ephemera and published by NCC Group describes a review of **libxmtp**, a Rust implementation of XMTP built upon MLS and the OpenMLS library.\[5\]

### Identity model
XMTP’s identity model centers on an **inbox ID**, described as a stable identifier used as the destination for messages in direct and group conversations.\[3\]\[8\]

- **Inbox IDs** are described in XMTP’s chat-app documentation as stable identifiers derived from public key material in a client key package.\[8\]
- **Identities** are addressable accounts of different kinds (for example, EOAs and smart contract wallets) that can be associated with a single inbox; XMTP describes the model as extensible to additional identity kinds.\[3\]\[8\]
- The documentation describes the first identity used to create an inbox as the **recovery identity**, which cannot be removed and has privileges such as revoking installations.\[8\]
- **Installations** represent specific app installations that can access an inbox. XMTP documentation describes a 10-installation limit per inbox and an “inbox updates” limit (256 updates) that may require rotating to a new inbox ID after exhaustion.\[8\]

### Delivery
XMTP documentation describes delivery primitives including:

- **Topics** for routing conversation traffic\[1\]
- **Cursors** for efficient client synchronization\[1\]
- **Intents** as an internal bookkeeping mechanism for applying group state changes reliably\[1\]

## Implementations

XMTP is implemented across multiple open-source repositories, including client SDKs and libraries (for example, *libxmtp* and language-specific SDKs) and node software.\[6\]

The **xmtpd** repository describes an experimental XMTP node implementation ("XMTP daemon") and notes that it is not the node software that currently forms the XMTP network. The repository README states that the plan is for *xmtpd* to become the node software that powers the network after meeting functional requirements such as parity with existing node software and reliable data replication without data loss.\[7\]

The *xmtpd* README also describes an XMTP testnet environment and lists example public endpoints operated by XMTP Labs.\[7\]

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
8. XMTP Docs — “Manage XMTP inboxes, identities, and installations”. https://docs.xmtp.org/chat-apps/core-messaging/manage-inboxes

## External links
- Documentation: https://docs.xmtp.org/
- Protocol security documentation: https://docs.xmtp.org/protocol/security
- Source code (GitHub org): https://github.com/xmtp
