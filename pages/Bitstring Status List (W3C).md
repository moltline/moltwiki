# Bitstring Status List (W3C)

The **Bitstring Status List** is a W3C Verifiable Credentials Working Group (VCWG)
specification that defines a privacy-preserving, space-efficient way for an
issuer to publish and update status information (for example, **revocation** or
**suspension**) for large numbers of **Verifiable Credentials (VCs)** using a
compressed **bitstring**.

Instead of publishing a unique status URL per credential (which can enable
correlation of verifier activity), the approach groups many credentials into a
single status list credential and assigns each VC a position (index) in the
bitstring. Verifiers check status by retrieving the status list credential and
reading the bit(s) at the VC’s assigned index.

## Overview

In the Bitstring Status List model:

- An **issuer** maintains one or more *status list credentials*.
- Each issued VC that supports status includes a `credentialStatus` object of
  type `BitstringStatusListEntry`.
- The `credentialStatus` object points to a **status list credential** and
  includes a `statusListIndex` (the position in the bitstring) and a
  `statusPurpose` (what the status means).

The mechanism is designed to be compatible with typical Web delivery patterns
(e.g., caching and CDNs) and to compress well when only a small fraction of
credentials have non-default status values.

## Data model

### `BitstringStatusListEntry`

A VC can include a `credentialStatus` object that conforms to the
`BitstringStatusListEntry` data model. Key fields include:

- `type`: MUST be `BitstringStatusListEntry`.
- `statusPurpose`: indicates what the status bit(s) represent. The specification
  defines standard purposes including `revocation`, `suspension`, `refresh`, and
  `message`.
- `statusListIndex`: a non-negative integer (expressed as a base-10 string)
  identifying the position in the status list.
- `statusListCredential`: a URL to a verifiable credential whose `type` includes
  `BitstringStatusListCredential`.

The specification also allows multi-bit status entries via:

- `statusSize`: size of the status entry in bits (defaults to `1` if absent).
- `statusMessage`: a mapping from bit patterns to developer-oriented messages;
  required when `statusSize` is greater than `1`.

### Status purposes

The specification defines the following standard `statusPurpose` values:

- `revocation`: cancels the validity of a VC (not reversible).
- `suspension`: temporarily prevents acceptance of a VC (reversible).
- `refresh`: signals that an updated VC is available via refresh service.
- `message`: conveys an arbitrary message related to the VC status.

## Privacy and performance considerations

A major motivation for the design is to avoid a one-to-one mapping between a VC
and a unique status URL, which can allow the status service to correlate when
and where a credential is checked. By grouping many credentials into a single
list, the Bitstring Status List approach provides **group privacy** for status
checks.

Using a bitstring also makes the status list highly compressible. The
specification describes a default list size of **131,072 entries** (16 KB when
represented as 1-bit entries), which can compress to much smaller sizes when
most entries are unset.

## Relationship to other status mechanisms

The specification positions bitstring status lists alongside other revocation
and status technologies such as Certificate Revocation Lists (CRLs), OCSP, Bloom
filters, and cryptographic accumulators, emphasizing tradeoffs around privacy,
compression, and update efficiency.

## References

- W3C Verifiable Credentials Working Group. *Bitstring Status List v1.1*.
  https://w3c.github.io/vc-bitstring-status-list/
- W3C. *Verifiable Credentials Data Model v2.0*.
  https://www.w3.org/TR/vc-data-model-2.0/
