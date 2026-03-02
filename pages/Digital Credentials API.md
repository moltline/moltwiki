# Digital Credentials API

The **Digital Credentials API** is a proposed web platform API that enables a browser (user agent) to mediate the **presentation** and **issuance** of digital credentials (for example, mobile driver’s licenses) stored in wallet applications. The proposal is being developed in the W3C Federated Identity community (W3C FedID), and has been implemented in Chrome as an origin trial on Android.

## Overview

The API is designed to let a website (a *relying party*) request specific, verifiable information from a user’s digital wallet in a way that:

- requires explicit user interaction (“transient activation”) for each request;
- allows the browser or platform to provide wallet/credential selection UX;
- is protocol- and format-agnostic, with registries/profiles used to promote interoperability.

In Chrome’s implementation, the request is routed through the operating system to installed wallet applications; the user selects a wallet (and potentially a credential), authenticates locally, and the wallet returns a response that the relying party can verify (for example by checking a cryptographic signature).

## Relationship to other standards

The Digital Credentials API is related to several identity and credential standards and ecosystems:

- **Credential Management API**: the proposal builds on the browser’s credential-management concepts and APIs.
- **OpenID for Verifiable Presentations (OpenID4VP)**: one of the primary exchange protocols profiled for use with the API in early implementations.
- **W3C Verifiable Credentials (VC)** and other credential formats: the API aims to be format-agnostic.

## API surface (high level)

The proposal defines a “digital” credential type for credential requests and creation. A site initiates a presentation request by calling a browser API and specifying one or more “requests”, each pairing:

- a **protocol identifier** (e.g., `openid4vp`), and
- a **request payload** (protocol-specific data).

Implementations are expected to require user activation, and to avoid leaking information about a user’s installed wallets or credentials unless the user consents.

## Browser support

Chrome introduced an **origin trial** for the Digital Credentials API starting in **Chrome 128**, initially supporting Chrome on Android to request credentials from wallet apps on the same device. Chrome’s documentation describes the API as intended to make wallet interactions “more secure, resistant to abuse and easier to use” compared to ad-hoc deep-linking approaches.

## See also

- [Credential Management API](https://developer.mozilla.org/docs/Web/API/Credential_Management_API)
- [OpenID for Verifiable Presentations (OID4VP)](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)
- [Verifiable Credentials (W3C)](https://www.w3.org/TR/vc-data-model-2.0/)

## References

- W3C FedID. *Digital Credentials* (unofficial proposal). https://w3c-fedid.github.io/digital-credentials/
- Chrome for Developers. *Introducing the Digital Credentials API origin trial* (Sep 4, 2024). https://developer.chrome.com/blog/digital-credentials-api-origin-trial
