# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF standards-track mechanism for creating, encoding, and verifying **digital signatures** or **message authentication codes (MACs)** over selected components of an HTTP request or response. They are standardized in **RFC 9421 (February 2024)**. https://www.rfc-editor.org/rfc/rfc9421

Unlike transport security (e.g., TLS), HTTP Message Signatures operate at the **HTTP application layer**. This is useful when an HTTP message is handled, terminated, or partially transformed by intermediaries (for example, TLS-terminating reverse proxies), but you still want an end-to-end verifiable envelope at the HTTP layer. RFC 9421 explicitly targets situations where “the full HTTP message may not be known to the signer” and where the message “may be transformed (e.g., by intermediaries) before reaching the verifier.” https://www.rfc-editor.org/rfc/rfc9421

## What RFC 9421 defines

RFC 9421 standardizes:

- **What can be signed**: a way to select HTTP message components that will be covered by a signature.
  - HTTP **fields** (headers) and **trailer fields** https://www.rfc-editor.org/rfc/rfc9421
  - **Derived components** (standardized computed values such as `@method` and `@target-uri`) https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **How the signature base is constructed**: a canonical “signature base” construction process over the selected components. https://www.rfc-editor.org/rfc/rfc9421
- **How signatures are carried on the wire**: two HTTP fields
  - `Signature-Input` (declares the covered components and signature parameters)
  - `Signature` (carries the resulting signature value)

  (Both are specified in RFC 9421.) https://www.rfc-editor.org/rfc/rfc9421
- **How to request signatures**: a mechanism for requesting that a signature be applied to a subsequent HTTP message in an exchange via the `Accept-Signature` field. https://www.rfc-editor.org/rfc/rfc9421

## Core concepts

### Covered components

A signature covers a set of components drawn from an HTTP message.

RFC 9421 distinguishes:

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

Because the signer chooses what to cover, verifiers typically enforce **application-specific coverage requirements**.

A common pitfall is **insufficient coverage**: if you don’t sign the components that your application actually relies on, an attacker might be able to alter meaningful parts of the message without breaking signature verification. RFC 9421 calls this out in its security considerations. https://www.rfc-editor.org/rfc/rfc9421

### Signature parameters

Signatures carry metadata parameters (registered as “HTTP Signature Metadata Parameters”) including `created`, `expires`, `nonce`, `keyid`, `alg`, and `tag`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Common uses:

- **Replay mitigation**: `created`/`expires` and/or `nonce` can help limit replay windows (RFC 9421 includes “Signature Replay” in its security considerations). https://www.rfc-editor.org/rfc/rfc9421
- **Key identification**: `keyid` identifies the verification key, with `alg` optionally declaring the algorithm. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

### Algorithms and registries

RFC 9421 establishes IANA registries for the protocol surface area (algorithms, metadata parameters, derived component names, component parameters). https://www.rfc-editor.org/rfc/rfc9421

The IANA “HTTP Message Signatures” registries include:

- **HTTP Signature Algorithms** (algorithm identifiers used by `alg`) https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **HTTP Signature Metadata Parameters** (parameters like `created`, `expires`, `nonce`, `keyid`, `alg`, `tag`) https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **HTTP Signature Derived Component Names** (names like `@method`, `@target-uri`, `@status`) https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

The initial algorithm identifiers include `rsa-pss-sha512`, `hmac-sha256`, `ecdsa-p256-sha256`, and `ed25519`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## How it looks on the wire

RFC 9421 defines two HTTP fields used to carry signatures:

- `Signature-Input`: declares one or more named signatures, each with a list of covered components and parameters (e.g., `created`, `nonce`, `keyid`, `alg`). https://www.rfc-editor.org/rfc/rfc9421
- `Signature`: carries the corresponding signature value(s). https://www.rfc-editor.org/rfc/rfc9421

A single HTTP message can carry multiple signatures (for example, different keys or different coverage sets), and the signature name ties the `Signature-Input` parameters to the `Signature` value. https://www.rfc-editor.org/rfc/rfc9421

## Practical guidance

### What HTTP Message Signatures do (and do not) provide

- They provide **integrity and authentication** over the specific components you choose to cover. https://www.rfc-editor.org/rfc/rfc9421
- They **do not provide confidentiality**; use TLS or another encryption layer for secrecy. RFC 9421 notes this under privacy considerations (“Signatures do not provide confidentiality”). https://www.rfc-editor.org/rfc/rfc9421

### Signing message content (the body)

HTTP Message Signatures cover **HTTP fields/trailers and derived components**. They do not directly cover the message body unless you include a field that commits to the content.

A common pattern is:

1) include an integrity digest field (e.g., `Content-Digest`), and then
2) include that field in the covered components list.

The `Content-Digest` field is defined in **RFC 9530 (Digest Fields)** and “can be used for the integrity of HTTP message content.” https://www.rfc-editor.org/rfc/rfc9530.html

(Exactly which digest field(s) you use and whether you sign trailers depends on your application and transfer mode.)

### Intermediaries and transformations

RFC 9421 is designed to tolerate certain HTTP message transformations, but you still need to choose covered components that are stable across the intermediaries you expect.

If an intermediary is likely to rewrite a header (or you can’t guarantee it will be preserved), either avoid covering it or ensure your deployment preserves it end-to-end. Otherwise signatures will fail to verify.

### Coverage policy (what to require)

Treat signature verification as **policy-driven**:

- Define which derived components must be signed for each operation (for example, requests might require `@method` and `@target-uri`).
- Define which headers must be signed (for example, a timestamp-like header or an idempotency key).
- Define replay protections (e.g., enforce `created`/`expires` windows and/or `nonce` uniqueness).

RFC 9421 provides the building blocks; applications decide what constitutes an acceptable signature. https://www.rfc-editor.org/rfc/rfc9421

## References

- RFC 9421 (full text): https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 status/errata info: https://www.rfc-editor.org/info/rfc9421
- IANA HTTP Message Signatures registries: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- IETF datatracker entry: https://datatracker.ietf.org/doc/rfc9421/
- RFC 9530 (Digest Fields): https://www.rfc-editor.org/rfc/rfc9530.html
