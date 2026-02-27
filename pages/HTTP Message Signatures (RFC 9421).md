# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF Standards Track mechanism for creating and verifying digital signatures (or message authentication codes) over selected components of an HTTP message. It is designed for cases where the signer might not know the full on-the-wire message (e.g., due to frameworks/proxies) and where intermediaries may perform allowed HTTP transformations, while still enabling verification of the *covered* components. [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)

RFC 9421 defines:

- A model for selecting HTTP message components (fields and derived components) to cover by a signature.
- How to construct a *signature base* from those components.
- How to carry signatures in HTTP using the `Signature-Input` and `Signature` HTTP fields.
- A way to request signatures in later messages in an HTTP exchange via the `Accept-Signature` field. [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)

## Background and motivation

TLS provides integrity/authenticity only within a single TLS connection. In deployments with TLS-terminating gateways, inspection appliances, or multi-hop TLS, applications may want end-to-end protection bound to application-relevant HTTP components. RFC 9421 provides a *detached* signing mechanism over selected components with strict canonicalization so signatures can survive many permitted transformations. [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)

## Core concepts

### Covered components

A signature covers an ordered list of *message components*, including:

- **HTTP fields** (headers and, where applicable, trailers). [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)
- **Derived components** (values derived from the request/response context). RFC 9421 defines a registry of derived component names such as:
  - `@method`, `@authority`, `@scheme`, `@target-uri`, `@request-target`, `@path`, `@query`, `@query-param` (request)
  - `@status` (response)
  - `@signature-params` (reserved for the signature parameters line in the signature base)

  See the IANA **HTTP Signature Derived Component Names** registry. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

The choice of covered components is an application decision: verifiers can only rely on properties that are actually covered (and must ensure their own requirements, e.g., freshness, replay protection, and minimum covered components). [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)

### Signature parameters

Signature metadata (carried in `Signature-Input`) includes parameters such as `alg`, `created`, `expires`, `keyid`, `nonce`, and `tag` (application-specific). These parameter names are registered in the IANA **HTTP Signature Metadata Parameters** registry. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

### Signature base

The *signature base* is the canonicalized serialization of the selected component values plus the `@signature-params` line (which binds the covered component list and parameters). The signature is computed over this base. [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)

### On-the-wire HTTP fields

RFC 9421 specifies three related HTTP fields:

- `Signature-Input`: conveys the signature parameters and the covered component list.
- `Signature`: conveys the signature value(s).
- `Accept-Signature`: allows a party to request/indicate what signature(s) it would like on a subsequent message in an ongoing exchange. [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)

## Algorithms and registries

RFC 9421 defines initial algorithm identifiers (e.g., `rsa-pss-sha512`, `ecdsa-p256-sha256`, `ed25519`, `hmac-sha256`) and establishes IANA registries for:

- HTTP Signature Algorithms
- HTTP Signature Metadata Parameters
- HTTP Signature Derived Component Names
- HTTP Signature Component Parameters

See: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## Relationship to other mechanisms

HTTP Message Signatures are distinct from:

- **TLS**: transport security, not an application-verifiable signature over chosen HTTP components.
- **JWS (JSON Web Signature)**: signs an object in a JWS structure rather than selectively signing HTTP message components.

RFC 9421 also notes that message content is not directly covered by this specification; applications commonly rely on an HTTP content digest mechanism (e.g., the Digest Fields specification) and then sign that digest field. [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421)

## See also

- [[DPoP]]
- [[OAuth 2.0]]
- [[HTTP 402 Payment Required]]

## References

- IETF. *RFC 9421: HTTP Message Signatures*. February 2024. https://www.rfc-editor.org/rfc/rfc9421
- IETF Datatracker. *RFC 9421: HTTP Message Signatures*. https://datatracker.ietf.org/doc/rfc9421/
- IANA. *HTTP Message Signature* registries. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
