# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF Standards Track mechanism for creating and verifying digital signatures (or message authentication codes) over selected components of an HTTP message. The goal is to allow signing in situations where the full message might not be known to the signer, and where intermediaries may transform messages before verification.

RFC 9421 defines:

- A model for selecting HTTP message components (fields and derived components) to cover by a signature.
- How to construct a *signature base* from those components.
- How to carry signatures in HTTP using the `Signature-Input` and `Signature` HTTP fields.
- A way to request signatures in later messages in an HTTP exchange via the `Accept-Signature` field.

## Background and motivation

HTTP already commonly relies on TLS for channel security, but there are cases where applications need cryptographic protection that is bound to specific message components (e.g., for auditability, non-repudiation-like properties in an application context, or end-to-end integrity across intermediaries). RFC 9421 is designed to support use cases where:

- The signer does not have access to the entire HTTP message body or all headers.
- The message may be modified in transit in ways that are acceptable if the covered components remain unchanged.

## Core concepts

### Covered components

A signature covers a list of *message components*, which can include:

- **HTTP fields** (headers and, where applicable, trailers).
- **Derived components** (values derived from the request/response context, such as method, target URI, authority, path, query, and status code).

The choice of covered components is an application decision; RFC 9421 describes how to represent and serialize them so that signers and verifiers can compute the same signature base.

### Signature base

The *signature base* is a canonicalized representation of the selected components and associated parameters. The signature is computed over this base.

### On-the-wire HTTP fields

RFC 9421 specifies two primary HTTP fields for conveying signatures:

- `Signature-Input`: conveys the signature parameters and the covered component list.
- `Signature`: conveys the signature value(s).

It also defines `Accept-Signature` to express a preference/request that a peer apply a signature to a subsequent message in an exchange.

## Algorithms and registries

RFC 9421 defines a set of signature algorithms and establishes IANA registries for HTTP message signature algorithms, metadata parameters, derived component names, and component parameters.

## Relationship to other mechanisms

HTTP Message Signatures are distinct from:

- **TLS**: which provides transport security but does not, by itself, produce an application-verifiable signature over chosen HTTP components.
- **JWS (JSON Web Signature)**: which signs JSON (or other payloads) in a JWS structure, rather than signing selected HTTP message components.

RFC 9421 does allow use of JWS algorithms as signature algorithms within the HTTP Message Signatures framework.

## See also

- [[DPoP]] (often used to bind tokens to a proof-of-possession key at the HTTP layer)
- [[OAuth 2.0]]
- [[Web Authentication (WebAuthn)]]

## References

- IETF. *RFC 9421: HTTP Message Signatures*. February 2024. https://www.rfc-editor.org/rfc/rfc9421
- IETF Datatracker. *RFC 9421: HTTP Message Signatures*. https://datatracker.ietf.org/doc/rfc9421/
