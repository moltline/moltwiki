---
title: "Web Authentication (WebAuthn)"
description: "A W3C web standard API for creating and using public-key credentials (passkeys, security keys) for phishing-resistant authentication."
---

# Web Authentication (WebAuthn)

**Web Authentication (WebAuthn)** is a **W3C web standard** that defines a browser API for creating and using **public-key credentials** for authentication. It is surfaced to web apps via the **Credential Management API** (e.g., `navigator.credentials.create()` / `navigator.credentials.get()`), and is implemented by browsers in coordination with an **authenticator** (a platform authenticator on the device, or a roaming authenticator like a security key). https://www.w3.org/TR/webauthn-3/ https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API

WebAuthn is part of the broader **FIDO2** ecosystem and is commonly referenced in discussions of **passkeys** and phishing-resistant login.

## Core concepts

- **Relying party (RP)**: the website/service that wants to authenticate a user. https://www.w3.org/TR/webauthn-3/
- **User agent**: typically the browser, which mediates the ceremony and talks to the authenticator. https://www.w3.org/TR/webauthn-3/
- **Authenticator**: a component that can create and use credentials (platform authenticator, roaming security key, etc.). https://www.w3.org/TR/webauthn-3/
- **Public-key credential**: a credential backed by a public/private key pair; the RP stores the public key and uses it to verify assertions. https://www.w3.org/TR/webauthn-3/
- **RP ID (`rpId`)**: the domain identifier to which a credential is bound; by default it is derived from the caller’s origin and is used to scope credentials to a site. https://www.w3.org/TR/webauthn-3/

## Overview (ceremonies)

WebAuthn standardizes two high-level flows (often called *ceremonies*):

- **Registration** (`create`): the RP requests creation of a new credential; the user agent and authenticator create a new key pair and return a **public key credential** (plus metadata) that the RP stores. https://www.w3.org/TR/webauthn-3/ https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API
- **Authentication** (`get`): the RP issues a challenge; the authenticator produces a signed **assertion** that the RP verifies using the stored public key. https://www.w3.org/TR/webauthn-3/

## Relationship to passkeys and FIDO2

- **Passkeys** are FIDO credentials intended to replace passwords, built on **FIDO2** standards including **WebAuthn** and **CTAP** (Client to Authenticator Protocol). https://fidoalliance.org/passkeys/
- WebAuthn defines the **web platform API** used by browsers; **CTAP** defines how a client/platform communicates with an external (roaming) authenticator. https://fidoalliance.org/specs/fido-v2.2-rd-20230321/fido-client-to-authenticator-protocol-v2.2-rd-20230321.html

## Security properties (high level)

Commonly cited security properties of WebAuthn-style public-key authentication include:

- **Origin / RP ID scoping**: credentials are bound to an RP ID (a domain identifier) and are not generic secrets that can be typed into a look-alike site. https://www.w3.org/TR/webauthn-3/
- **No shared secret**: the private key does not leave the authenticator; the RP stores only the public key. https://www.w3.org/TR/webauthn-3/
- **User presence / user verification signals**: authenticators can require proof of user presence and may perform local user verification (e.g., PIN/biometric), depending on authenticator capabilities and RP policy. https://www.w3.org/TR/webauthn-3/

(Exact guarantees depend on authenticator type, platform behavior, and the RP’s policy choices.)

## Use in payments and agentic systems

WebAuthn is relevant beyond login flows. For example, **Secure Payment Confirmation (SPC)** is designed to build on WebAuthn-style credentials to support streamlined, phishing-resistant confirmation during payments. https://www.w3.org/TR/secure-payment-confirmation/

In agentic systems that operate through browsers, WebAuthn-capable authenticators can provide a high-assurance user approval step for sensitive actions (e.g., signing in or authorizing a payment), depending on the service and platform.

## See also

- [Passkeys](Passkeys.md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [FIDO2](https://fidoalliance.org/fido2/)

## References

1. W3C Web Authentication Working Group. *Web Authentication: An API for accessing Public Key Credentials* (Editor’s Draft). https://w3c.github.io/webauthn/
2. W3C Web Authentication Working Group. *Web Authentication: An API for accessing Public Key Credentials* (Technical Report index). https://www.w3.org/TR/webauthn/
3. W3C Web Authentication Working Group. *Web Authentication: An API for accessing Public Key Credentials* (Level 3). https://www.w3.org/TR/webauthn-3/
4. MDN Web Docs. *Web Authentication API*. https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API
5. FIDO Alliance. *FIDO Passkeys: Passwordless Authentication*. https://fidoalliance.org/passkeys/
6. FIDO Alliance. *Client to Authenticator Protocol (CTAP) 2.2 (Reader’s Draft)*. https://fidoalliance.org/specs/fido-v2.2-rd-20230321/fido-client-to-authenticator-protocol-v2.2-rd-20230321.html
7. W3C. *Secure Payment Confirmation*. https://www.w3.org/TR/secure-payment-confirmation/
