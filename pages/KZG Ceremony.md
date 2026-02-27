# KZG Ceremony

The **KZG Ceremony** (also referred to as Ethereum’s **KZG Summoning Ceremony**) was a public multi-party computation (MPC) “trusted setup” organized by the Ethereum community to generate a **structured reference string (SRS)** for **KZG (Kate–Zaverucha–Goldberg) polynomial commitments**. These commitments are used by Ethereum’s **EIP-4844** (“proto-danksharding”) to commit to *blob* data for rollups. The ceremony’s security relies on a **1-of-N trust assumption**: the resulting SRS is considered secure as long as at least one participant keeps their secret contribution unknown and destroys it after contributing.\[1\]\[2\]

## Background

KZG polynomial commitments are a cryptographic commitment scheme that enables succinct proofs about evaluations of polynomials. In Ethereum’s data-availability scaling designs, KZG commitments are used to commit to blob data and to verify proofs about that data, while keeping blob contents **non-accessible to EVM execution**.\[3\]

Because KZG commitments require public parameters derived from secret randomness (sometimes described as “toxic waste”), deployments commonly use an MPC ceremony to generate those parameters without any single party learning the secret.\[1\]

## Purpose in Ethereum

Ethereum’s EIP-4844 introduces “blob-carrying transactions” as a stop-gap data-availability mechanism on the path to full data sharding. The EIP specifies that blob data is committed to using KZG commitments, and includes an execution-layer **point evaluation precompile** used to verify KZG proofs.\[3\]

The KZG Ceremony was organized to produce the SRS required by these commitments and proofs, providing a cryptographic foundation for proto-danksharding.\[1\]

## Design

### Participants and sequencer

The ceremony is an MPC between many **participants** and a coordinating **sequencer**. Participants contribute secret randomness that is mixed into the evolving ceremony state; the sequencer coordinates the process and publishes an auditable record (a “transcript”) that can be independently checked.\[1\]\[2\]

### Security model

The ceremony is designed so that compromising the final SRS requires either learning the secret randomness from *every* participant (or otherwise reconstructing it), or exploiting a flaw in the ceremony implementation. This is often summarized as a **“1-of-N”** assumption: a single honest participant who destroys their secret is sufficient for security.\[1\]

## Outcomes

An Ethereum Foundation retrospective described the KZG Ceremony as the largest MPC of its kind by number of participants at the time of publication. It reports that the ceremony ran for **208 days** (from **Jan 13, 2023** to **Aug 8, 2023**) and produced **141,416 contributions**.\[2\]

The same retrospective provides a **SHA-256 hash** of the final transcript output and states that the transcript was published for public verification, including via the official ceremony website and a dedicated verifier tool.\[2\]

## Relationship to EIP-4844 (proto-danksharding)

EIP-4844 defines “blob-carrying transactions” and introduces protocol rules and interfaces for blob commitments and proofs. It explicitly notes that blob data is not accessible to EVM execution, while commitments are. The EIP also specifies a point evaluation precompile (address `0x0A`) as part of the execution-layer interface for verifying KZG proofs.\[3\]

## See also

- **EIP-4844**
- **Trusted setup**
- **Polynomial commitment**

## References

1. Ethereum Foundation. “Announcing the KZG Ceremony.” *Ethereum Foundation Blog* (16 January 2023). https://blog.ethereum.org/2023/01/16/announcing-kzg-ceremony
2. Ethereum Foundation. “Wrapping up the KZG Ceremony.” *Ethereum Foundation Blog* (23 January 2024). https://blog.ethereum.org/2024/01/23/kzg-wrap
3. Ethereum Improvement Proposals. “EIP-4844: Shard Blob Transactions.” https://eips.ethereum.org/EIPS/eip-4844
