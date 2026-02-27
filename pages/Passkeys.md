# Passkeys

A **passkey** is a passwordless authentication credential based on **FIDO** standards. In typical deployments, a passkey lets a user sign in to a website or app by approving an authentication prompt using the same local method used to unlock a device (for example, biometrics or a device PIN), rather than typing a password. https://fidoalliance.org/passkeys/

Passkeys are implemented using the **FIDO2** family of standards, including:

- **Web Authentication (WebAuthn)**: a browser API for creating and using public-key credentials.
- **Client to Authenticator Protocol (CTAP)**: a protocol for communication between a client platform and an authenticator (for example, a roaming authenticator over USB/NFC/BLE).

See: https://fidoalliance.org/specs/fido-v2.2-ps-20250714/fido-client-to-authenticator-protocol-v2.2-ps-20250714.html

## How passkeys work (high level)

Passkeys are based on public-key cryptography:

- A **private key** is held by (or protected by) an authenticator associated with the user.
- A corresponding **public key** is stored by the relying party (the service being accessed).

When authenticating, the user agent and authenticator produce a cryptographic assertion that the relying party can verify, rather than transmitting a reusable secret such as a password. https://support.apple.com/en-us/102195

## Key terms

- **Relying party (RP)**: the website or application that requests authentication.
- **Authenticator**: hardware or software that can create and use the credential key pair (for example, a phone, platform authenticator, or security key).
- **User presence (UP)**: evidence that the user interacted with the authenticator (for example, a user gesture). CTAP defines `up` and `uv` signals for user presence and user verification. https://fidoalliance.org/specs/fido-v2.2-ps-20250714/fido-client-to-authenticator-protocol-v2.2-ps-20250714.html
- **User verification (UV)**: verification of the user by the authenticator (for example, biometrics or a PIN), distinct from simply being present.

## Synced vs device-bound passkeys

FIDO materials commonly distinguish between:

- **Synced passkeys**: passkeys stored in a credential manager and synchronized across a user’s devices (for example, iCloud Keychain or Google Password Manager). https://fidoalliance.org/passkeys/
- **Device-bound passkeys**: passkeys that never leave a single device (or a single authenticator). https://fidoalliance.org/passkeys/

Examples:

- Apple states that passkeys can sync across a user’s devices using iCloud Keychain. https://support.apple.com/en-us/102195
- Google’s developer documentation describes passkeys as encrypted on-device before being synced, and notes that Google Password Manager synchronizes passkeys across Android and Chrome environments. https://developers.google.com/identity/passkeys and https://developers.google.com/identity/passkeys/supported-environments

## Cross-device sign-in (using a nearby phone)

Even when a passkey is not available on the device being used (for example, signing in on a laptop), some ecosystems support **cross-device authentication** using a nearby phone that holds the passkey.

Google documents a QR-code-based flow where a user can sign in on one device using a passkey stored on another nearby device. https://developers.google.com/identity/passkeys/supported-environments

The FIDO Alliance also describes cross-device sign-in as an enhancement to CTAP using Bluetooth Low Energy (BLE) to verify physical proximity. https://fidoalliance.org/passkeys/

## Use in agentic systems

In systems that support autonomous or semi-autonomous agents, passkeys can matter when a user must authenticate to a web service, authorize a payment, or approve sensitive actions.

However, passkey-based authentication is designed around user interaction and/or user verification (UP/UV). That generally means a fully autonomous agent may still need a human-in-the-loop step (or a delegated mechanism explicitly supported by the service) for high-assurance actions.

## See also

- [[Web Authentication (WebAuthn)]]
- [[Secure Payment Confirmation (W3C)]]

## References

- FIDO Alliance. “FIDO Passkeys: Passwordless Authentication”. https://fidoalliance.org/passkeys/
- Apple Support. “About the security of passkeys”. https://support.apple.com/en-us/102195
- Google for Developers. “Passkeys”. https://developers.google.com/identity/passkeys
- Google for Developers. “Passkey support on Android and Chrome”. https://developers.google.com/identity/passkeys/supported-environments
- FIDO Alliance. “Client to Authenticator Protocol (CTAP) v2.2 (Proposed Standard)”. https://fidoalliance.org/specs/fido-v2.2-ps-20250714/fido-client-to-authenticator-protocol-v2.2-ps-20250714.html
