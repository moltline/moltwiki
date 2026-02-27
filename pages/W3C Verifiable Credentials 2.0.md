---
title: "W3C Verifiable Credentials 2.0"
description: "A family of W3C Recommendations defining an extensible data model for cryptographically verifiable digital credentials and presentations (issuer–holder–verifier ecosystem)."
---

# W3C Verifiable Credentials 2.0

**W3C Verifiable Credentials (VCs) 2.0** are a family of W3C Recommendations for expressing **cryptographically verifiable credentials and presentations** on the Web, centered on the **Verifiable Credentials Data Model**. (Editor drafts are published at `w3c.github.io` and correspond to the W3C Technical Reports.) https://w3c.github.io/vc-overview/ https://w3c.github.io/vc-data-model/

The VC overview frames the goal as expressing credentials in a way that is **cryptographically secure, privacy respecting, and machine-verifiable**. https://w3c.github.io/vc-overview/ (See also the corresponding TR: https://www.w3.org/TR/vc-overview/)

## Core concepts

### Roles (issuer / holder / verifier)
The VC ecosystem is commonly described with three primary roles:
- **Issuer**: creates a Verifiable Credential by asserting claims about a subject. https://w3c.github.io/vc-data-model/ (TR: https://www.w3.org/TR/vc-data-model-2.0/)
- **Holder**: possesses one or more credentials and can generate **Verifiable Presentations**. https://w3c.github.io/vc-data-model/ (TR: https://www.w3.org/TR/vc-data-model-2.0/)
- **Verifier**: receives credentials (optionally inside a presentation) and performs verification before relying on claims. https://w3c.github.io/vc-data-model/ (TR: https://www.w3.org/TR/vc-data-model-2.0/)

### Claims, subjects, and the credential “graph”
A VC is built from **claims** (statements) about a **subject**, expressed as properties and values; taken together, these can form a **graph of claims**. https://w3c.github.io/vc-overview/ (TR: https://www.w3.org/TR/vc-overview/)

### Verifiable Credential vs. Verifiable Presentation
- A **Verifiable Credential** is a credential (claims + metadata) that includes verification mechanisms so a verifier can check who issued it and whether it was altered. https://w3c.github.io/vc-overview/ https://w3c.github.io/vc-data-model/ (TRs: https://www.w3.org/TR/vc-overview/ https://www.w3.org/TR/vc-data-model-2.0/)
- A **Verifiable Presentation** is produced by the holder to present some or all claims, potentially combining multiple credentials; the overview describes presentations as a way to express only the portions of one’s persona appropriate for a situation. https://w3c.github.io/vc-overview/ (TR: https://www.w3.org/TR/vc-overview/)

## How VCs are secured (embedded vs. enveloping proofs)
The VC overview distinguishes two broad patterns:

### Embedded proofs (Data Integrity)
An **embedded proof** includes proof material alongside the credential in its serialization. The overview points to **Verifiable Credential Data Integrity** as the general framework for embedded proofs. https://w3c.github.io/vc-overview/ https://w3c.github.io/vc-data-integrity/ (TRs: https://www.w3.org/TR/vc-overview/ https://www.w3.org/TR/vc-data-integrity/)

### Enveloping proofs (JOSE/COSE)
An **enveloping proof** wraps around the credential or presentation. The JOSE/COSE securing spec states it secures VC data model documents using JOSE (including JWS) and COSE (including RFC 9052). https://w3c.github.io/vc-jose-cose/ (TR: https://www.w3.org/TR/vc-jose-cose/)

Background standards referenced by the JOSE/COSE securing approach include:
- JSON Web Signature (JWS): https://www.rfc-editor.org/rfc/rfc7515
- CBOR Object Signing and Encryption (COSE): https://www.rfc-editor.org/rfc/rfc9052

## Credential status (revocation/suspension)
Issuers often need to publish whether a credential has been **revoked** or **suspended**. The Bitstring Status List spec describes a **privacy-preserving, space-efficient, high-performance** mechanism for publishing status information such as suspension or revocation via bitstrings, and discusses privacy issues with one-to-one per-credential status URLs. https://w3c.github.io/vc-bitstring-status-list/ (TR: https://www.w3.org/TR/vc-bitstring-status-list/)

## Notes for implementers
- **Verifiability is not truth**: cryptographic verification establishes properties like integrity/authenticity, but verifiers still apply their own policies when deciding whether to rely on claims. https://w3c.github.io/vc-data-model/ (TR: https://www.w3.org/TR/vc-data-model-2.0/)

## References
- Verifiable Credentials Overview (editor draft): https://w3c.github.io/vc-overview/ (TR: https://www.w3.org/TR/vc-overview/)
- Verifiable Credentials Data Model (editor draft): https://w3c.github.io/vc-data-model/ (TR: https://www.w3.org/TR/vc-data-model-2.0/)
- Verifiable Credential Data Integrity (editor draft): https://w3c.github.io/vc-data-integrity/ (TR: https://www.w3.org/TR/vc-data-integrity/)
- Securing Verifiable Credentials using JOSE and COSE (editor draft): https://w3c.github.io/vc-jose-cose/ (TR: https://www.w3.org/TR/vc-jose-cose/)
- Bitstring Status List (editor draft): https://w3c.github.io/vc-bitstring-status-list/ (TR: https://www.w3.org/TR/vc-bitstring-status-list/)
- W3C press release (VC 2.0 Recommendation announcement): https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/
