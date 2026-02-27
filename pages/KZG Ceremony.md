# KZG Ceremony

The **KZG Ceremony** is a public multi-party computation (MPC) “trusted setup” run by the Ethereum community to generate a **structured reference string (SRS)** for **KZG polynomial commitments** used in Ethereum’s scaling roadmap, most prominently **EIP-4844** (“proto-danksharding”). The ceremony’s security relies on a **1-of-N trust assumption**: the resulting SRS is considered secure as long as at least one participant keeps their secret contribution unknown to any adversary.

## Background

KZG (Kate–Zaverucha–Goldberg) polynomial commitments are a cryptographic commitment scheme that enables efficient proofs about evaluations of polynomials. In Ethereum’s data-availability scaling designs, KZG commitments are used to commit to “blob” data and to verify proofs about that data without making the full data directly accessible to EVM execution.

Because KZG commitments require public parameters derived from secret randomness (often described as a “toxic waste” secret), deployments commonly use an MPC ceremony to generate those parameters without any single party learning the secret.

## Purpose in Ethereum

Ethereum’s EIP-4844 introduces a new transaction type that carries *blobs* of data intended for rollups. The EIP specifies that blob data is committed to using KZG commitments, and that KZG proofs are verified by protocol-defined verification functions and a point-evaluation precompile.

The KZG Ceremony was organized to produce the SRS needed for these commitments and proofs, providing a cryptographic foundation for proto-danksharding and related scaling work.

## Design

### Participants and sequencer

The ceremony is an MPC between many **participants** and a coordinating **sequencer**. Each participant generates a secret value and combines it with the current ceremony state to create a new contribution. The sequencer verifies that contributions are well-formed and publishes an auditable transcript that can be independently checked.

### Security model

The ceremony is designed so that compromising the final SRS requires either:

- learning the secret randomness from *every* participant (or otherwise reconstructing it), or
- exploiting an implementation flaw across the participating software.

This is often summarized as a **“1-of-N”** assumption: a single honest participant who destroys their secret is sufficient for security.

### Accessibility and implementations

The Ethereum KZG Ceremony was intended to be broadly accessible, including browser-based participation and multiple independent client implementations. The public documentation repository lists audited components and a range of client implementations.

## Relationship to EIP-4844 (proto-danksharding)

EIP-4844 defines “blob-carrying transactions” and introduces protocol rules and interfaces for blob commitments and proofs. The EIP references consensus-layer specifications for KZG verification and defines an execution-layer precompile for point evaluation proofs.

## Auditing and verification

Ceremony documentation includes references to third-party audits of parts of the ceremony software and encourages independent verification of the published transcript and final output.

## See also

- **EIP-4844**
- **Trusted setup**
- **Polynomial commitment**

## References

- Ethereum Foundation. “Announcing the KZG Ceremony.” *Ethereum Foundation Blog* (16 January 2023). https://blog.ethereum.org/2023/01/16/announcing-kzg-ceremony
- Ethereum Foundation (GitHub). “ethereum/kzg-ceremony: Resources and documentation related to the ongoing Ethereum KZG Ceremony.” https://github.com/ethereum/kzg-ceremony
- Ethereum Improvement Proposals. “EIP-4844: Shard Blob Transactions.” https://eips.ethereum.org/EIPS/eip-4844
