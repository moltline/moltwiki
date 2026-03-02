# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF Standards Track mechanism for creating, encoding, and verifying **digital signatures** or **message authentication codes (MACs)** over selected components of an HTTP request or response, standardized in **RFC 9421 (February 2024)**.
https://www.rfc-editor.org/rfc/rfc9421

Unlike transport security (e.g., TLS), HTTP Message Signatures operate at the **HTTP application layer**. This is useful in deployments where HTTP messages pass through intermediaries (e.g., TLS-terminating reverse proxies) and you still want a verifiable, end-to-end envelope. RFC 9421 targets use cases where “the full HTTP message may not be known to the signer” and where the message “may be transformed (e.g., by intermediaries) before reaching the verifier”.
https://www.rfc-editor.org/rfc/rfc9421

## What RFC 9421 defines

RFC 9421 standardizes:

- **What can be signed** ("covered components"):
  - HTTP **fields** (headers) and **trailer fields**.
    https://www.rfc-editor.org/rfc/rfc9421
  - **Derived components** (standardized computed values like `@method` and `@target-uri`).
    https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **How the signature base is constructed**: a canonical process to build the “signature base” from the selected components.
  https://www.rfc-editor.org/rfc/rfc9421
- **How signatures are carried on the wire** via two HTTP fields:
  - `Signature-Input` (declares the covered components and signature parameters)
  - `Signature` (carries the resulting signature value)

  https://www.rfc-editor.org/rfc/rfc9421
- **How to request signatures**: a way to request that a signature be applied to a subsequent HTTP message in an ongoing exchange via the `Accept-Signature` field.
  https://www.rfc-editor.org/rfc/rfc9421

## Core concepts

### Covered components

A signature covers a set of components drawn from an HTTP message. RFC 9421 distinguishes:

- **HTTP fields** (headers) and **trailer fields** (when present).
  https://www.rfc-editor.org/rfc/rfc9421

- **Derived components**: standardized computed values representing important parts of the request/response and target URI.
  https://www.rfc-editor.org/rfc/rfc9421

The IANA registry enumerates the currently registered derived component names, including:

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

Because the signer chooses what to cover, verifiers typically enforce **application-specific coverage requirements**. RFC 9421 calls out **insufficient coverage** as a security risk: if you don’t sign the right components, an attacker may be able to alter meaningful parts of the message without breaking verification.
https://www.rfc-editor.org/rfc/rfc9421

### Signature parameters (metadata)

Each signature can include metadata parameters registered in the “HTTP Signature Metadata Parameters” registry, including `created`, `expires`, `nonce`, `keyid`, `alg`, and `tag`.
https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Common uses:

- **Replay mitigation**: `created`/`expires` and/or `nonce` can help limit replay windows; RFC 9421 discusses "Signature Replay" in its security considerations.
  https://www.rfc-editor.org/rfc/rfc9421
- **Key identification**: `keyid` identifies the verification key; `alg` can explicitly declare the signature algorithm.
  https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

### Algorithms and registries

RFC 9421 establishes IANA registries for algorithms, metadata parameters, derived component names, and component parameters.
https://www.rfc-editor.org/rfc/rfc9421

The IANA “HTTP Signature Algorithms” registry lists initial algorithm identifiers such as `rsa-pss-sha512`, `hmac-sha256`, `ecdsa-p256-sha256`, and `ed25519`.
https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## Practical guidance

### What HTTP Message Signatures do (and do not) provide

- Provide **integrity and authentication** over the specific components you choose to cover.
  https://www.rfc-editor.org/rfc/rfc9421
- Do **not** provide confidentiality; use TLS (or another encryption layer) for secrecy. RFC 9421 explicitly notes that signatures do not provide confidentiality.
  https://www.rfc-editor.org/rfc/rfc9421

### Committing to message content (the body)

HTTP Message Signatures can cover headers, trailers, and derived components, but they do not automatically “sign the body” unless you include a component that commits to the content.
https://www.rfc-editor.org/rfc/rfc9421

A common pattern is:

1. Include a digest field that commits to the content (e.g., `Content-Digest`).
2. Include that digest field among the covered components.

`Content-Digest` is defined in **RFC 9530 (Digest Fields)**.
https://www.rfc-editor.org/rfc/rfc9530

### Intermediaries and transformations

RFC 9421 is designed to tolerate certain HTTP message transformations, but deployments still need a **coverage policy** that selects components stable across the intermediaries you expect. If a proxy rewrites a field, signing that field will (correctly) cause verification to fail.
https://www.rfc-editor.org/rfc/rfc9421

## Relationship to agent security and API protection

In tool-using/agentic architectures, HTTP Message Signatures can authenticate and integrity-protect calls between components (e.g., agent gateway → downstream tool service) in environments where TLS termination or intermediaries complicate end-to-end guarantees.

The key design step is a **coverage policy**: which derived components and fields must be signed for each API operation, and what replay protections are required.

## References

- RFC 9421 (full text): https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 status/errata info: https://www.rfc-editor.org/info/rfc9421
- IANA HTTP Message Signatures registries: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- IETF datatracker entry: https://datatracker.ietf.org/doc/rfc9421/
- RFC 9530 (Digest Fields): https://www.rfc-editor.org/rfc/rfc9530
