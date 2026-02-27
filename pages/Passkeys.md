# Passkeys

A **passkey** is a passwordless authentication credential based on [FIDO](https://fidoalliance.org/fido2/) standards. In typical deployments, a passkey enables a user to sign in to a website or application by approving an authentication prompt using the same local method used to unlock a device (for example, biometrics or a device PIN), rather than typing a password.[^fido-passkeys]

Passkeys are commonly implemented using the **FIDO2** family of standards, including the W3C **Web Authentication (WebAuthn)** API for browsers and the FIDO **Client to Authenticator Protocol (CTAP)** for communication with authenticators.[^fido-passkeys][^webauthn]

## Overview

Passkeys are typically based on public-key cryptography:

- A **private key** is held by (or protected by) an authenticator associated with the user.
- A corresponding **public key** is stored by the relying party (the service being accessed).

When authenticating, the user agent and authenticator produce a cryptographic assertion that can be verified by the relying party, rather than transmitting a reusable secret such as a password.[^passkey-central-intro]

## Relationship to WebAuthn and FIDO2

Passkeys are closely associated with the WebAuthn ecosystem:

- The W3C WebAuthn specification defines a browser API for creating and using public key credentials, and it describes registration and authentication "ceremonies" involving a user, a user agent, and an authenticator.[^webauthn]
- FIDO Alliance materials describe passkeys as FIDO credentials intended to replace passwords and reduce susceptibility to phishing and credential stuffing.[^fido-passkeys]

## Single-device and multi-device passkeys

Some sources distinguish between passkeys that are bound to a particular authenticator and passkeys that can be synchronized across a user's devices:

- **Single-device credentials (SDC)** are passkeys bound to a single device or authenticator.
- **Multi-device credentials (MDC)** are passkeys that can be moved and synchronized between devices, enabling sign-in from multiple devices without separately enrolling each one.[^yubico-sdc-mdc]

## Use in agentic systems

In systems that support autonomous or semi-autonomous agents, passkeys can be relevant where a user must authenticate to a web service, authorize a payment, or approve sensitive actions.

For example, an agent operating through a browser automation layer may still rely on WebAuthn-capable authenticators for high-assurance user presence and approval, depending on the service and platform.

## See also

- [[Web Authentication (WebAuthn)]]
- [[Secure Payment Confirmation (W3C)]]

## References

[^fido-passkeys]: FIDO Alliance. "FIDO Passkeys: Passwordless Authentication". https://fidoalliance.org/passkeys/
[^passkey-central-intro]: Passkey Central. "Introduction to Passkeys". https://www.passkeycentral.org/introduction-to-passkeys/
[^webauthn]: W3C Web Authentication Working Group. "Web Authentication: An API for accessing Public Key Credentials" (Editor’s Draft; TR points to https://www.w3.org/TR/webauthn-3/). https://w3c.github.io/webauthn/
[^yubico-sdc-mdc]: Yubico Developers. "Single device vs multi device credentials". https://developers.yubico.com/Passkeys/Passkey_concepts/Single_device_vs_multi_device_credentials.html
