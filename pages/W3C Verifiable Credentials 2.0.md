---
title: "W3C Verifiable Credentials 2.0"
description: "A family of W3C specifications defining a data model for cryptographically verifiable digital credentials and presentations (issuer–holder–verifier ecosystem), commonly used with DIDs and digital wallets."
---

# W3C Verifiable Credentials 2.0

**W3C Verifiable Credentials (VCs) 2.0** are a family of W3C specifications that define an extensible **data model** and related concepts for issuing, holding, presenting, and verifying **cryptographically verifiable digital credentials** on the Web. [^vc-dm]

The family is organized around the **Verifiable Credentials Data Model 2.0** as the core specification, with additional documents describing how to secure credentials and how to publish credential status information. The W3C *Verifiable Credentials Overview* presents the VC specifications as a roadmap and distinguishes two broad approaches to securing credentials: **embedded proofs** and **enveloping proofs**. [^vc-overview]

In agent-oriented systems, VCs are often discussed as building blocks for identity assertions, authorization/mandates, and wallet-based presentation of claims. (Whether a verifier should rely on a particular claim remains a policy decision outside the data model; the data model focuses on making credentials tamper-evident and verifiable.) [^vc-dm]

## Core concepts

### Roles
The VC ecosystem is commonly described with several roles, including:
- **Issuer**: creates a Verifiable Credential by asserting claims about a subject.
- **Holder**: possesses one or more credentials and can generate **Verifiable Presentations**.
- **Verifier**: receives credentials (optionally inside a presentation) and performs verification. [^vc-dm]

### Verifiable Credential vs. Verifiable Presentation
- A **Verifiable Credential** is a set of claims plus metadata, secured so that a verifier can check authenticity and integrity. [^vc-dm]
- A **Verifiable Presentation** is produced by the holder to present some or all claims, potentially combining multiple credentials, and is often treated as short-lived. [^vc-overview]

### Securing credentials (embedded vs. enveloping proofs)
The VC 2.0 ecosystem supports two broad patterns for attaching cryptographic protection:

- **Enveloping proofs**: the proof *wraps* the credential or presentation. The W3C specification *Securing Verifiable Credentials using JOSE and COSE* defines how to secure VC data model documents using IETF technologies such as **JWS**, **SD-JWT**, and **COSE**. [^vc-jose-cose]

- **Embedded proofs**: the proof is included *within* the credential or presentation serialization. The W3C Overview points to the *Verifiable Credential Data Integrity* specification as the general framework for embedded proofs, with separate “cryptosuite” specifications defining concrete algorithms and serialization details. [^vc-overview] [^vc-di]

### Credential status (revocation/suspension)
Issuers often need to publish whether a credential has been **revoked** or **suspended**. The VC family includes a status-list approach: the *Bitstring Status List* specification describes a privacy-preserving, space-efficient mechanism for publishing status information using bitstrings, and discusses privacy concerns with one-to-one “per-credential URL” status checks. [^vc-bitstring-status-list]

## Notes for implementers

- **Verifiability is not truth**: the data model notes that successful cryptographic verification does not by itself imply that the claims are true; verifiers apply their own policies and business rules when deciding whether to rely on claims. [^vc-dm]

- **Media types**: the data model defines media types for conforming documents (for example `application/vc` for verifiable credentials and `application/vp` for verifiable presentations). [^vc-dm]

- **Status-list privacy**: the Bitstring Status List design aims to improve privacy by grouping many credentials into a single list, reducing correlation risks and enabling efficient caching and compression. [^vc-bitstring-status-list]

## References

[^vc-dm]: W3C Verifiable Credentials Working Group. *Verifiable Credentials Data Model v2.0*. https://www.w3.org/TR/vc-data-model-2.0/
[^vc-overview]: W3C Verifiable Credentials Working Group. *Verifiable Credentials Overview*. https://www.w3.org/TR/vc-overview/
[^vc-jose-cose]: W3C Verifiable Credentials Working Group. *Securing Verifiable Credentials using JOSE and COSE*. https://www.w3.org/TR/vc-jose-cose/
[^vc-di]: W3C Verifiable Credentials Working Group. *Verifiable Credential Data Integrity 1.0*. https://www.w3.org/TR/vc-data-integrity/
[^vc-bitstring-status-list]: W3C Verifiable Credentials Working Group. *Bitstring Status List v1.1*. https://www.w3.org/TR/vc-bitstring-status-list/
