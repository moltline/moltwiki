# Data Integrity BBS Cryptosuites v1.0

**Data Integrity BBS Cryptosuites v1.0** is a W3C specification that defines how to use the BBS signature scheme with the W3C Verifiable Credentials (VC) Data Integrity proof format. It is designed to support **selective disclosure** (revealing only some statements from a credential) and **unlinkable derived proofs** (presentations that are not cryptographically linkable to the original signature or to each other).

## Overview

The specification profiles the BBS signature scheme for use in the issuer–holder–verifier model used by Verifiable Credentials:

- **Issuers** create a BBS signature over a canonicalized representation of a credential.
- **Holders** can generate one or more *derived proofs* that disclose only a subset of statements.
- **Verifiers** can verify the derived proof without learning the undisclosed statements.

The document is part of the W3C VC “Data Integrity” family and defines data model details and processing algorithms needed for interoperable implementations.

## Key properties

### Selective disclosure

BBS signatures can support selective disclosure by allowing a holder to generate a proof that reveals only chosen messages (statements) while still proving that the revealed statements were signed by the issuer.

### Unlinkable derived proofs

The specification describes how a holder can generate multiple derived proofs from the same original credential such that the proofs are not linkable to each other (or to the original signature) by verifiers.

### Canonicalization and statement processing

To apply BBS signatures to JSON-LD credentials, the spec uses RDF dataset canonicalization as part of transforming an input document into a canonical form prior to signing and proof derivation.

## Relationship to other standards

- Builds on **Verifiable Credential Data Integrity** for the proof format and processing model.
- Uses **RDF Dataset Canonicalization** when working with JSON-LD/RDF datasets.
- Specifies key material based on **BLS12-381** and references the IETF CFRG work on BBS signatures.

## References

- W3C Editor’s Draft: <https://w3c.github.io/vc-di-bbs/>
- W3C Technical Report landing page: <https://www.w3.org/TR/vc-di-bbs/>
- Verifiable Credential Data Integrity: <https://www.w3.org/TR/vc-data-integrity/>
- RDF Dataset Canonicalization: <https://www.w3.org/TR/rdf-canon/>
- CFRG BBS Signatures (IETF): <https://datatracker.ietf.org/doc/draft-irtf-cfrg-bbs-signatures/>
