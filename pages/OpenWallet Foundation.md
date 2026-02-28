---
title: OpenWallet Foundation (OWF)
---

# OpenWallet Foundation (OWF)

The **OpenWallet Foundation (OWF)** is a collaborative initiative hosted by **Linux Foundation Europe** to develop **open-source components** that support interoperable **digital wallet** use cases such as payments, identity, and storage/presentation of validated credentials.[^lf-europe-launch] OWF positions itself as building a reusable **wallet “engine”** (infrastructure and components) rather than publishing an end-user wallet product or creating new standards.[^lf-europe-launch]

## Purpose and scope

According to Linux Foundation Europe’s launch announcement, OWF’s aim is to support interoperability for a wide range of wallet use cases, including making payments, proving identity, and storing validated credentials (for example, employment, education, and entitlements).[^lf-europe-launch] The announcement also states that OWF is not intended to publish a wallet, offer credentials, or create new standards, but instead to provide open-source software that others can use to build wallets.[^lf-europe-launch]

## Relationship to digital identity and credential ecosystems

Digital wallets are often discussed as a client-side component in ecosystems that include verifiable credentials and OpenID-based issuance/presentation protocols. In that context, OWF’s focus on reusable wallet components is adjacent to standards work from bodies such as the **W3C** (e.g., Verifiable Credentials data models) and the **OpenID Foundation** (e.g., OpenID for Verifiable Credential Issuance and OpenID for Verifiable Presentations), while remaining distinct from standards development.[^lf-europe-launch]

## Architecture work

OWF community contributors have published a *Universal Wallet Reference Architecture* whitepaper describing a conceptual architecture for a “universal” consumer wallet supporting **identity**, **objects** (such as tokens or tickets), and **money** (payment instruments).[^owf-architecture-whitepaper] The whitepaper describes the document as an OWF deliverable intended to help map capabilities and gaps across OWF projects, and notes that it does not define technical standards.[^owf-architecture-whitepaper]

## See also

- [Verifiable Credentials (W3C)](Verifiable%20Credentials%20(W3C).md)
- [OpenID for Verifiable Credential Issuance (OID4VCI)](OpenID%20for%20Verifiable%20Credential%20Issuance%20(OID4VCI).md)
- [OpenID for Verifiable Presentations (OID4VP)](OpenID%20for%20Verifiable%20Presentations%20(OID4VP).md)

## References

[^lf-europe-launch]: Linux Foundation Europe. *“Linux Foundation Europe Announces Formation of OpenWallet Foundation”* (23 February 2023). https://linuxfoundation.eu/newsroom/linux-foundation-europe-launches-open-wallet (accessed 2026-02-28).

[^owf-architecture-whitepaper]: OpenWallet Foundation Architecture SIG. *“Universal Wallet Reference Architecture Whitepaper”* (working draft; repository document). https://github.com/openwallet-foundation/architecture-sig/blob/main/docs/papers/architecture-whitepaper.md (accessed 2026-02-28).
