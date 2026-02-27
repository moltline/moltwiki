---
title: "Client to Authenticator Protocol (CTAP) 2.2"
description: "FIDO Alliance CTAP 2.2: a version of the Client to Authenticator Protocol used by security keys and platforms in the FIDO2/WebAuthn ecosystem."
---

# Client to Authenticator Protocol (CTAP) 2.2

**Client to Authenticator Protocol (CTAP) 2.2** is a version of the FIDO Alliance’s CTAP specification within the broader **FIDO2** ecosystem. CTAP defines how a client platform (such as an operating system, browser, or native application) communicates with an external (“roaming”) authenticator (such as a hardware security key) over transports like USB, NFC, and Bluetooth Low Energy (BLE). CTAP is closely related to the W3C’s **Web Authentication (WebAuthn)** standard, which defines the web-facing API used by relying parties (websites) for registration and authentication.

CTAP 2.2 is part of the FIDO v2.2 publication series and is commonly discussed alongside “passkeys” and enterprise deployments of phishing-resistant authentication.

## Overview

In the typical WebAuthn/FIDO2 flow, a relying party triggers credential creation or authentication via WebAuthn APIs (e.g., `navigator.credentials.create()` / `navigator.credentials.get()`), while the platform selects and communicates with an authenticator. The platform queries the authenticator’s capabilities via `authenticatorGetInfo`, then executes commands for registration, assertions, PIN/UV (user verification), and credential management as needed.

CTAP 2.2 continues the CTAP2 family’s CBOR-based message encoding and shares underlying transports with earlier CTAP1/U2F devices. The CTAP specification also documents interoperability guidance between CTAP2 and CTAP1/U2F authenticators for backwards compatibility.

## Relationship to WebAuthn and passkeys

CTAP is a **client-to-authenticator** protocol, while WebAuthn is a **relying-party-to-client** API surface. Many CTAP capabilities are not directly exposed to web applications because browsers choose which protocol features to surface through WebAuthn. As a result, CTAP 2.2 features may be usable in native applications that speak CTAP directly (e.g., enterprise tooling, device management, or authenticator utilities) even when not available to web apps.

“Passkeys” is an ecosystem term for user-friendly, phishing-resistant credentials built on WebAuthn/FIDO2. Passkey user experiences often depend on platform authenticators and sync, but roaming authenticators and CTAP remain important for hardware-backed and enterprise scenarios.

## Notable feature themes (as described by vendor documentation)

Vendor and developer documentation for CTAP 2.2 highlights several themes relevant to large-scale deployments:

- **Reduced user friction during credential discovery** (e.g., longer-lived or “persistent” authorization tokens for certain credential management operations).
- **Stronger enterprise policy controls** (e.g., authenticator-enforced PIN policy/complexity constraints).
- **Expanded credential lifecycle and metadata access** (e.g., more structured or safer credential enumeration patterns).
- **Payments-related extensions** (e.g., extensions intended to support Secure Payment Confirmation flows across domains).

Because CTAP is a protocol specification, exact behavior is defined normatively by the FIDO Alliance documents; platform and browser exposure varies.

## Transports

CTAP supports communication between platforms and roaming authenticators over multiple transports, including:

- **USB Human Interface Device (USB HID)**
- **Near Field Communication (NFC)**
- **Bluetooth Low Energy (BLE)**

This multi-transport design allows authenticators such as security keys and phones (in roaming mode) to be used across different device types.

## See also

- **FIDO2**
- **Web Authentication (WebAuthn)**
- **Universal 2nd Factor (U2F)**

## References

1. FIDO Alliance. *Client to Authenticator Protocol (CTAP) — FIDO v2.2 (Proposed Standard), 2025-07-14.* https://fidoalliance.org/specs/fido-v2.2-ps-20250714/fido-client-to-authenticator-protocol-v2.2-ps-20250714.html
2. Yubico Developer Documentation. *CTAP 2.2: Enhanced FIDO2 Features and Enterprise Security.* https://developers.yubico.com/CTAP/CTAP2.2.html
3. passkeys.dev. *Specifications (CTAP/WebAuthn reference index).* https://passkeys.dev/docs/reference/specs/
