# Client to Authenticator Protocol (CTAP)

The **Client to Authenticator Protocol (CTAP)** is a FIDO Alliance protocol for communication between a **client** (for example, a platform or browser) and a **roaming authenticator** (for example, a security key or smartphone used as an authenticator). CTAP is part of the broader **FIDO2** family and is closely related to the W3C **Web Authentication (WebAuthn)** specification.[^ctap]

CTAP is used alongside WebAuthn in end-to-end authentication flows: a relying party (website or native app) invokes WebAuthn APIs on the client platform, and the platform uses CTAP over a transport (e.g., USB, NFC, BLE) to talk to an authenticator.[^ctap]

## Relationship to WebAuthn

FIDO2 is commonly described as having two standardized components:

- **WebAuthn**: the web-facing API and data model used by relying parties (websites) via the browser.
- **CTAP**: the protocol used by clients/platforms to communicate with authenticators (especially roaming authenticators such as security keys).[^yubico-ctap]

In practice, most web developers interact with WebAuthn and do not implement CTAP directly; CTAP is typically implemented by operating systems, browsers, authenticator vendors, and libraries.[^yubico-ctap]

## Protocol versions

The CTAP specification refers to two protocol versions:[^ctap]

- **CTAP1 / U2F**: based on the U2F raw message formats; often described as APDU-like binary messages.
- **CTAP2**: uses CBOR-encoded messages and supports a wider set of capabilities.

The CTAP specification notes that CTAP1 and CTAP2 share common underlying transports such as USB HID, NFC, and BLE.[^ctap]

## Transports

CTAP defines bindings for communicating with roaming authenticators over multiple transports, including:

- **USB Human Interface Device (USB HID)**
- **Near Field Communication (NFC)**
- **Bluetooth Low Energy (BLE)**

These transports are referenced in the CTAP specification as shared by CTAP1 and CTAP2.[^ctap]

## Conceptual flow (high level)

A simplified flow, as described in the CTAP protocol overview, is:

1. A relying party initiates registration or authentication (for websites, via `navigator.credentials.create()` or `navigator.credentials.get()`; for native apps, via platform equivalents).[^ctap]
2. The platform selects an appropriate authenticator.
3. The platform queries authenticator capabilities (e.g., using an *authenticatorGetInfo* command).
4. The platform invokes further authenticator commands depending on the requested operation and authenticator capabilities.[^ctap]

## Related topics

- [Passkeys](Passkeys.md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [Payment Request API](Payment%20Request%20API.md)
- [Web Authentication (WebAuthn)](https://www.w3.org/TR/webauthn-3/)

## References

[^ctap]: FIDO Alliance, “Client to Authenticator Protocol (CTAP) 2.2 (Proposed Standard)”. https://fidoalliance.org/specs/fido-v2.2-ps-20250714/fido-client-to-authenticator-protocol-v2.2-ps-20250714.html

[^yubico-ctap]: Yubico, “Client To Authenticator Protocol (CTAP) – FIDO2 Developer Guide”. https://developers.yubico.com/CTAP/
