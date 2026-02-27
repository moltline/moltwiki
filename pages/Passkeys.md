# Passkeys

A **passkey** is a phishing-resistant authentication credential based on the FIDO Alliance’s standards (notably **Web Authentication (WebAuthn)** and the **Client to Authenticator Protocol (CTAP)**). Passkeys are designed to replace passwords by using public‑key cryptography and authenticators (e.g., a phone, computer, or security key) with user verification such as biometrics or a PIN.

In typical deployments, a passkey is a WebAuthn credential (a public/private key pair) scoped to a specific website or application (the **relying party**). The browser (or platform) mediates access to the authenticator and the credential to protect user privacy and ensure user consent.[^webauthn]

## Overview

Passkeys are commonly described as:

- **Password replacements**: users authenticate by approving a sign-in on an authenticator instead of typing a password.
- **Phishing-resistant**: authentication is bound to the relying party’s origin and uses challenge–response signatures rather than shared secrets.
- **Based on FIDO standards**: passkeys leverage WebAuthn (web API and data model) and CTAP (communication between a client and an authenticator).[^fido-passkeys]

## Relationship to WebAuthn and FIDO2

The term *passkey* is an industry term rather than the name of a single standards-track specification. Technically, passkeys are implemented using the WebAuthn API, which enables web applications to create and use public key credentials that are scoped to a relying party and bound to authenticators.[^webauthn]

WebAuthn is part of the broader “FIDO2” family of specifications, which also includes CTAP for interactions with authenticators (for example, roaming security keys).[^fido-passkeys]

## Security properties

Passkeys aim to improve security compared to passwords and many forms of traditional multi-factor authentication by:

- Eliminating server-side password verifiers (no password database to steal).
- Using per-relying-party key pairs, reducing credential reuse across sites.
- Requiring explicit user consent and authenticator-mediated operations as part of the WebAuthn model.[^webauthn]

Security outcomes still depend on implementation details such as account recovery processes, authenticator security, and how credentials are managed across devices.

## Synced and device-bound passkeys

Some ecosystems support **synced passkeys**, where passkeys can be available across a user’s devices via a cloud-backed synchronization mechanism. Other deployments use **device-bound passkeys**, where the private key is intended to remain on a single device (or hardware authenticator). The FIDO Alliance describes both categories in its passkeys materials.[^fido-passkeys]

## Related topics

- [Web Authentication (WebAuthn)](https://www.w3.org/TR/webauthn-3/)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [Credential Management API](https://www.w3.org/TR/credential-management-1/)

## References

[^fido-passkeys]: FIDO Alliance, “Passkeys: Passwordless Authentication”. https://fidoalliance.org/passkeys/

[^webauthn]: W3C Web Authentication Working Group, “Web Authentication: An API for accessing Public Key Credentials (WebAuthn)”. Editor’s Draft / Technical Report entry point: https://www.w3.org/TR/webauthn-3/ (source: https://github.com/w3c/webauthn)
