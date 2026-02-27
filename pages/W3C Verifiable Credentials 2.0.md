---
title: "W3C Verifiable Credentials 2.0"
description: "A family of W3C Recommendations defining an extensible data model for cryptographically verifiable digital credentials and presentations (issuer–holder–verifier ecosystem)."
---

# W3C Verifiable Credentials 2.0

**W3C Verifiable Credentials (VCs) 2.0** are a family of W3C Recommendations for expressing **cryptographically verifiable credentials and presentations** on the Web, centered on the **Verifiable Credentials Data Model v2.0**. https://www.w3.org/TR/vc-overview/ https://www.w3.org/TR/vc-data-model-2.0/

The VC overview frames the goal as expressing credentials in a way that is **cryptographically secure, privacy respecting, and machine-verifiable**. https://www.w3.org/TR/vc-overview/

## Core concepts

### Roles (issuer / holder / verifier)
The VC ecosystem is commonly described with three primary roles:
- **Issuer**: creates a Verifiable Credential by asserting claims about a subject. https://www.w3.org/TR/vc-data-model-2.0/
- **Holder**: possesses one or more credentials and can generate **Verifiable Presentations**. https://www.w3.org/TR/vc-data-model-2.0/
- **Verifier**: receives credentials (optionally inside a presentation) and performs verification before relying on claims. https://www.w3.org/TR/vc-data-model-2.0/

### Claims, subjects, and the credential “graph”
A VC is built from **claims** (statements) about a **subject**, expressed as properties and values; taken together, these can form a **graph of claims**. https://www.w3.org/TR/vc-overview/

### Verifiable Credential vs. Verifiable Presentation
- A **Verifiable Credential** is a credential (claims + metadata) that includes verification mechanisms so a verifier can check who issued it and whether it was altered. https://www.w3.org/TR/vc-overview/ https://www.w3.org/TR/vc-data-model-2.0/
- A **Verifiable Presentation** is produced by the holder to present some or all claims, potentially combining multiple credentials; the overview describes presentations as a way to express only the portions of one’s persona appropriate for a situation. https://www.w3.org/TR/vc-overview/

## How VCs are secured (embedded vs. enveloping proofs)
The VC overview distinguishes two broad patterns:

### Embedded proofs (Data Integrity)
An **embedded proof** includes proof material alongside the credential in its serialization. The overview points to **Verifiable Credential Data Integrity** as the general framework for embedded proofs, with separate “cryptosuite” specifications defining concrete algorithms and serialization details. https://www.w3.org/TR/vc-overview/ https://www.w3.org/TR/vc-data-integrity/

### Enveloping proofs (JOSE/COSE)
An **enveloping proof** wraps around the credential or presentation. The overview states that a family of enveloping proofs is defined in **Securing Verifiable Credentials using JOSE and COSE** and relies on IETF technologies. https://www.w3.org/TR/vc-overview/ https://www.w3.org/TR/vc-jose-cose/

## Credential status (revocation/suspension)
Issuers often need to publish whether a credential has been **revoked** or **suspended**. The overview describes the **Bitstring Status List** specification as a **privacy-preserving, space-efficient, high-performance** mechanism for publishing credential status using bitstrings. https://www.w3.org/TR/vc-overview/ https://www.w3.org/TR/vc-bitstring-status-list/

## Notes for implementers
- **Verifiability is not truth**: the data model notes that successful cryptographic verification does not by itself imply that the claims are true; verifiers apply their own policies when deciding whether to rely on claims. https://www.w3.org/TR/vc-data-model-2.0/
- **Media types**: the data model defines media types for conforming documents (for example `application/vc` for verifiable credentials and `application/vp` for verifiable presentations). https://www.w3.org/TR/vc-data-model-2.0/

## References
- Verifiable Credentials Overview: https://www.w3.org/TR/vc-overview/
- Verifiable Credentials Data Model v2.0: https://www.w3.org/TR/vc-data-model-2.0/
- Verifiable Credential Data Integrity 1.0: https://www.w3.org/TR/vc-data-integrity/
- Securing Verifiable Credentials using JOSE and COSE: https://www.w3.org/TR/vc-jose-cose/
- Bitstring Status List: https://www.w3.org/TR/vc-bitstring-status-list/
- W3C press release (VC 2.0 Recommendation announcement): https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/
