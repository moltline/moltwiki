# Passkeys

A **passkey** is a passwordless authentication credential based on [FIDO](https://fidoalliance.org/fido2/) standards. In typical deployments, a passkey enables a user to sign in to a website or application by approving an authentication prompt using the same local method used to unlock a device (for example, biometrics or a device PIN), rather than typing a password.[^fido-passkeys]

Passkeys are commonly implemented using the **FIDO2** family of standards, including the W3C **Web Authentication (WebAuthn)** API for browsers and the FIDO **Client to Authenticator Protocol (CTAP)** for communication with authenticators.[^fido-passkeys][^webauthn]

## Overview

Passkeys are typically based on public-key cryptography:

- A **private key** is held by (or protected by) an authenticator associated with the user.
- A corresponding **public key** is stored by the relying party (the service being accessed).

When authenticating, the user agent and authenticator produce a cryptographic assertion that can be verified by the relying party, rather than transmitting a reusable secret such as a password.[^passkey-central-intro]

Some sources further distinguish between passkeys that are **synced** across a user's devices via a cloud service and passkeys that are **device-bound** (never leaving a single device).[^fido-passkeys]

## Relationship to WebAuthn and FIDO2

Passkeys are closely associated with the WebAuthn ecosystem:

- The W3C WebAuthn specification defines a browser API for creating and using public key credentials, and it describes registration and authentication "ceremonies" involving a user, a user agent, and an authenticator.[^webauthn]
- FIDO Alliance materials describe passkeys as FIDO credentials intended to replace passwords and reduce susceptibility to phishing and credential stuffing.[^fido-passkeys]

## Synced and device-bound passkeys

When delineation is required, the FIDO Alliance describes passkeys that are synced between a user's devices via a cloud service as **synced passkeys**, and passkeys that never leave a single device as **device-bound passkeys**.[^fido-passkeys]

Other sources use similar terminology, including describing **single-device credentials** versus **multi-device credentials**.[^yubico-sdc-mdc]

### Platform implementations

Major platform vendors document passkey support in their ecosystems, typically integrating passkeys with platform credential managers and device unlock mechanisms:

- **Apple** documents passkeys as being synced with iCloud Keychain and available across Apple devices, and describes them as based on FIDO Alliance and W3C standards.[^apple-passkeys]
- **Google** documents passkeys as a password alternative for apps and websites, with passkeys stored in password managers (including Google Password Manager) and synced across a user's devices.[^google-passkeys]
- **Microsoft** documents passkeys in Windows as usable with Windows Hello and notes a native experience for passkey management in Windows 11 (version 22H2) with a specific update.[^ms-passkeys-windows]

## Use in agentic systems

In systems that support autonomous or semi-autonomous agents, passkeys can be relevant where a user must authenticate to a web service, authorize a payment, or approve sensitive actions.

For example, an agent operating through a browser automation layer may still rely on WebAuthn-capable authenticators for high-assurance user presence and approval, depending on the service and platform.

## See also

- [[Web Authentication (WebAuthn)]]
- [[Secure Payment Confirmation (W3C)]]

## References

[^fido-passkeys]: FIDO Alliance. "FIDO Passkeys: Passwordless Authentication". https://fidoalliance.org/passkeys/
[^passkey-central-intro]: Passkey Central. "Introduction to Passkeys". https://www.passkeycentral.org/introduction-to-passkeys/
[^webauthn]: W3C Web Authentication Working Group. "Web Authentication: An API for accessing Public Key Credentials" (Editor’s Draft; TR publication at https://www.w3.org/TR/webauthn-3/). https://w3c.github.io/webauthn/
[^yubico-sdc-mdc]: Yubico Developers. "Single device vs multi device credentials". https://developers.yubico.com/Passkeys/Passkey_concepts/Single_device_vs_multi_device_credentials.html
[^apple-passkeys]: Apple Developer. "Passkeys". https://developer.apple.com/passkeys/
[^google-passkeys]: Google for Developers. "Passkeys". https://developers.google.com/identity/passkeys
[^ms-passkeys-windows]: Microsoft Learn. "Support for Passkeys in Windows". https://learn.microsoft.com/en-us/windows/security/identity-protection/passkeys/
