---
title: "W3C Verifiable Credentials 2.0"
description: "A W3C standard for cryptographically verifiable digital credentials and presentations (issuer–holder–verifier model), commonly used with DIDs and digital wallets."
---

# W3C Verifiable Credentials 2.0

**W3C Verifiable Credentials (VCs) 2.0** are a family of W3C specifications that define a **data model** and related concepts for issuing, holding, presenting, and verifying **cryptographically verifiable digital credentials** on the Web.

This family is organized around the **Verifiable Credentials Data Model v2.0** as the core dependency, with additional specifications describing how to secure credentials and how to publish credential status information. The W3C *Verifiable Credentials Overview* describes the VC 2.0 specifications as a roadmap and distinguishes two broad approaches to securing credentials: **embedded proofs** and **enveloping proofs**. [^vc-overview]

In agent-oriented systems, VCs are often discussed as building blocks for:
- identity assertions (e.g., “this agent is operated by X”),
- authorization/mandates (what an agent is allowed to do),
- portable reputation/compliance signals,
- wallet-based credential storage and selective disclosure via presentations.

## Core concepts

### Roles
The VC ecosystem is commonly described with three primary roles:
- **Issuer**: creates a Verifiable Credential about a subject.
- **Holder**: possesses credentials and produces **Verifiable Presentations**.
- **Verifier**: checks proofs and status to decide whether to accept presented claims.

### Verifiable Credential vs. Verifiable Presentation
- A **Verifiable Credential** is a set of claims plus metadata, secured by a proof so verifiers can check authenticity and integrity.
- A **Verifiable Presentation** is created by the holder to present some or all claims, potentially combining multiple credentials.

### Securing credentials (embedded vs. enveloping proofs)
The VC 2.0 ecosystem supports two broad ways to attach cryptographic protection to credentials and presentations:

- **Enveloping proofs**: the proof *wraps* the credential/presentation. The W3C specification *Securing Verifiable Credentials using JOSE and COSE* defines how to secure VC data model documents using IETF technologies including **JWS**, **SD-JWT**, and **COSE**. [^vc-jose-cose]
- **Embedded proofs**: the proof is included *within* the credential/presentation serialization. The W3C Overview points to **Verifiable Credential Data Integrity** as the general structure for embedded proofs, and to separate “cryptosuite” specifications (for example EdDSA/ECDSA/BBS) as concrete instantiations. [^vc-overview]

One example cryptosuite specification (EdDSA) describes how a processor canonicalizes input (using RDF Dataset Canonicalization or JCS), hashes it, and produces a detached signature, in conformance with the Data Integrity framework. [^vc-di-eddsa]

### Credential status (revocation/suspension)
Issuers often need to publish whether a credential is **revoked** or **suspended**. The VC 2.0 family includes a status-list approach: the *Bitstring Status List* specification describes a privacy-preserving, space-efficient mechanism for publishing credential status information using bitstrings, and discusses privacy concerns with one-to-one “per-credential URL” status checks. [^vc-bitstring-status-list] [^vc-overview]

## Why it matters for agents
Agentic systems frequently need portable, machine-verifiable answers to questions like:
- Who is this agent (or the organization behind it)?
- What capabilities is it authorized to exercise (and under what limits)?
- Can a verifier validate those claims and check credential status?

VCs provide a standards-based vocabulary and proof model for these flows, and are often paired with **Decentralized Identifiers (DIDs)** and **digital wallets**.

## References

[^vc-overview]: W3C (VCWG). *Verifiable Credentials Overview*. https://w3c.github.io/vc-overview/
[^vc-jose-cose]: W3C. *Securing Verifiable Credentials using JOSE and COSE*. https://www.w3.org/TR/vc-jose-cose/
[^vc-di-eddsa]: W3C. *Data Integrity EdDSA Cryptosuites v1.1*. https://w3c.github.io/vc-di-eddsa/
[^vc-bitstring-status-list]: W3C. *Bitstring Status List v1.1*. https://www.w3.org/TR/vc-bitstring-status-list/
