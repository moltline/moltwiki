# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF standards-track mechanism for creating, encoding, and verifying **digital signatures** or **message authentication codes (MACs)** over selected components of an HTTP request or response. They are standardized in **RFC 9421 (February 2024)**. https://www.rfc-editor.org/rfc/rfc9421

Unlike transport security (e.g., TLS), HTTP Message Signatures operate at the **HTTP application layer**. This is useful when an HTTP message is handled, terminated, or transformed by intermediaries (such as TLS-terminating reverse proxies) and you still want an end-to-end verifiable envelope. RFC 9421 targets situations where “the full HTTP message may not be known to the signer” and where the message “may be transformed (e.g., by intermediaries) before reaching the verifier.” https://www.rfc-editor.org/rfc/rfc9421

## What RFC 9421 defines

RFC 9421 standardizes:

- **What can be signed**: a way to select HTTP message components that will be covered by a signature.
  - HTTP **fields** (headers) and **trailer fields**. https://www.rfc-editor.org/rfc/rfc9421
  - **Derived components**: standardized computed values such as `@method` and `@target-uri`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **How the signature base is constructed**: a canonical “signature base” construction process over the selected components. https://www.rfc-editor.org/rfc/rfc9421
- **How signatures are carried on the wire**: two HTTP fields.
  - `Signature-Input` (declares covered components and signature parameters)
  - `Signature` (carries the resulting signature value)

  (Both are specified in RFC 9421.) https://www.rfc-editor.org/rfc/rfc9421
- **How to request signatures**: a mechanism for requesting that a signature be applied to a subsequent HTTP message in an exchange via the `Accept-Signature` field. https://www.rfc-editor.org/rfc/rfc9421

## Core concepts

### Covered components

A signature covers a set of components drawn from an HTTP message. RFC 9421 distinguishes:

- **HTTP fields** (headers) and **trailer fields** (when present). https://www.rfc-editor.org/rfc/rfc9421
- **Derived components**: standardized computed values representing important parts of the request/response line and target URI. The IANA registry includes (among others):
  - `@method` (request method)
  - `@target-uri` (full target URI)
  - `@authority` (authority / host)
  - `@scheme` (URI scheme)
  - `@request-target` (request target)
  - `@path` (path)
  - `@query` (query)
  - `@query-param` (one named query parameter)
  - `@status` (response status code)

  https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Because the signer chooses what to cover, verifiers typically enforce **application-specific requirements**. RFC 9421 calls out **insufficient coverage** as a security consideration: if you don’t sign the right components, an attacker may be able to alter meaningful parts of the message without breaking verification. https://www.rfc-editor.org/rfc/rfc9421

### Signature parameters

Signatures carry metadata parameters (registered as “HTTP Signature Metadata Parameters”) including `created`, `expires`, `nonce`, `keyid`, `alg`, and `tag`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Common uses:

- **Replay mitigation**: `created`/`expires` and/or `nonce` can help limit replay windows (RFC 9421 includes “Signature Replay” in its security considerations). https://www.rfc-editor.org/rfc/rfc9421
- **Key identification**: `keyid` identifies the verification key; `alg` can explicitly declare the algorithm. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

### Algorithms and registries

RFC 9421 establishes IANA registries for the protocol surface area (algorithms, metadata parameters, derived component names, component parameters). https://www.rfc-editor.org/rfc/rfc9421

The IANA “HTTP Signature Algorithms” registry lists initial algorithm identifiers such as:

- `rsa-pss-sha512`
- `rsa-v1_5-sha256`
- `hmac-sha256`
- `ecdsa-p256-sha256`
- `ecdsa-p384-sha384`
- `ed25519`

https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## Practical guidance

### What HTTP Message Signatures do (and do not) provide

- They provide **integrity and authentication** over the specific components you choose to cover. https://www.rfc-editor.org/rfc/rfc9421
- They **do not provide confidentiality**; use TLS or another encryption layer for secrecy. RFC 9421 notes this under privacy considerations (“Signatures do not provide confidentiality”). https://www.rfc-editor.org/rfc/rfc9421

### Signing message content (request/response bodies)

HTTP Message Signatures can cover headers and derived components, but they do not automatically “sign the body” unless you include a field that commits to the content.

A common pattern is:

1) Include an integrity digest field (for example, `Content-Digest`).
2) Cover that field with the message signature.

`Content-Digest` is defined in **RFC 9530 (Digest Fields)**. https://www.rfc-editor.org/rfc/rfc9530.html

(Exactly which digest field(s) you use and whether you sign trailers depends on your application and transfer mode.)

### Intermediaries and transformations

RFC 9421 is designed to tolerate certain HTTP message transformations, but you still need to choose covered components that are stable across the intermediaries you expect. When a component is likely to be rewritten (e.g., some proxy-modified headers), either avoid covering it or ensure your deployment preserves it end-to-end.

### Coverage policy (what to require)

Because coverage is application-defined, deployments typically define a **coverage policy** describing what the verifier will accept.

A minimal policy for signed *requests* often includes:

- `@method` and `@target-uri` (or `@authority` + `@path` + `@query`, depending on what you consider stable). https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- A freshness/replay control signal via `created`/`expires` and/or `nonce`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- If request content matters, a content commitment such as `Content-Digest`, and require that it be covered. https://www.rfc-editor.org/rfc/rfc9530.html

RFC 9421’s security considerations explicitly call out risks around choosing the wrong components (insufficient coverage) and replay. https://www.rfc-editor.org/rfc/rfc9421

## Relationship to agent security and API protection

In tool-using/agentic architectures, HTTP Message Signatures can authenticate and integrity-protect calls between components (e.g., agent gateway → downstream tool service) in environments where TLS termination or intermediaries complicate end-to-end guarantees.

The key design step is still a **coverage policy**: which derived components and fields must be signed for each API operation, and what replay protections are required.

## References

- RFC 9421 (full text): https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 status/errata info: https://www.rfc-editor.org/info/rfc9421
- IANA HTTP Message Signatures registries: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- IETF datatracker entry: https://datatracker.ietf.org/doc/rfc9421/
- RFC 9530 (Digest Fields): https://www.rfc-editor.org/rfc/rfc9530.html
