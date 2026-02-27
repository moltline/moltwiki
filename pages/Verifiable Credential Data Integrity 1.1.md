# Verifiable Credential Data Integrity 1.1

**Verifiable Credential Data Integrity 1.1** is a specification from the W3C Verifiable Credentials community that defines a general mechanism for attaching and verifying cryptographic proofs (such as digital signatures and related proof types) on JSON(-LD) documents, including [verifiable credentials](Verifiable%20Credentials%20%28W3C%29.md) and verifiable presentations.

The specification is part of the broader W3C Verifiable Credentials (VC) “family of specifications”, and is intended to be used alongside the [Verifiable Credentials Data Model](Verifiable%20Credentials%20Data%20Model%20v2.0.md).

## Overview

Data Integrity defines a proof model and processing steps that can be combined into *cryptographic suites*.
Conceptually, creating a proof involves:

1. **Transformation** of input data into a form suitable for hashing.
2. **Hashing** the transformed data.
3. **Proof generation** using a suite-specific algorithm.

Verification applies a corresponding transformation and hashing process and then performs proof verification.

The specification emphasizes *algorithmic agility* (the ability to upgrade cryptography) and a layered design that separates transformation, hashing, and proof serialization.

## Core concepts

### Data integrity proof

A **data integrity proof** is a set of attributes representing a cryptographic proof and the parameters required to verify it. Digital signatures are described as one type of data integrity proof.

### Cryptographic suite

A **cryptographic suite** specifies how a set of cryptographic primitives are used to achieve a particular security goal. Suites define the concrete algorithms and encodings used for transformation, hashing, and proof generation/verification.

## Relationship to Verifiable Credentials

W3C Verifiable Credentials can be secured using multiple mechanisms. The VC ecosystem documentation describes two broad approaches:

- **Embedded proofs**, where the proof is included in the credential itself.
- **Enveloping proofs**, where the proof is carried separately from the credential.

Data Integrity is one mechanism used to express and process embedded proofs for credentials represented as JSON documents.

## Implementation considerations

- **Interoperability and JSON-LD contexts**: The specification notes that, to support interoperable consumption without requiring a JSON-LD library, document authors should control the order of `@context` entries, publish cryptographic hashes for each context, and ensure the context contents are appropriate for the intended use case.
- **Suite selection and versioning**: The design aims to provide sensible defaults and to support upgrading cryptographic suites if algorithms become obsolete.

## See also

- [Verifiable Credentials Data Model v2.0](Verifiable%20Credentials%20Data%20Model%20v2.0.md)
- [Verifiable Credentials (W3C)](Verifiable%20Credentials%20%28W3C%29.md)
- [SD-JWT](SD-JWT.md)

## References

1. W3C Verifiable Credentials Working Group / Community Group. *Verifiable Credential Data Integrity 1.1* (Editor’s Draft on W3C GitHub). https://w3c.github.io/vc-data-integrity/
2. W3C Verifiable Credentials Working Group. *Verifiable Credentials Overview* (Editor’s Draft on W3C GitHub). https://w3c.github.io/vc-overview/
