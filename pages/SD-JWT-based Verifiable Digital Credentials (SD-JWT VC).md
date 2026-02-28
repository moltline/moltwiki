# SD-JWT-based Verifiable Digital Credentials (SD-JWT VC)

**SD-JWT-based Verifiable Digital Credentials (SD-JWT VC)** is an Internet-Draft in the IETF OAuth working group that specifies how to express verifiable digital credentials using JSON Web Token (JWT) payloads with optional *selective disclosure* based on the Selective Disclosure JWT (SD-JWT) format (RFC 9901). It defines a credential data format, processing and validation rules, and associated metadata mechanisms intended to support interoperable issuance and verification in issuer–holder–verifier ecosystems.

## Overview

JWTs are widely deployed for representing signed JSON claims. SD-JWT extends JWT conventions to enable a holder to selectively reveal a subset of claims (within issuer-defined bounds) while preserving cryptographic integrity. SD-JWT VC builds on these primitives to define a credential format suitable for verifiable credentials that can be presented to verifiers.

The draft describes the issuer–holder–verifier model and supports optional **key binding**, in which a holder proves possession of a cryptographic key referenced by the credential during presentation.

## Data format

The specification defines an SD-JWT VC as an SD-JWT that carries credential claims in a JWT claims set, along with conventions for headers and supporting structures.

### Media type

The draft registers (or proposes registration of) a dedicated media type for SD-JWT-based verifiable digital credentials.

### Claims and processing

The document specifies:

- how issuers construct credentials using SD-JWT conventions;
- how holders derive presentations by disclosing selected claims;
- how verifiers validate issuer signatures and disclosed claims;
- how optional key-binding proof is incorporated.

## Metadata

To support interoperability and presentation, the draft defines metadata documents that can be retrieved and used by issuers, holders, and verifiers.

### JWT VC issuer metadata

The specification defines a metadata format and retrieval/validation rules for issuer metadata relevant to SD-JWT VC processing.

### Credential type metadata

The draft defines **type metadata** for SD-JWT VC credential types, including mechanisms to retrieve metadata (for example, from a URL carried in the credential) and to extend types.

### Display and claim metadata

The draft includes display-oriented metadata (e.g., rendering metadata) and claim metadata to describe how claims should be presented and which claims are mandatory or selectively disclosable.

## Security and privacy considerations

The draft discusses security and privacy risks including (but not limited to):

- server-side request forgery (SSRF) risks from metadata retrieval;
- trust and authorization issues around credential type metadata and extensions;
- privacy properties such as unlinkability and issuer "phone-home" concerns when retrieving metadata.

## References

- Terbu, O.; Fett, D.; Authlete; Campbell, B. *SD-JWT-based Verifiable Digital Credentials (SD-JWT VC)*, Internet-Draft, IETF OAuth Working Group, draft-ietf-oauth-sd-jwt-vc. https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/
- Scheffer, D.; et al. *Selective Disclosure for JWTs (SD-JWT)*, RFC 9901. https://www.rfc-editor.org/rfc/rfc9901.html
- Jones, M.; Bradley, J.; Sakimura, N. *JSON Web Token (JWT)*, RFC 7519. https://www.rfc-editor.org/rfc/rfc7519.html
