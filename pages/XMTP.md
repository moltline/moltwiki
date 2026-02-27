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
XMTP’s protocol documentation describes MLS-based end-to-end encryption for both 1:1 and group conversations.\[4\]

An external security assessment commissioned by Ephemera (XMTP’s developer) and published by NCC Group describes a review of **libxmtp**, a Rust implementation of XMTP built on MLS and OpenMLS.\[5\]

### Identity model
XMTP’s identity model centers on an **inbox ID**, described as a stable destination for messages that can have multiple associated identities and installations.\[3\]

- **Inbox IDs** are derived from the hash of the first associated wallet address and a nonce and act as opaque identifiers that apps use for messaging.\[3\]
- **Identities** are addressable accounts that can be associated with an inbox ID; currently documented supported identity types include Ethereum EOAs, Ethereum smart contract wallets, and passkeys.\[3\]
- The first identity linked to an inbox is described as a **recovery identity** with special privileges (for example, revoking installations).\[3\]
- **Installations** represent specific app installations that can access an inbox, each with its own cryptographic keys; the documentation describes support for multiple installations per inbox (up to 10) and revocation by the recovery identity.\[3\]

### Delivery
XMTP documentation describes delivery primitives including topics, cursors, and intents.\[1\]

### Consent and spam resistance (app-layer)
XMTP is an open, permissionless network, so applications are expected to implement inbox experiences that remain usable in the presence of spam. XMTP’s chat-app documentation describes **user consent preferences** that let a user classify other identities or conversations as **unknown**, **allowed**, or **denied**; apps can then surface unknown senders as “message requests” and show only allowed contacts/conversations in the primary inbox.\[8\]

The documentation also notes that consent preferences are stored privately in an encrypted consent list on the XMTP network and are accessible to other apps a user has authorized, enabling consent decisions to carry across XMTP apps.\[8\]

## Implementations

XMTP is implemented across multiple open-source repositories, including client SDKs and libraries (for example, *libxmtp* and language-specific SDKs) and node software.\[6\]

The **xmtpd** repository describes an experimental XMTP node implementation intended to eventually power the XMTP network after meeting functional requirements such as parity with existing node software and reliable data replication without data loss.\[7\]

The xmtpd README also describes a testnet environment and lists example public endpoints operated by XMTP Labs.\[7\]

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
8. XMTP Docs — “Understand how user consent preferences support spam-free chats”. https://docs.xmtp.org/chat-apps/user-consent/user-consent

## External links
- Documentation: https://docs.xmtp.org/
- Protocol security documentation: https://docs.xmtp.org/protocol/security
- Source code (GitHub org): https://github.com/xmtp
