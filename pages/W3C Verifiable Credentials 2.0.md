---
title: "W3C Verifiable Credentials 2.0"
description: "A family of W3C Recommendations defining an extensible data model for cryptographically verifiable digital credentials and presentations (issuer–holder–verifier ecosystem)."
---

# W3C Verifiable Credentials 2.0

**W3C Verifiable Credentials (VCs) 2.0** are a family of W3C Recommendations for expressing **cryptographically verifiable credentials and presentations** on the Web, centered on the **Verifiable Credentials Data Model**.[^vc-overview][^vcdm]

The Verifiable Credentials Overview describes the goal as expressing digital credentials in a way that is **cryptographically secure, privacy-respecting, and machine-verifiable**.[^vc-overview]

## Standardization status

In 2025, W3C published **Verifiable Credentials 2.0** as a W3C Standard (Recommendation), including the Verifiable Credentials Data Model v2.0 and related specifications in the same family.[^w3c-press-vc20]

## Core concepts

### Roles (issuer / holder / verifier)
The VC ecosystem is commonly described with three primary roles:
- **Issuer**: creates a Verifiable Credential by asserting claims about a subject.[^vcdm]
- **Holder**: possesses one or more credentials and can generate **Verifiable Presentations**.[^vcdm]
- **Verifier**: receives credentials (optionally inside a presentation) and performs verification before relying on claims.[^vcdm]

### Claims, subjects, and the credential “graph”

A VC is built from **claims** (statements) about a **subject**, expressed as properties and values; taken together, these can form a **graph of claims**.[^vc-overview]

### Verifiable Credential vs. Verifiable Presentation
- A **Verifiable Credential** is a credential (claims + metadata) that includes verification mechanisms so a verifier can check who issued it and whether it was altered.[^vc-overview][^vcdm]
- A **Verifiable Presentation** is produced by the holder to present some or all claims, potentially combining multiple credentials; the overview describes presentations as a way to express only the portions of one’s persona appropriate for a situation.[^vc-overview]

## How VCs are secured (embedded vs. enveloping proofs)
The VC overview distinguishes two broad patterns:

### Embedded proofs (Data Integrity)

An **embedded proof** includes proof material alongside the credential in its serialization. The overview points to **Verifiable Credential Data Integrity** as the general framework for embedded proofs.[^vc-overview][^vc-di]

### Enveloping proofs (JOSE/COSE)

An **enveloping proof** wraps around the credential or presentation. The "Securing Verifiable Credentials using JOSE and COSE" specification defines how to secure credentials and presentations conforming to the Verifiable Credentials Data Model using JOSE and COSE.[^vc-jose-cose]

Background standards referenced by the JOSE/COSE securing approach include:
- JSON Web Signature (JWS): https://www.rfc-editor.org/rfc/rfc7515
- CBOR Object Signing and Encryption (COSE): https://www.rfc-editor.org/rfc/rfc9052

## Credential status (revocation/suspension)

Issuers often need to publish whether a credential has been **revoked** or **suspended**. The **Bitstring Status List v1.0** specification describes a **privacy-preserving, space-efficient, and high-performance** mechanism for publishing status information (such as suspension or revocation) using bitstrings, and discusses privacy issues with one-to-one per-credential status URLs.[^vc-bsl]

Bitstring Status List v1.0 was published as a W3C Recommendation in May 2025.[^vc-bsl-history]

## Notes for implementers

- **Verifiability is not truth**: cryptographic verification establishes properties like integrity and authenticity, but verifiers still apply their own policies when deciding whether to rely on claims.[^vcdm]

## References

[^vc-overview]: W3C. "Verifiable Credentials Overview" (W3C Recommendation). https://www.w3.org/TR/vc-overview/

[^vcdm]: W3C. "Verifiable Credentials Data Model v2.0" (W3C Recommendation). https://www.w3.org/TR/vc-data-model-2.0/

[^vc-di]: W3C. "Verifiable Credential Data Integrity 1.0" (W3C Recommendation). https://www.w3.org/TR/vc-data-integrity/

[^vc-jose-cose]: W3C. "Securing Verifiable Credentials using JOSE and COSE" (W3C Technical Report). https://www.w3.org/TR/vc-jose-cose/

[^vc-bsl]: W3C. "Bitstring Status List v1.0" (W3C Recommendation). https://www.w3.org/TR/vc-bitstring-status-list/

[^vc-bsl-history]: W3C. "Bitstring Status List v1.0 publication history" (Standards history). https://www.w3.org/standards/history/vc-bitstring-status-list/

[^w3c-press-vc20]: W3C. "W3C publishes Verifiable Credentials 2.0 as a W3C Standard" (Press release, 2025). https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/
