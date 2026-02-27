# CAIP-2 (Blockchain ID Specification)

**CAIP-2** (“Blockchain ID Specification”) is a *Chain Agnostic Improvement Proposal* that standardizes a **blockchain identifier** (short: **chain ID**) as a human-readable, developer-friendly string of the form `namespace:reference`.[1]

It is commonly used as the “chain identifier” component inside other CAIP identifiers (for accounts, assets, etc.) so that those identifiers can unambiguously specify *which network* they refer to.[1]

## Specification (syntax)

A CAIP-2 chain ID is a **case-sensitive** string with two components separated by a colon:[1]

```
chain_id:    namespace + ":" + reference
namespace:   [-a-z0-9]{3,8}
reference:   [-_a-zA-Z0-9]{1,32}
```

Practical notes:

* The full string is at most **41 characters** (8 + 1 + 32).[1]
* The allowed characters are intentionally constrained so chain IDs can fit in on-chain data structures and be displayed in constrained UX (e.g., hardware wallets).[1]

## Semantics

### Namespace

The **namespace** indicates a class of chains that share an identification and resolution method (e.g., an ecosystem or standard such as `eip155` or `cosmos`).[1]

CAIP-2’s intent is that a namespace maps to a well-defined **resolution method** for interpreting the `reference` value.[1]

### Reference

The **reference** identifies a specific chain *within* the namespace.[1]

CAIP-2 deliberately does **not** define what each reference means for each namespace; those details are delegated to separate namespace specifications.[1]

## Rationale (what CAIP-2 is trying to solve)

Many ecosystems have their own “chain id” concept (e.g., Ethereum’s EIP-155 chain ID), but those identifiers don’t generalize across ecosystems. CAIP-2 provides a single top-level format so software can represent “which chain?” consistently across many networks.[1]

The spec calls out these goals:[1]

* Global uniqueness across the broader blockchain ecosystem.
* Some degree of human readability (useful for debugging).
* Restricted length and character set so it can be stored on-chain and shown in constrained environments.

It also notes secondary goals such as being usable unescaped in URL paths and as filenames on case-sensitive UNIX filesystems, while explicitly giving up on case-insensitive filesystem compatibility.[1]

## Examples

From the CAIP-2 test cases and common usage:[1]

* `eip155:1` — Ethereum mainnet (EIP-155 chain id 1)
* `bip122:000000000019d6689c085ae165831e93` — Bitcoin mainnet (BIP-122-style genesis-hash-based reference)
* `cosmos:cosmoshub-3` — Cosmos Hub chain ID string

## Relationship to other identifiers

* **CAIP-10** (account identifiers) and **CAIP-19** (asset identifiers) build on the CAIP-2 chain ID so accounts/assets can be located on a specific network.[1]
* The `bip122` namespace is commonly understood to use the **genesis block hash** (or fork point) as the chain identifier concept described in BIP-122’s “Definition of chain ID”.[2]

## See also

* Chain Agnostic Improvement Proposals (CAIPs): https://github.com/ChainAgnostic/CAIPs
* CAIP-2 rendered spec: https://standards.chainagnostic.org/CAIPs/caip-2
* EIP-155 (Ethereum chain ID): https://eips.ethereum.org/EIPS/eip-155
* BIP-122 (Blockchain references / exploration): https://github.com/bitcoin/bips/blob/master/bip-0122.mediawiki

## References

1. Simon Warta; ligi; Pedro Gomes; Antoine Herzog. “CAIP-2: Blockchain ID Specification.” *Chain Agnostic Improvement Proposals* (Final; created 2019-12-05; updated 2021-08-25). https://standards.chainagnostic.org/CAIPs/caip-2 (accessed 2026-02-27).
2. Marco Pontello. “BIP 122: URI scheme for Blockchain references / exploration” (Draft). Section “Definition of chain ID” (genesis block hash / fork point). https://raw.githubusercontent.com/bitcoin/bips/master/bip-0122.mediawiki (accessed 2026-02-27).
