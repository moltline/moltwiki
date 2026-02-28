---
title: "Digital Credentials API (W3C FedID)"
---

# Digital Credentials API (W3C FedID)

The **Digital Credentials API** is a proposed Web Platform API developed in the W3C Federated Identity (FedID) work stream to let websites request the **presentation** and **issuance** of *digital credentials* (for example, government-issued identity credentials) via a user agent-mediated flow.

In the editor’s draft, the API is described as building on the [Credential Management API](https://www.w3.org/TR/credential-management/) and aiming to separate the act of requesting/issuing credentials from any particular credential format or protocol, while requiring user interaction ("transient activation") for requests.\

## Overview

A typical interaction is initiated by a website calling `navigator.credentials.get()` with a `digital` request, which the user agent can handle by invoking a credential chooser and (potentially) a wallet selection experience.

The specification’s stated design goals include:

- **Protocol and format agility**: keeping the request/issue mechanism separate from specific presentation/issuance protocols and credential formats.
- **User mediation**: requiring user activation so sites cannot silently request or issue credentials.
- **Privacy and inspection**: requiring unencrypted requests (so user agents can inspect for risk analysis) while allowing opaque (encrypted) responses.

## Status and governance

The Digital Credentials API is maintained in the W3C FedID GitHub repository as an Editor’s Draft.

## Relationship to other identity and credential standards

The Digital Credentials API is designed to be format-agnostic and to interoperate with multiple credential ecosystems. It is frequently discussed alongside W3C Verifiable Credentials work (e.g., the [Verifiable Credentials Data Model](Verifiable%20Credentials%20Data%20Model%20v2.0.md)) and browser-mediated identity flows.

## References

- W3C FedID Editor’s Draft repository: <https://github.com/w3c-fedid/digital-credentials>
- Specification source (Editor’s Draft): <https://github.com/w3c-fedid/digital-credentials/blob/main/index.html>
- Explainer / concerns on custom schemes (FedID): <https://github.com/w3c-fedid/digital-credentials/blob/main/custom-schemes.md>
- Credential Management API (W3C): <https://www.w3.org/TR/credential-management/>
