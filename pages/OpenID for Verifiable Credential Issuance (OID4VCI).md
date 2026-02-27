# OpenID for Verifiable Credential Issuance (OID4VCI)

**OpenID for Verifiable Credential Issuance** (often abbreviated **OID4VCI**) is an OpenID Foundation specification that defines an OAuth 2.0–protected API for issuing **verifiable credentials** to a wallet or other client.

The specification is part of the OpenID Foundation’s work on “digital credentials protocols” and is commonly discussed alongside related OpenID4VC* specifications such as OpenID for Verifiable Presentations (OID4VP).

## Overview

OID4VCI specifies how a **Credential Issuer** can provide one or more credentials to a client using standardized endpoints and request/response formats. The protocol is designed to reuse widely deployed web standards (notably OAuth 2.0 and OpenID Connect ecosystem conventions) while supporting multiple credential formats.

The OID4VCI specification defines, among other elements:

- A **credential offer** mechanism, including ways to transmit an offer by value or by reference (URI).
- Use of OAuth 2.0 authorization flows (including an **authorization code** flow and a **pre-authorized code** flow) to obtain the authorization needed for issuance.
- A **credential endpoint** where the client requests issuance and receives the issued credential.
- Optional endpoints and behaviors such as **nonce** handling, **deferred** issuance, and **notification**.

## Credential formats

OID4VCI is designed to support issuance of credentials in different formats. The specification includes profiles and references for multiple credential families, including W3C Verifiable Credentials and other formats used in digital credential ecosystems.

## Relationship to other standards

OID4VCI is defined as an OpenID Foundation specification and builds on OAuth 2.0 concepts and endpoints. It is frequently paired with:

- **OpenID for Verifiable Presentations (OID4VP)**, which defines mechanisms for requesting and presenting credentials.
- Broader security guidance for OAuth 2.0 deployments, referenced in the specification’s security considerations.

## Standardization status

OpenID for Verifiable Credential Issuance 1.0 has been published by the OpenID Foundation as a specification, with the Foundation also announcing approval of a “Final Specification” version for implementers.

## References

1. OpenID Foundation. *OpenID for Verifiable Credential Issuance 1.0* (specification). https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html
2. OpenID Foundation. *OpenID for Verifiable Credential Issuance 1.0 Final Specification Approved* (announcement). https://openid.net/openid-for-verifiable-credential-issuance-1-final-specification-approved/
3. OpenID Foundation. *OpenID for Verifiable Presentations 1.0* (specification). https://openid.net/specs/openid-4-verifiable-presentations-1_0.html
