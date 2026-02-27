# CAIP-2 (Blockchain ID Specification)

**CAIP-2** ("Blockchain ID Specification") is a *Chain Agnostic Improvement Proposal* that defines a standard, human-readable identifier for a blockchain network (for example, Ethereum mainnet, a Bitcoin network, or a Cosmos Hub) using a `namespace:reference` string format.[1] The identifier is commonly referred to as a **chain ID** in CAIP terminology.[1]

## Specification

CAIP-2 defines a case-sensitive string with two components separated by a colon:[1]

```
chain_id:    namespace + ":" + reference
namespace:   [-a-z0-9]{3,8}
reference:   [-_a-zA-Z0-9]{1,32}
```

### Semantics

In CAIP-2, a **namespace** groups related chains under a shared identification and resolution approach (for example, an ecosystem or standard such as `eip155` for Ethereum-style chain IDs).[1] The **reference** identifies a particular chain within that namespace.[1]

CAIP-2 specifies the top-level format and delegates the detailed meaning and resolution rules for each namespace to separate specifications.[1]

## Rationale and goals

CAIP-2 was designed to provide chain identifiers that are:[1]

* **Unique** across the broader blockchain ecosystem.
* **Human-readable** enough to aid debugging.
* **Restricted in length and character set** so they can be stored on-chain and displayed in constrained environments (such as hardware wallets).

## Examples

The CAIP-2 specification includes illustrative examples such as:[1]

* `eip155:1` (Ethereum mainnet)
* `bip122:000000000019d6689c085ae165831e93` (Bitcoin mainnet; using a BIP-122 genesis-hash-based reference)
* `cosmos:cosmoshub-3` (Cosmos Hub chain ID)

## Relationship to other CAIP identifiers

CAIP-2 defines a blockchain identifier format that is used by other chain-agnostic identifier standards. For example, CAIP-10 (account identifiers) and CAIP-19 (asset identifiers) build on the concept of a chain identifier to unambiguously locate accounts and assets on specific networks.[1]

## See also

* [Chain Agnostic Improvement Proposals (CAIPs)](https://github.com/ChainAgnostic/CAIPs)
* [EIP-155 (Ethereum chain ID)](https://eips.ethereum.org/EIPS/eip-155)

## References

1. ChainAgnostic. "CAIP-2: Blockchain ID Specification." *Chain Agnostic Improvement Proposals* (Final; updated 2021-08-25). https://raw.githubusercontent.com/ChainAgnostic/CAIPs/main/CAIPs/caip-2.md (accessed 2026-02-27).
