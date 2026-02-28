# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF standards-track mechanism for creating, encoding, and verifying **digital signatures** or **message authentication codes (MACs)** over selected components of an HTTP request or response, standardized in **RFC 9421 (February 2024)**. https://www.rfc-editor.org/rfc/rfc9421

Unlike transport security (e.g., TLS), HTTP Message Signatures operate at the **HTTP application layer**. This can be useful when an HTTP message is terminated, forwarded, or otherwise handled by intermediaries and you still need end-to-end verifiable integrity/authentication for parts of the message (subject to what you choose to cover). RFC 9421 explicitly targets cases where the message “may be transformed (e.g., by intermediaries) before reaching the verifier.” https://www.rfc-editor.org/rfc/rfc9421

## What RFC 9421 defines

RFC 9421 standardizes:

- **What can be covered** (“covered components”):
  - HTTP **fields** (headers) and **trailer fields**. https://www.rfc-editor.org/rfc/rfc9421
  - **Derived components** (standardized computed values such as `@method` and `@target-uri`). https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **How the signature base is constructed**: a canonical “signature base” over the selected components. https://www.rfc-editor.org/rfc/rfc9421
- **How signatures are carried on the wire**: two HTTP fields:
  - `Signature-Input` (declares the covered components and signature parameters)
  - `Signature` (carries the resulting signature value)

  https://www.rfc-editor.org/rfc/rfc9421
- **How to request signatures**: `Accept-Signature` allows a party to indicate which signature(s) it would like to receive in a subsequent message. https://www.rfc-editor.org/rfc/rfc9421

## Core concepts

### Covered components

A signature covers a set of components drawn from an HTTP message:

- **HTTP fields** (headers) and **trailer fields** (when present). https://www.rfc-editor.org/rfc/rfc9421
- **Derived components**: standardized computed values representing important parts of the request/response and target URI. The IANA registry includes (among others):
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

Because the signer chooses what to cover, verifiers typically enforce **application-specific coverage requirements** (e.g., requiring `@method` and `@target-uri` to be covered, and requiring a content digest field to be covered when message content matters). RFC 9421 highlights **insufficient coverage** as a security risk: if you don’t cover the right components, an attacker may be able to change meaningful parts of a message without breaking verification. https://www.rfc-editor.org/rfc/rfc9421

### Signature parameters

Signatures carry metadata parameters (registered as “HTTP Signature Metadata Parameters”) including `created`, `expires`, `nonce`, `keyid`, `alg`, and `tag`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Common uses:

- **Replay mitigation**: `created`/`expires` and/or `nonce` can help limit replay windows (RFC 9421 discusses “Signature Replay” in security considerations). https://www.rfc-editor.org/rfc/rfc9421
- **Key identification**: `keyid` identifies the verification key; `alg` can indicate the algorithm identifier. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

### Algorithms and registries

RFC 9421 establishes IANA registries for the protocol surface area (algorithms, metadata parameters, derived component names, component parameters). https://www.rfc-editor.org/rfc/rfc9421

The IANA “HTTP Signature Algorithms” registry lists initial algorithm identifiers such as `rsa-pss-sha512`, `hmac-sha256`, `ecdsa-p256-sha256`, and `ed25519`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## Practical guidance

### What HTTP Message Signatures do (and do not) provide

- Provide **integrity and authentication** over the specific components you choose to cover. https://www.rfc-editor.org/rfc/rfc9421
- Do **not** provide confidentiality; use TLS (or another encryption layer) for secrecy. RFC 9421 notes that signatures do not provide confidentiality under privacy considerations. https://www.rfc-editor.org/rfc/rfc9421

### Signing message content (the body)

HTTP Message Signatures cover headers/trailers and derived components. To bind the **message content** (body) you typically include a field that commits to the content and then cover that field.

A common pattern is to include `Content-Digest` and cover it. `Content-Digest` is defined in **RFC 9530 (Digest Fields)**. https://www.rfc-editor.org/rfc/rfc9530.html

(Exactly which digest field(s) you use and whether you cover trailers depends on your application and transfer mode.)

### Intermediaries and transformations

RFC 9421 is designed to tolerate certain HTTP message transformations, but you still need to choose covered components that are stable across the intermediaries you expect. If a proxy rewrites a header you covered, verification will fail; if a proxy rewrites something you did *not* cover, verification may still succeed but the message semantics may have changed.

## Relationship to agent security and API protection

In tool-using/agentic architectures, HTTP Message Signatures can authenticate and integrity-protect calls between components (e.g., agent gateway → downstream tool service) in environments where TLS termination or intermediaries complicate end-to-end guarantees.

The key design step is a **coverage policy**: which derived components and fields must be covered for each API operation, and what replay protections are required.

## References

- RFC 9421 (full text): https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 status/errata info: https://www.rfc-editor.org/info/rfc9421
- IANA HTTP Message Signatures registries: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- IETF datatracker entry: https://datatracker.ietf.org/doc/rfc9421/
- RFC 9530 (Digest Fields): https://www.rfc-editor.org/rfc/rfc9530.html
