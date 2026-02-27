# Web Authentication (WebAuthn) (W3C)

**Web Authentication (WebAuthn)** is a W3C web standard that defines a browser API for creating and using **public key credentials** to authenticate users. WebAuthn is a core component of the broader **FIDO2** ecosystem and is commonly used to implement **passkeys** and other phishing-resistant sign-in methods.

WebAuthn is exposed to web applications primarily through the `navigator.credentials.create()` and `navigator.credentials.get()` methods (as part of the Credential Management model), with user agents mediating access to authenticators.

**Type:** Web standard (W3C Technical Report)

## Overview

WebAuthn enables a website (the **Relying Party**, or RP) to register a credential bound to an authenticator (for example, a platform authenticator on a phone or laptop, or a roaming security key). Later, the RP can request an assertion proving that the user controls that credential.

At a high level:

1. **Registration**: the RP asks the browser to create a new credential. The authenticator generates a new key pair and returns a public key (and related metadata) to the RP.
2. **Authentication**: the RP sends a challenge and asks the browser to obtain a signed assertion from the authenticator, which the RP verifies using the stored public key.

The user agent and authenticator are intended to ensure that operations occur with appropriate **user consent** and to limit tracking and privacy risks.

## Key concepts

- **Public key credential**: a credential based on asymmetric cryptography, scoped to an RP.
- **Relying Party (RP)**: the website or service requesting authentication.
- **Authenticator**: hardware or software that stores private keys and performs cryptographic operations (e.g., platform authenticator, security key).
- **Attestation**: optional evidence about authenticator characteristics provided during credential creation.
- **Assertion**: the signed response returned during authentication.

## Relationship to other standards and systems

- **Passkeys**: Passkeys are typically implemented using WebAuthn and platform authenticator capabilities, often combined with syncing and platform UX.
- **FIDO2 / CTAP**: WebAuthn specifies the web API; the Client-to-Authenticator Protocol (CTAP) defines how clients communicate with roaming authenticators.
- **Secure Payment Confirmation (SPC)**: SPC builds payment-specific capabilities on top of WebAuthn, including transaction confirmation UX and signed transaction details.

## Security and privacy considerations

WebAuthn is designed to support phishing-resistant authentication by binding credentials to an RP and requiring a browser-mediated ceremony. The specification also describes how user agents should mediate access to authenticators to preserve user privacy.

## See also

- [Passkeys](./Passkeys.md)
- [Secure Payment Confirmation (W3C)](./Secure%20Payment%20Confirmation%20(W3C).md)

## References

1. W3C, *Web Authentication: An API for accessing Public Key Credentials* (Level 3), Technical Report.
   https://www.w3.org/TR/webauthn-3/
2. W3C WebAuthn Working Group, *webauthn* (specification source repository).
   https://github.com/w3c/webauthn
