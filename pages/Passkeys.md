# Passkeys

A **passkey** is a passwordless authentication credential based on [FIDO](https://fidoalliance.org/fido2/) standards. In typical deployments, a passkey enables a user to sign in to a website or application by approving an authentication prompt using the same local method used to unlock a device (for example, biometrics or a device PIN), rather than typing a password.[^fido-passkeys]

Passkeys are commonly implemented using the **FIDO2** family of standards, including the W3C **Web Authentication (WebAuthn)** API for browsers and the FIDO **Client to Authenticator Protocol (CTAP)** for communication with authenticators.[^fido-passkeys][^webauthn]

## Overview

Passkeys are typically based on public-key cryptography:

- A **private key** is held by (or protected by) an authenticator associated with the user.
- A corresponding **public key** is stored by the relying party (the service being accessed).

When authenticating, the user agent and authenticator produce a cryptographic assertion that can be verified by the relying party, rather than transmitting a reusable secret such as a password.[^passkey-central-intro]

## Relationship to WebAuthn, CTAP, and FIDO2

Passkeys are commonly implemented using the FIDO2 ecosystem, which combines:

- **WebAuthn** (a W3C specification) for browser and platform APIs that create and use public key credentials.[^webauthn]
- **CTAP** (Client to Authenticator Protocol, published by the FIDO Alliance) for communication between a client platform and an authenticator, including external authenticators such as security keys over transports like USB, NFC, or Bluetooth.[^fido-specs][^ctap]

FIDO Alliance materials describe passkeys as a password replacement that is phishing-resistant by design, and emphasize that passkeys are cryptographic credentials tied to a user account on a website or application.[^fido-passkeys]

## Single-device and multi-device passkeys

Some sources distinguish between passkeys that are bound to a particular authenticator and passkeys that can be synchronized across a user's devices:

- **Single-device credentials (SDC)** are passkeys bound to a single device, meaning the credential can only be validated using the device that created it.[^yubico-sdc-mdc]
- **Multi-device credentials (MDC)** are passkeys that can be moved and synchronized between devices, enabling sign-in from multiple devices without separately enrolling each one.[^yubico-sdc-mdc]

## Use in agentic systems

In systems that support autonomous or semi-autonomous agents, passkeys can be relevant where a user must authenticate to a web service, authorize a payment, or approve sensitive actions.

For example, an agent operating through a browser automation layer may still rely on WebAuthn-capable authenticators for high-assurance user presence and approval, depending on the service and platform.

## See also

- [[Web Authentication (WebAuthn)]]
- [[Secure Payment Confirmation (W3C)]]

## References

[^fido-passkeys]: FIDO Alliance. "FIDO Passkeys: Passwordless Authentication". https://fidoalliance.org/passkeys/
[^fido-specs]: FIDO Alliance. "FIDO User Authentication Specifications". https://fidoalliance.org/specifications/
[^ctap]: FIDO Alliance. "Client to Authenticator Protocol (CTAP)" (CTAP 2.1, errata 2022-06-21). https://fidoalliance.org/specs/fido-v2.1-ps-20210615/fido-client-to-authenticator-protocol-v2.1-ps-errata-20220621.html
[^passkey-central-intro]: Passkey Central. "Introduction to Passkeys". https://www.passkeycentral.org/introduction-to-passkeys/
[^webauthn]: W3C Web Authentication Working Group. "Web Authentication: An API for accessing Public Key Credentials" (Editor’s Draft). https://w3c.github.io/webauthn/
[^yubico-sdc-mdc]: Yubico Developers. "Single device vs multi device credentials". https://developers.yubico.com/Passkeys/Passkey_concepts/Single_device_vs_multi_device_credentials.html
