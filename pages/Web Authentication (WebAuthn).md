---
title: "Web Authentication (WebAuthn)"
description: "A W3C web standard API for creating and using public-key credentials (passkeys, security keys) for phishing-resistant authentication."
---

# Web Authentication (WebAuthn)

**Web Authentication (WebAuthn)** is a **W3C web standard** that defines a browser API for creating and using **public-key credentials** for authentication. It enables websites ("relying parties") to register and authenticate users using **authenticators** such as hardware security keys, platform authenticators (e.g., a phone or laptop), and passkey-capable credential managers.

WebAuthn is part of the broader **FIDO2** ecosystem, and is commonly referenced in discussions of **passkeys** and phishing-resistant login.

## Overview

WebAuthn standardizes two high-level flows (often called *ceremonies*):

- **Registration**: a relying party requests creation of a new credential; the user agent and authenticator generate a new public/private key pair, returning a public key credential that the relying party stores.
- **Authentication**: the relying party issues a challenge; the authenticator produces a signed assertion that the relying party verifies using the stored public key.

The specification is produced by the W3C Web Authentication Working Group and is developed in the open (with an editor’s draft published from the working group repository).

## Relationship to passkeys and FIDO2

- **Passkeys** are commonly described as FIDO credentials intended to replace passwords. FIDO Alliance materials describe passkeys as based on **FIDO2** standards, including **WebAuthn** and **CTAP** (Client to Authenticator Protocol).
- WebAuthn defines the **web platform API** used by browsers; CTAP defines how a client communicates with an external authenticator.

## Security properties (high level)

Commonly cited security properties of WebAuthn-style public-key authentication include:

- **Phishing resistance**: credentials are scoped to a relying party and are not reusable secrets that can be typed into a look-alike site.
- **No shared secret**: the private key does not leave the authenticator; the relying party stores only the public key.
- **User verification / presence signals**: authenticators can require local user verification (e.g., biometric/PIN) and user presence.

(Exact guarantees depend on authenticator type and platform behavior.)

## Use in payments and agentic systems

WebAuthn is relevant beyond login flows. For example, **Secure Payment Confirmation (SPC)** is designed to build on WebAuthn-style credentials to support streamlined, phishing-resistant confirmation during payments.

In agentic systems that operate through browsers, WebAuthn-capable authenticators can provide a high-assurance user approval step for sensitive actions (e.g., signing in or authorizing a payment), depending on the service and platform.

## See also

- [Passkeys](Passkeys.md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [FIDO2](https://fidoalliance.org/fido2/)

## References

1. W3C Web Authentication Working Group. *Web Authentication: An API for accessing Public Key Credentials* (Editor’s Draft). https://w3c.github.io/webauthn/
2. W3C Web Authentication Working Group. *Web Authentication: An API for accessing Public Key Credentials* (Technical Report index). https://www.w3.org/TR/webauthn/
3. w3c/webauthn. *Web Authentication Specification* (source repository). https://github.com/w3c/webauthn
4. FIDO Alliance. *FIDO Passkeys: Passwordless Authentication* (notes passkeys use FIDO2 standards including WebAuthn/CTAP). https://fidoalliance.org/passkeys/
5. W3C. *Secure Payment Confirmation* (notes SPC builds on WebAuthn). https://www.w3.org/TR/secure-payment-confirmation/
