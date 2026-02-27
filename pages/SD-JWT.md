# SD-JWT

**SD-JWT** (Selective Disclosure for JSON Web Tokens) is an Internet Standards Track specification from the Internet Engineering Task Force (IETF) that defines a mechanism for selectively disclosing individual elements of a JSON data structure carried in a JSON Web Signature (JWS). A primary use case is selectively disclosing JSON Web Token (JWT) claims while allowing a verifier to validate the issuer’s signature.

SD-JWT is commonly discussed in the context of privacy-preserving digital credentials and verifiable presentations, because it provides a standardized way to reveal only the minimum set of claims needed for a particular interaction.

## Overview

The SD-JWT specification defines:

- **A data format and processing model** for producing an issuer-signed JWT (a JWS) that includes digests of selectively disclosable claims.
- **Disclosures** (separately conveyed values) that can be presented to a verifier to reveal chosen claims.
- **Optional key binding**, in which a holder presents a separate **Key Binding JWT** to prove control of a key and bind the presentation to that key (often written as **SD-JWT+KB**).

## Publication and status

SD-JWT was published as **RFC 9901** in **November 2025** as an IETF **Proposed Standard**.

The RFC Editor errata database listed **no errata records** for RFC 9901 at the time of writing.

## See also

- [W3C Verifiable Credentials Data Model v2.0](Verifiable%20Credentials%20Data%20Model%20v2.0.md)
- [W3C Verifiable Credentials 2.0](W3C%20Verifiable%20Credentials%202.0.md)

## References

- D. Fett; K. Yasuda; B. Campbell. *Selective Disclosure for JSON Web Tokens*. RFC 9901 (Proposed Standard), November 2025. https://www.rfc-editor.org/rfc/rfc9901
- RFC Editor. *Information on RFC 9901*. https://www.rfc-editor.org/info/rfc9901
- RFC Editor. *RFC Errata Report: RFC 9901*. https://www.rfc-editor.org/errata_search.php?rfc=9901
