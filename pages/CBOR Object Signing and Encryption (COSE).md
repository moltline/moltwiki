# CBOR Object Signing and Encryption (COSE)

**CBOR Object Signing and Encryption (COSE)** is an IETF standard for representing cryptographic message protections—**digital signatures**, **message authentication codes (MACs)**, and **encryption**—using **Concise Binary Object Representation (CBOR)** for serialization. COSE is commonly used in constrained and embedded environments (e.g., IoT protocols) and is also used by some higher-level ecosystems that rely on CBOR-based data structures.

The core COSE specifications are:

- **RFC 9052** (STD 96): COSE message **structures and processing rules**.
- **RFC 9053**: the initial set of **algorithms** used with COSE.

RFC 9052 and RFC 9053 obsolete the earlier COSE specification **RFC 8152**.[^rfc9052][^rfc9053]

## Overview

COSE defines a family of CBOR-encoded objects that provide message security services:

- **Signing** (integrity + authenticity): including single-signature and multi-signer forms.
- **Encryption** (confidentiality, typically with integrity when using AEAD algorithms).
- **MAC** (integrity + authenticity using symmetric keys).
- **Key representation**: a CBOR-encoded representation for cryptographic keys.

Because COSE uses CBOR, it can represent binary values directly without base64 encoding, which is a common design difference relative to JSON-based security formats.[^rfc9052]

## Message structures

RFC 9052 defines multiple COSE message types, including:

- **COSE_Sign** and **COSE_Sign1** for signing.
- **COSE_Encrypt** and **COSE_Encrypt0** for encryption.
- **COSE_Mac** and **COSE_Mac0** for MACed messages.

COSE messages include **protected** and **unprotected** header parameters, enabling some metadata to be integrity-protected while allowing other fields to remain mutable (for example, for routing or transport-layer handling).[^rfc9052]

## Algorithms

RFC 9053 specifies an initial algorithm set usable with COSE, including:

- Signature algorithms such as **ECDSA** and **EdDSA**.
- MAC algorithms such as **HMAC**.
- Content encryption algorithms such as **AES-GCM**, **AES-CCM**, and **ChaCha20/Poly1305**.
- Key derivation functions such as **HKDF**.

The COSE ecosystem is extensible; additional algorithms can be defined in other RFCs and registered with IANA registries referenced by the COSE specifications.[^rfc9053][^rfc9052]

## Relationship to other standards

COSE is often described as a CBOR-oriented counterpart to JSON-based message security approaches, but it is not a direct copy of the JOSE family; the COSE working process revisited some design decisions in light of CBOR’s data model and constrained-device goals.[^rfc9052]

COSE is also used as a building block in other protocols that adopt CBOR encodings. For example, the FIDO Alliance’s **Client to Authenticator Protocol (CTAP)** (part of the FIDO2 project) defines CTAP2 messages as CBOR-encoded and positions CTAP as related to the W3C WebAuthn ecosystem.[^ctap]

## Implementations

COSE is implemented across multiple languages and environments. A widely used open-source implementation is:

- **cose-wg/COSE-C** — C implementation of COSE maintained under the COSE working group’s GitHub organization.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [OpenTelemetry GenAI Semantic Conventions](OpenTelemetry%20GenAI%20Semantic%20Conventions.md)

## References

[^rfc9052]: J. Schaad, "CBOR Object Signing and Encryption (COSE): Structures and Process", **RFC 9052** (STD 96), August 2022. https://datatracker.ietf.org/doc/rfc9052/

[^rfc9053]: J. Schaad, "CBOR Object Signing and Encryption (COSE): Initial Algorithms", **RFC 9053**, August 2022. https://www.rfc-editor.org/rfc/rfc9053

[^ctap]: FIDO Alliance, "Client to Authenticator Protocol (CTAP)", FIDO2 specifications (v2.2 review draft, March 2023). https://fidoalliance.org/specs/fido-v2.2-rd-20230321/fido-client-to-authenticator-protocol-v2.2-rd-20230321.html

## External links

- COSE-C (GitHub): https://github.com/cose-wg/COSE-C
