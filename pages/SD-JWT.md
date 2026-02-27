# SD-JWT

**SD-JWT** (Selective Disclosure for JSON Web Tokens) is an Internet Standards Track specification from the Internet Engineering Task Force (IETF) that defines a mechanism for selectively disclosing individual elements of a JSON data structure used as the payload of a JSON Web Signature (JWS). The primary use case described by the specification is selectively disclosing JSON Web Token (JWT) claims while still allowing a verifier to validate the issuer’s signature.[^rfc9901]

SD-JWT is commonly discussed in the context of privacy-preserving digital credentials and verifiable presentations, because it provides a standardized way to reveal only the minimum set of claims needed for a particular interaction.

## Overview

The SD-JWT specification defines a mechanism based on "salted hashes". For any data element that should be selectively disclosable, the issuer does not include the cleartext value in the signed JSON payload; instead, a digest is included. At presentation time, the holder transmits the signed payload along with disclosures containing the cleartext values (and salts) for the claims it chooses to reveal, enabling the verifier to recompute digests and confirm they match values covered by the issuer signature.[^rfc9901]

The specification defines:

- **A data format and processing model** for producing an issuer-signed JWT (a JWS) that includes digests of selectively disclosable claims.[^rfc9901]
- **Disclosures** (separately conveyed values) that can be presented to a verifier to reveal chosen claims.[^rfc9901]
- **Optional key binding**, in which a holder presents a separate **Key Binding JWT** to prove control of a key and bind the presentation to that key (often written as **SD-JWT+KB**).[^rfc9901]

## Publication and status

SD-JWT was published as **RFC 9901** in **November 2025** as an IETF **Proposed Standard**.[^rfc9901-info]

## See also

- [W3C Verifiable Credentials Data Model v2.0](Verifiable%20Credentials%20Data%20Model%20v2.0.md)
- [W3C Verifiable Credentials 2.0](W3C%20Verifiable%20Credentials%202.0.md)

## References

[^rfc9901]: D. Fett; K. Yasuda; B. Campbell. *Selective Disclosure for JSON Web Tokens*. RFC 9901 (Proposed Standard), November 2025. RFC Editor. https://www.rfc-editor.org/rfc/rfc9901
[^rfc9901-info]: RFC Editor. *Information on RFC 9901*. https://www.rfc-editor.org/info/rfc9901
