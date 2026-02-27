---
title: "Decentralized Identifiers (DIDs) v1.0 (W3C)"
description: "A W3C Recommendation defining a URI-based identifier scheme and DID documents for decentralized, cryptographically verifiable identifiers."
---

# Decentralized Identifiers (DIDs) v1.0 (W3C)

**Decentralized Identifiers (DIDs) v1.0** is a **W3C Recommendation** that defines a new kind of identifier—**a DID**—designed to enable **verifiable, decentralized digital identity**. The specification defines the **DID syntax**, a common **data model** for **DID documents**, and core properties and operations used with DIDs. [W3C TR: Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)

A DID is expressed as a URI with the scheme `did:` and a **DID method** component (e.g., `did:example:...`). DID methods define how DIDs are created, resolved, updated, and deactivated for a particular system (often using a ledger, database, or other verifiable data registry). [W3C TR: Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)

## Core concepts

### DID, DID URL, and DID method
- **DID**: the base identifier (a `did:` URI) that identifies a subject.
- **DID URL**: a DID plus additional components (path, query, fragment) used to locate or refer to specific resources or verification material associated with the DID.
- **DID method**: the method-specific rules and procedures for DID operations and resolution.

These are defined in the core specification. [W3C TR: Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)

### DID document
A **DID document** is a data structure associated with a DID that expresses information needed to interact with the DID subject, such as **verification methods** and **service endpoints**. DID documents are the primary objects returned (or discovered) via **DID resolution**. [W3C TR: Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)

Common DID document properties include:
- **Verification methods**: cryptographic material (e.g., public keys) and metadata used for authentication and other proofs.
- **Verification relationships**: how verification methods are intended to be used (e.g., authentication).
- **Services**: service endpoints that enable interaction with the DID subject (e.g., messaging, credential exchange), expressed as service entries.

(Exact property names and processing rules are specified normatively in DID Core.) [W3C TR: Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)

## DID resolution and dereferencing
The DID Core specification defines the concept of **DID resolution** (obtaining a DID document and related metadata for a DID) and **DID URL dereferencing** (retrieving a resource identified by a DID URL). Work on common resolution and dereferencing algorithms has been developed in the W3C Credentials Community Group and referenced by later W3C charter drafts for DID work. [W3C Charter Draft: Decentralized Identifier Working Group](https://w3c.github.io/charter-drafts/2023/did-wg.html)

## Relationship to Verifiable Credentials
DIDs are commonly used as identifiers for issuers, holders, and verifiers in ecosystems built around **W3C Verifiable Credentials**, though the VC specifications do not require DIDs specifically. See: [W3C Verifiable Credentials 2.0](./W3C%20Verifiable%20Credentials%202.0.md).

## Publication and status
The DID Core v1.0 specification was published as a W3C Recommendation on **2022-07-19** (as referenced in W3C charter materials for DID maintenance work). [W3C Charter Draft: Decentralized Identifier Working Group](https://w3c.github.io/charter-drafts/2023/did-wg.html)

## References
- [W3C TR: Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)
- [W3C Charter Draft: Decentralized Identifier Working Group](https://w3c.github.io/charter-drafts/2023/did-wg.html)
