# Controlled Identifiers (W3C)

**Controlled Identifiers** are a W3C specification that defines a family of data model concepts for **identifier documents** that contain **cryptographic material** (for example, verification methods) and optionally **service endpoints**, for use in verifying cryptographic proofs.

In the W3C Verifiable Credentials ecosystem, Controlled Identifiers provides common terminology and a baseline model for expressing verification relationships and methods that can be referenced by other specifications.

## Overview

A controlled identifier document is intended to:

- associate an identifier with **verification methods** (cryptographic public keys and related metadata), and
- express **verification relationships** (how a verification method is used, such as for authentication or assertion), and
- optionally advertise **service endpoints**.

The specification is designed to be usable by multiple identifier systems and proof formats.

## Core concepts

### Controlled identifier document

A **controlled identifier document** is a document associated with an identifier. It contains cryptographic and service information used by verifiers.

### Verification methods

A **verification method** represents cryptographic material (typically a public key) plus metadata needed to use it.

### Verification relationships

A **verification relationship** links verification methods to particular proof purposes (for example, authentication or assertion).

### Service endpoints

A controlled identifier document may include **service endpoints** that advertise ways to interact with the controller of the identifier.

## Relationship to Verifiable Credentials

Verifiable Credentials specifications often rely on external mechanisms to express and resolve public keys and verification relationships. Controlled Identifiers provides shared definitions and a common model that can be referenced when describing how proofs are verified.

## References

- W3C Technical Report: **Controlled Identifiers v1.0**: https://www.w3.org/TR/cid-1.0/
- Editor’s Draft (source): https://github.com/w3c/cid
- Verifiable Credentials Overview (mentions Controlled Identifiers): https://www.w3.org/TR/vc-overview/
