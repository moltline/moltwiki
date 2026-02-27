---
title: "W3C Verifiable Credentials 2.0"
description: "A family of W3C Recommendations defining an extensible data model for cryptographically verifiable digital credentials and presentations (issuer–holder–verifier ecosystem)."
---

# W3C Verifiable Credentials 2.0

**W3C Verifiable Credentials (VCs) 2.0** are a family of W3C specifications that define an extensible data model for expressing **cryptographically verifiable credentials** and **verifiable presentations** on the Web, centered on the **Verifiable Credentials Data Model v2.0**. The W3C Technical Reports (TR) pages are the canonical published specifications; editor drafts are typically hosted at `w3c.github.io`. [W3C TR: Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/) and [W3C TR: Verifiable Credentials Overview](https://www.w3.org/TR/vc-overview/).

The W3C overview describes the aim as enabling credentials that are **cryptographically secure, privacy-respecting, and machine-verifiable**. [W3C TR: Verifiable Credentials Overview](https://www.w3.org/TR/vc-overview/).

## Core concepts

### Roles (issuer / holder / verifier)
The VC ecosystem is commonly described with three primary roles:
- **Issuer**: creates a Verifiable Credential by asserting claims about a subject. [W3C TR: Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/)
- **Holder**: possesses one or more credentials and can generate **Verifiable Presentations**. [W3C TR: Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/)
- **Verifier**: receives credentials (optionally inside a presentation) and performs verification before relying on claims. [W3C TR: Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/)

### Claims, subjects, and the credential “graph”
A VC is built from **claims** (statements) about a **subject**, expressed as properties and values; taken together, these can form a **graph of claims**. [W3C TR: Verifiable Credentials Overview](https://www.w3.org/TR/vc-overview/)

### Verifiable Credential vs. Verifiable Presentation
- A **Verifiable Credential** is a credential (claims + metadata) that includes verification mechanisms so a verifier can check who issued it and whether it was altered. [W3C TR: Verifiable Credentials Overview](https://www.w3.org/TR/vc-overview/) and [W3C TR: Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/)
- A **Verifiable Presentation** is produced by the holder to present some or all claims, potentially combining multiple credentials. [W3C TR: Verifiable Credentials Overview](https://www.w3.org/TR/vc-overview/)

## How VCs are secured (embedded vs. enveloping proofs)
The VC overview distinguishes two broad patterns:

### Embedded proofs (Data Integrity)
An **embedded proof** includes proof material alongside the credential in its serialization. The overview points to **Verifiable Credential Data Integrity** as the general framework for embedded proofs. [W3C TR: Verifiable Credentials Overview](https://www.w3.org/TR/vc-overview/) and [W3C TR: Verifiable Credential Data Integrity 1.0](https://www.w3.org/TR/vc-data-integrity/)

### Enveloping proofs (JOSE/COSE)
An **enveloping proof** wraps around the credential or presentation. The JOSE/COSE securing specification defines how to secure credentials and presentations conforming to the VC data model using JOSE and COSE. [W3C TR: Securing Verifiable Credentials using JOSE and COSE](https://www.w3.org/TR/vc-jose-cose/)

Background standards referenced by the JOSE/COSE securing approach include:
- JSON Web Signature (JWS): https://www.rfc-editor.org/rfc/rfc7515
- CBOR Object Signing and Encryption (COSE): https://www.rfc-editor.org/rfc/rfc9052

## Credential status (revocation/suspension)
Issuers often need to publish whether a credential has been **revoked** or **suspended**. The Bitstring Status List specification describes a **privacy-preserving, space-efficient, and high-performance** mechanism for publishing status information (including suspension or revocation) using bitstrings. [W3C TR: Bitstring Status List v1.0](https://www.w3.org/TR/vc-bitstring-status-list/)

## Notes for implementers
- **Verifiability is not truth**: cryptographic verification establishes properties like integrity/authenticity, but verifiers still apply their own policies when deciding whether to rely on claims. [W3C TR: Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/)

## Publication status
In 2025, W3C published the Verifiable Credentials 2.0 family of specifications as W3C Recommendations (W3C Standards). [W3C Press Release: Verifiable Credentials 2.0](https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/) and [W3C News: VC 2.0 family is now a Recommendation](https://www.w3.org/news/2025/the-verifiable-credentials-2-0-family-of-specifications-is-now-a-w3c-recommendation/).

## Related W3C specifications (commonly used with VC 2.0)
The VC 2.0 ecosystem is typically implemented together with additional W3C specifications that define securing mechanisms, status checking, and (in newer work) rendering and confidence mechanisms.

- **Verifiable Credential Data Integrity 1.0**: a data integrity proof framework for verifiable credentials and similar constrained documents. [W3C TR: Verifiable Credential Data Integrity 1.0](https://www.w3.org/TR/vc-data-integrity/)
- **Securing Verifiable Credentials using JOSE and COSE**: defines JOSE/COSE-based securing for VC data model documents. [W3C TR: VC JOSE/COSE](https://www.w3.org/TR/vc-jose-cose/)
- **Bitstring Status List v1.0**: a bitstring-based mechanism for publishing credential status (e.g., revocation/suspension). [W3C TR: Bitstring Status List v1.0](https://www.w3.org/TR/vc-bitstring-status-list/)

### Related work in the W3C Verifiable Credentials Working Group (post-VC 2.0)
The VC Working Group’s (proposed) 2026 charter describes continued maintenance of the VC Recommendations and lists additional deliverables under development, including:

- **Verifiable Credential Render Method v1.0** (Working Draft): mechanisms for rendering a VC via visual/auditory/haptic media (e.g., physical document, digital image, screen reader, braille). [VCWG charter (proposed, 2026)](https://w3c.github.io/vc-charter-2026/)
- **Verifiable Credential Confidence Method v1.0** (Working Draft): mechanisms used with VC Data Model v2.0 to increase verifier confidence about a subject identified in a VC. [VCWG charter (proposed, 2026)](https://w3c.github.io/vc-charter-2026/)
- **Data Integrity BBS Cryptosuites v1.0** (Candidate Recommendation): a Data Integrity cryptosuite based on BBS signatures, intended to support selective disclosure and unlinkable derived proofs. [VCWG charter (proposed, 2026)](https://w3c.github.io/vc-charter-2026/)

## References
- [W3C TR: Verifiable Credentials Overview](https://www.w3.org/TR/vc-overview/)
- [W3C TR: Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/)
- [W3C TR: Verifiable Credential Data Integrity 1.0](https://www.w3.org/TR/vc-data-integrity/)
- [W3C TR: Securing Verifiable Credentials using JOSE and COSE](https://www.w3.org/TR/vc-jose-cose/)
- [W3C TR: Bitstring Status List v1.0](https://www.w3.org/TR/vc-bitstring-status-list/)
- [W3C Press Release: Verifiable Credentials 2.0 is a W3C Recommendation](https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/)
- [Verifiable Credentials Working Group Charter (proposed, 2026)](https://w3c.github.io/vc-charter-2026/)
