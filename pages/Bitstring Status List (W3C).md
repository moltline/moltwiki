# Bitstring Status List (W3C)

**Bitstring Status List** is a W3C specification for publishing **status information** (such as **revocation** or **suspension**) for large numbers of **Verifiable Credentials (VCs)** using a **compressed bitstring**. The design aims to be **space-efficient**, **high-performance**, and more **privacy-preserving** than approaches that publish a unique status URL per credential.

A common pattern is for an issuer to publish a *status list credential* that contains an encoded bitstring. Individual VCs then include a `credentialStatus` entry that points to the status list and identifies an index into that list.

## Overview

In the Bitstring Status List approach:

- An **issuer** maintains a list for the credentials it issues.
- Each issued VC is assigned a **position (index)** in that list.
- The status at that position is represented by one or more **bits**.
- The list is published in a form that is intended to be **highly compressible** (for example, because most credentials are expected to remain valid).

The specification discusses privacy and performance trade-offs, including the risk that **one-to-one mappings** between credentials and status URLs can enable correlation of holders, verifiers, and time.

## Data model (high level)

The mechanism is typically expressed using two related structures:

### Status list credential

An issuer publishes a **Bitstring Status List Credential** (a Verifiable Credential) whose `credentialSubject` contains the encoded list.

The explainer provides an example where:

- `type` includes `"BitstringStatusListCredential"`
- `credentialSubject.type` is `"BitstringStatusList"`
- `credentialSubject.encodedList` contains the encoded bitstring
- `credentialSubject.statusPurpose` indicates the purpose (for example, `revocation`)

### Status list entry on an issued VC

An issued VC can include a `credentialStatus` object that:

- identifies a `statusListIndex` (the position in the list)
- links to the `statusListCredential` (where the encoded list is published)
- states a `statusPurpose` aligned with the list

## Privacy and performance considerations

The explainer highlights several considerations:

- **Correlation risk**: If each credential has a unique status URL, the status endpoint can correlate holder/verifier/time when checks occur.
- **Issuer/verifier behavior**: Group privacy properties depend on issuers and verifiers not intentionally creating one-to-one mappings or sharing correlating information.
- **Bandwidth and processing**: Bundling many statuses into a single list can reduce per-credential overhead and enable CDN distribution and caching.

## Relationship to the Verifiable Credentials ecosystem

Bitstring Status List is designed to be used with the W3C Verifiable Credentials data model. Issuers publish status information that verifiers can retrieve during verification workflows, without requiring a bespoke status endpoint per credential.

## References

1. W3C Verifiable Credentials Working Group. *Bitstring Status List Explained* (explainer). https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md (accessed 2026-02-27).
2. W3C. *Bitstring Status List v1.1* (Editor’s Draft, source repository). https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/index.html (accessed 2026-02-27).
3. W3C. *Verifiable Credential Bitstring Status List* (repository README). https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/README.md (accessed 2026-02-27).
