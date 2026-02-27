# Bitstring Status List (W3C)

**Bitstring Status List** is a W3C Verifiable Credentials Working Group specification for publishing **credential status information** (for example, **revocation** or **suspension**) for large numbers of **Verifiable Credentials (VCs)** using a **bitstring** that is intended to compress well (e.g., with GZIP). It is designed to be **space-efficient**, **high-performance**, and to improve **privacy** relative to schemes that publish a unique, per-credential status URL. https://w3c.github.io/vc-bitstring-status-list/

At a high level, an issuer publishes a *status list credential* containing an encoded bitstring. Each issued VC includes a `credentialStatus` entry that points to that status list and identifies the VC’s position in it (an index). https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md

## Why bitstrings?

The core idea is to express many credential statuses as bits in a single list:

- The issuer assigns each issued VC a **status list index**.
- The status list encodes a bitstring where each position corresponds to one VC.
- When a single bit is used, the specification’s conceptual model is: `1` means the status is true (e.g., revoked/suspended) and `0` means false. https://w3c.github.io/vc-bitstring-status-list/

Because most credentials are expected to remain valid, the bitstring tends to contain long runs of identical values and is therefore highly compressible (the spec discusses GZIP compression and gives concrete size examples). https://w3c.github.io/vc-bitstring-status-list/

## Data model (what shows up in credentials)

The mechanism is expressed using two related structures:

### 1) Status list credential (`BitstringStatusListCredential`)

The issuer publishes a **Verifiable Credential** whose `type` includes `"BitstringStatusListCredential"`. Its `credentialSubject` contains the list material (including `encodedList`) and metadata such as `statusPurpose`. https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md

Common fields (illustrative):

- `type`: `"BitstringStatusListCredential"` (alongside `"VerifiableCredential"`)
- `credentialSubject.type`: `"BitstringStatusList"`
- `credentialSubject.encodedList`: the encoded (and typically compressed) bitstring
- `credentialSubject.statusPurpose`: the purpose of the list (e.g., `"revocation"`) https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md

### 2) Status list entry on an issued VC (`BitstringStatusListEntry`)

An issued VC can include a `credentialStatus` object with `type` `"BitstringStatusListEntry"` that links the VC to the list:

- `statusListIndex`: the position in the list
- `statusListCredential`: a URL for the status list credential
- `statusPurpose`: the purpose of the status entry (must align with the list) https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md

The specification further constrains and describes these properties (for example, it notes that the optional `credentialStatus.id` is not the URL of the status list itself and is not used during verification). https://w3c.github.io/vc-bitstring-status-list/

## Privacy and performance considerations

The spec motivates this design with privacy and performance trade-offs:

- **Correlation risk with per-credential URLs**: a one-to-one mapping between a credential and a status URL can allow the status publisher to correlate the holder, verifier, and time of checks. https://w3c.github.io/vc-bitstring-status-list/
- **Group privacy**: bundling many credentials into one list can help hide any single holder’s activity within a larger set (though the explainer notes these protections can be undermined by malicious issuers/verifiers creating one-list-per-credential or otherwise reintroducing one-to-one mappings). https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md
- **Caching and CDNs**: distributing a single list via caching/CDNs can reduce load and can reduce direct issuer visibility into verifier fetch patterns. https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md

## Relationship to the VC ecosystem

Bitstring Status List is intended to be used with the W3C Verifiable Credentials data model: issuers publish status information that verifiers retrieve during verification workflows, without requiring a bespoke status endpoint per credential. https://w3c.github.io/vc-bitstring-status-list/

## References

- Bitstring Status List v1.1 (Editor’s Draft): https://w3c.github.io/vc-bitstring-status-list/
- Bitstring Status List Explained (explainer): https://raw.githubusercontent.com/w3c/vc-bitstring-status-list/main/EXPLAINER.md
- vc-bitstring-status-list source (for issues/history): https://github.com/w3c/vc-bitstring-status-list
