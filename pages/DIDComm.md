---
title: DIDComm
---

# DIDComm

**DIDComm** (short for **Decentralized Identifier Communication**) is a set of specifications for **secure, private, peer-to-peer messaging** between parties identified by **Decentralized Identifiers (DIDs)**. DIDComm is designed to be **transport-agnostic** (e.g., it can be carried over HTTPS or other transports) while providing confidentiality and integrity at the message layer, and it is commonly discussed in the context of decentralized identity systems.

## Overview

DIDComm is intended to enable application-level protocols and workflows built from structured messages exchanged between parties that control DIDs. A DIDComm interaction typically relies on DID Documents (and associated keys and service endpoints) to establish how parties can communicate and how messages are protected.

## DIDComm v2 (DIDComm Messaging)

The **DIDComm Messaging specification** (often referred to as **DIDComm v2**) is developed within the **Decentralized Identity Foundation (DIF)**. DIF has announced DIDComm v2 reaching **DIF Approved Status**, positioning it as a stable basis for implementations and further ecosystem adoption.

## Relationship to W3C DID Core

DIDComm is commonly described as complementary to the **W3C Decentralized Identifiers (DID) Core** specification: DID Core defines the identifier format and DID Documents, while DIDComm defines how DID controllers can exchange protected messages using keys and endpoints associated with those identifiers.

## See also

- [Decentralized Identifiers (DIDs)](https://www.w3.org/TR/did-core/)
- [Decentralized Identity Foundation (DIF)](https://identity.foundation/)

## References

- Decentralized Identity Foundation (DIF). “DIDComm v2 reaches approved spec status!” (blog post). https://blog.identity.foundation/didcomm-v2/
- Decentralized Identity Foundation (DIF). “DIDComm Messaging Specification v2” (specification). https://identity.foundation/didcomm-messaging/spec/
- W3C. “Decentralized Identifiers (DIDs) v1.0.” https://www.w3.org/TR/did-core/
