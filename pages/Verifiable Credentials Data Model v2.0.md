# Verifiable Credentials Data Model v2.0

The **Verifiable Credentials Data Model (VCDM) v2.0** is a W3C Recommendation that defines an extensible data model for expressing **verifiable credentials** and **verifiable presentations** on the Web.

It describes a three-party ecosystem (issuer, holder, verifier), the core properties used to represent credentials and presentations, and how these objects can be secured against tampering using one or more "verifiable credential securing mechanisms" (for example, data integrity proofs or JSON Web Tokens).

**Type:** W3C Recommendation (technical specification)  
**Status:** Recommendation  
**Specification:** https://www.w3.org/TR/vc-data-model-2.0/  
**Working Group:** W3C Verifiable Credentials Working Group  

## Overview

VCDM v2.0 standardizes a JSON(-LD) data model intended to make claims about a subject portable across systems, while allowing different ecosystems to choose appropriate security formats and trust frameworks.

At a high level:

- A **verifiable credential** is a set of claims made by an issuer about a subject, packaged in a standard data model.
- A **verifiable presentation** is a data model used to present one or more credentials (or derived claims) to a verifier.
- **Verifiability** is achieved by applying a securing mechanism and then checking it during verification.

## Core concepts

### Roles

The specification describes a common interaction model among:

- **Issuer**: creates and issues a verifiable credential.
- **Holder**: stores a credential and can present it.
- **Verifier**: requests and verifies a presentation.

### Data model objects

VCDM v2.0 defines the structure and semantics of:

- **Verifiable Credential** objects
- **Verifiable Presentation** objects

The model is designed to be extensible via additional properties and vocabularies.

### Securing mechanisms

Rather than mandating a single cryptographic format, VCDM v2.0 is designed to work with multiple securing mechanisms.

Examples of securing mechanisms referenced in the broader VC ecosystem include:

- **Data Integrity** proofs (e.g., Linked Data Proof-style approaches)
- **JWT-based** representations

Specific securing formats are typically defined in companion specifications.

## Related specifications and components

VCDM v2.0 is frequently used alongside:

- **Verifiable Credentials Overview** (W3C Note-style overview/roadmap)\[2\]
- **OpenID for Verifiable Credential Issuance (OID4VCI)** and **OpenID for Verifiable Presentations (OID4VP)** for request/response flows in OpenID-based ecosystems
- Status and revocation mechanisms such as **Status List 2021** and **Bitstring Status List**

## History

W3C publication history records VCDM v2.0 progressing through **Candidate Recommendation Draft** (25 February 2025) and **Proposed Recommendation** (20 March 2025) before reaching **Recommendation** maturity in May 2025.\[3\]

## See also

- [Verifiable Credentials (W3C)](./Verifiable%20Credentials%20(W3C).md)
- [W3C Verifiable Credentials 2.0](./W3C%20Verifiable%20Credentials%202.0.md)
- [Verifiable Credential Status List 2021](./Verifiable%20Credential%20Status%20List%202021.md)
- [Bitstring Status List (W3C)](./Bitstring%20Status%20List%20(W3C).md)

## References

1. W3C. *Verifiable Credentials Data Model v2.0* (Recommendation). https://www.w3.org/TR/vc-data-model-2.0/
2. W3C. *Verifiable Credentials Overview*. https://www.w3.org/TR/vc-overview/
3. W3C Standards. *Verifiable Credentials Data Model v2.0 — publication history*. https://www.w3.org/standards/history/vc-data-model-2.0/ (includes entries for Candidate Recommendation Draft (25 February 2025) and Proposed Recommendation (20 March 2025)).
