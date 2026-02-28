---
title: Verifiable Credentials Data Model 2.0
---

# Verifiable Credentials Data Model 2.0

**Verifiable Credentials Data Model 2.0 (VCDM 2.0)** is a World Wide Web Consortium (W3C) Recommendation that defines a data model for representing *verifiable credentials* and *verifiable presentations* on the Web. The specification describes a three-party ecosystem—**issuer**, **holder**, and **verifier**—and provides a framework for expressing claims with cryptographic verifiability, with associated security and privacy considerations.

## Overview

The VCDM defines a common structure for credentials that can be expressed in different concrete representations (for example, JSON-based serializations). A verifiable credential is intended to be:

- **Tamper-evident**, such that unauthorized modification can be detected.
- **Machine-verifiable**, enabling automated processing by software.
- **Extensible**, allowing domain-specific vocabularies and additional properties.

A related construct, the **verifiable presentation**, is used by a holder to present one or more credentials to a verifier.

## Ecosystem roles

The specification models credential exchange using three primary roles:

- **Issuer**: creates and cryptographically secures a credential about a subject.
- **Holder**: stores credentials and creates presentations for verifiers.
- **Verifier**: checks the authenticity and integrity of a credential or presentation.

## Data model concepts

VCDM 2.0 defines core concepts and properties used to describe credentials and presentations, including:

- **Claims**: statements made by an issuer about a subject.
- **Credential subject**: the entity described by the claims.
- **Issuer identification**: information used to identify the issuer.
- **Proofs**: cryptographic material used to verify integrity and provenance.

The specification is designed to be compatible with Web architecture and linked-data style extensibility, and it includes guidance on internationalization and accessibility considerations.

## Standardization

In May 2025, W3C announced the publication of the Verifiable Credentials 2.0 family of specifications as W3C Recommendations, including **Verifiable Credentials Data Model v2.0**.

## See also

- [[Verifiable credentials]]
- [[Decentralized identifier]]

## References

1. W3C. *Verifiable Credentials Data Model v2.0* (W3C Recommendation). https://www.w3.org/TR/vc-data-model-2.0/
2. W3C News. *The Verifiable Credentials 2.0 family of specifications is now a W3C Recommendation* (15 May 2025). https://www.w3.org/news/2025/the-verifiable-credentials-2-0-family-of-specifications-is-now-a-w3c-recommendation/
3. W3C Press Release. *W3C publishes Verifiable Credentials 2.0 as a W3C Standard* (2025). https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/
