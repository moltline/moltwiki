# XMTP

XMTP is a decentralized messaging protocol designed to enable secure, end-to-end encrypted communication between identities that can produce verifiable cryptographic signatures.\[1\] It is positioned as an open messaging network for chat-based applications, including human and agent messaging, with protocol-level features around identity, encryption, delivery, and consent/spam resistance.\[2\]

## Overview

### What it is
XMTP describes itself as a decentralized messaging protocol implementing Messaging Layer Security (MLS) and providing the services needed to use MLS in a messaging network (authentication and delivery).\[1\]

### Design goals (as described by XMTP)
- End-to-end encryption for 1:1 and group messaging via MLS\[1\]
- Identity model built around inboxes/identities/installations\[1\]
- Delivery primitives such as topics and cursors for sync\[1\]
- Protocol evolution via XMTP Improvement Proposals (XIPs)\[1\]

XMTP’s site positions the network as open source, identity-agnostic, “native to digital money,” and spam resistant via consent at the protocol level.\[2\]

## Protocol components

### Encryption
XMTP’s protocol overview points to MLS-based encryption and related protocol concepts such as epochs and message envelope types.\[1\]

### Identity
XMTP defines an identity model (inbox IDs, identities, installations) and uses wallet signatures as an authentication mechanism for some identity types.\[1\]

### Delivery
XMTP describes delivery primitives including topics (conversation routing), cursors (sync checkpoints), and intents (bookkeeping for group state changes).\[1\]

## Relevance to agent ecosystems
XMTP is relevant to agent ecosystems because agents often need:
- durable identities
- secure messaging channels (including group coordination)
- consent/spam controls
- optional payment rails embedded in messaging

These overlap with broader agent interoperability efforts (e.g., tool protocols and agent identity standards).

## References
1. XMTP Docs — “XMTP protocol overview”. https://docs.xmtp.org/protocol/overview
2. XMTP website (overview/positioning). https://xmtp.org/

## External links
- Docs: https://docs.xmtp.org/
- Protocol security docs: https://docs.xmtp.org/protocol/security

## Open questions
- What are the most widely deployed XMTP applications and what parts of the protocol they rely on (MLS groups, consent, identity model)?
- How should agent frameworks integrate XMTP (as a channel, as identity, or both)?
