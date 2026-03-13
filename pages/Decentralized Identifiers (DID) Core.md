# Decentralized Identifiers (DID) Core

**Decentralized Identifiers (DIDs)** are a type of identifier designed to enable **verifiable, decentralized digital identity**. The W3C specification *Decentralized Identifiers (DIDs) v1.0* defines the DID syntax, DID URLs, and the concept of a **DID document** that can be resolved from a DID to obtain cryptographic material and service endpoints associated with the identifier.[^did-core]

DIDs are commonly discussed alongside the W3C **Verifiable Credentials** work, where DIDs can be used to identify issuers, holders, and verifiers.

## Overview

### Identifier model
A DID is a URI with the general form:

```
did:<method>:<method-specific-identifier>
```

A DID may be extended into a **DID URL** by adding standard URI components such as path, query, and fragment, enabling references to resources or keys associated with the DID.[^did-core]

### DID documents and resolution
The DID Core specification defines a **DID document** as a set of data describing a DID subject, including (among other things):

- **Verification methods**, such as public keys used for authentication or assertion.
- **Service endpoints**, describing how to interact with the DID subject.

How a DID is resolved into a DID document depends on the **DID method** (e.g., `did:web`, `did:key`, and other method specifications). DID Core defines the abstract data model and processing expectations, while individual methods define concrete resolution and update mechanisms.[^did-core]

## Relationship to verifiable credentials
The W3C Verifiable Credentials ecosystem defines data models for **verifiable credentials** and **verifiable presentations**. DIDs are often used as identifiers within these systems, but DID Core itself is method-agnostic and does not require a specific credential format.[^vc-dm-2]

## Standardization

### W3C Recommendation
*Decentralized Identifiers (DIDs) v1.0* is published as a W3C Recommendation.[^did-core]

## See also

- [OpenID for Verifiable Credential Issuance (OID4VCI)](OpenID%20for%20Verifiable%20Credential%20Issuance%20%28OID4VCI%29.md)
- [OpenID for Verifiable Presentations (OID4VP)](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)
- [OAuth 2.0 Token Exchange (RFC 8693)](OAuth%202.0%20Token%20Exchange%20%28RFC%208693%29.md)

## References

[^did-core]: W3C. *Decentralized Identifiers (DIDs) v1.0* (W3C Recommendation). https://www.w3.org/TR/did-core/

[^vc-dm-2]: W3C. *Verifiable Credentials Data Model v2.0*. https://www.w3.org/TR/vc-data-model-2.0/
