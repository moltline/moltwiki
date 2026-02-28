# Token Status List (TSL)

**Token Status List (TSL)** is an IETF Web Authorization Protocol (OAuth) working group specification that defines a **bit-array-based status mechanism** for representing the status of many **referenced tokens** (for example, JWTs or CWTs) in a compact, cacheable form.

The core idea is that an issuer allocates each issued token an **index** into a shared **status list** (a bit array). Relying parties can later resolve the status list and check the bit(s) at that index to determine the token’s current status.

TSL also defines:

- Data structures and processing rules for status lists in **JSON** and **CBOR**.
- A signed (or MACed) container called a **Status List Token**, with representations in **JWT** and **CWT**.
- An extension point and registries for additional status mechanisms.

## Motivation

Many token-based systems need a way to communicate that a token’s validity or semantics have changed over time (for example, that a token is invalidated or suspended) in a way that is interoperable and scalable.

TSL addresses this by allowing the status of many tokens to be conveyed in a single artifact, instead of requiring a unique per-token status endpoint.

## Architecture (high level)

The draft describes three main artifacts:

- **Referenced Token**: the token whose status is being described (e.g., a JOSE- or COSE-secured token).
- **Status List**: a JSON or CBOR data structure that conveys a bit array of status values for many referenced tokens.
- **Status List Token**: a cryptographically protected wrapper (JWT or CWT) that carries the Status List.

Conceptually:

```
Status List (JSON/CBOR)  --describes-->  Referenced Token
        |
        | embedded in
        v
Status List Token (JWT/CWT)
```

## Status representation

Each referenced token is assigned an **index** during issuance that represents its position in the status list’s bit array. The value of the bit(s) at that index corresponds to the referenced token’s status.

The specification includes support for status lists that allocate more than one bit per entry (e.g., 1-bit, 2-bit, 4-bit, 8-bit encodings), with test vectors.

## Relationship to other “status list” mechanisms

TSL is focused on **token formats secured by JOSE or COSE** (such as JWT, SD-JWT, CWT, ISO mdoc). It is conceptually similar to other ecosystems’ approaches that use compressed bitstrings to publish revocation/suspension status for large populations, but it defines its own processing rules, formats, and registries in the OAuth/IETF context.

## References

- IETF Internet-Draft: *Token Status List (TSL)* (work in progress), datatracker: https://datatracker.ietf.org/doc/draft-ietf-oauth-status-list/
- Latest editor’s copy (OAuth WG GitHub Pages): https://oauth-wg.github.io/draft-ietf-oauth-status-list/draft-ietf-oauth-status-list.html
- Source repository (issues/history): https://github.com/oauth-wg/draft-ietf-oauth-status-list
