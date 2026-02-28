# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF standards-track mechanism for creating, encoding, and verifying **digital signatures** or **message authentication codes (MACs)** over selected components of an HTTP request or response. They are specified in **RFC 9421 (February 2024)**. https://www.rfc-editor.org/rfc/rfc9421

Unlike transport security (e.g., TLS), HTTP Message Signatures operate at the **HTTP application layer**. This supports use cases where the full message may not be known to the signer and where the message may be transformed by intermediaries before verification. https://www.rfc-editor.org/rfc/rfc9421

## What RFC 9421 standardizes

RFC 9421 defines:

- **Message components that can be covered** by a signature: HTTP fields (headers), trailer fields, and a set of standardized **derived components**. https://www.rfc-editor.org/rfc/rfc9421
- **Signature base construction**: how to serialize the selected components into a canonical “signature base” for signing and verification. https://www.rfc-editor.org/rfc/rfc9421
- **On-the-wire fields** used to carry signatures:
  - `Signature-Input` (declares covered components + parameters)
  - `Signature` (carries the signature value)

  https://www.rfc-editor.org/rfc/rfc9421
- **Signature requests** via `Accept-Signature` (requesting a signature on a subsequent message in an exchange). https://www.rfc-editor.org/rfc/rfc9421

## Core concepts

### Covered components

A signature covers a set of components drawn from an HTTP message:

- **HTTP fields** (headers) and **trailer fields** (when present). https://www.rfc-editor.org/rfc/rfc9421
- **Derived components**: standardized computed values representing important parts of the request/response line and target URI.

The IANA registry lists the currently-defined derived component names, including:

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

Because the signer chooses what to cover, verifiers typically enforce **application-specific requirements** (e.g., “requests MUST sign `@method` and `@target-uri` and MUST include a digest field”). RFC 9421 calls out **insufficient coverage** as a security risk: if you don’t sign the right components, an attacker may be able to alter meaningful parts of the message without breaking verification. https://www.rfc-editor.org/rfc/rfc9421

### Signature parameters

RFC 9421 defines signature metadata parameters (and IANA registers them) such as:

- `created`, `expires` (timestamps)
- `nonce` (single-use value)
- `keyid` (key identifier)
- `alg` (explicit algorithm identifier)
- `tag` (application-specific tag)

https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Common uses:

- **Replay mitigation**: constrain validity windows with `created`/`expires` and/or use `nonce` (see “Signature Replay” in RFC 9421 security considerations). https://www.rfc-editor.org/rfc/rfc9421
- **Key identification**: `keyid` identifies which verification key to use; `alg` can declare the algorithm identifier. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

### Algorithms and registries

RFC 9421 establishes IANA registries for algorithms, metadata parameters, derived component names, and component parameters. https://www.rfc-editor.org/rfc/rfc9421

The IANA “HTTP Signature Algorithms” registry lists initial algorithm identifiers such as `rsa-pss-sha512`, `hmac-sha256`, `ecdsa-p256-sha256`, and `ed25519`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## Practical guidance

### What HTTP Message Signatures provide (and do not provide)

- Provide **integrity and authentication** over the specific components you choose to cover. https://www.rfc-editor.org/rfc/rfc9421
- Do **not** provide confidentiality; use TLS (or another encryption layer) for secrecy. RFC 9421 notes that signatures do not provide confidentiality. https://www.rfc-editor.org/rfc/rfc9421

### Committing to message content (body)

HTTP Message Signatures cover headers/trailers and derived components; they do not automatically cover the message body unless you include a field that commits to the content.

A common pattern is to include `Content-Digest` (an integrity digest over the message content) and then sign that field. `Content-Digest` is defined in **RFC 9530 (Digest Fields)**. https://www.rfc-editor.org/rfc/rfc9530

### Intermediaries and transformations

RFC 9421 is designed to tolerate certain HTTP message transformations, but you still need to choose covered components that are stable across the intermediaries you expect. When a component is likely to be rewritten (e.g., proxy-modified headers), either avoid covering it or ensure your deployment preserves it end-to-end. https://www.rfc-editor.org/rfc/rfc9421

## Relationship to agent security and API protection

In agentic / tool-calling architectures, HTTP Message Signatures can authenticate and integrity-protect calls between components (e.g., agent gateway → downstream tool service) in environments where TLS termination or intermediaries complicate end-to-end guarantees.

A key design step is a **coverage policy**: which derived components and fields must be signed for each API operation, and what replay protections are required.

## References

- RFC 9421 (full text): https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 status/errata info: https://www.rfc-editor.org/info/rfc9421
- IANA HTTP Message Signatures registries: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- IETF datatracker entry: https://datatracker.ietf.org/doc/rfc9421/
- RFC 9530 (Digest Fields): https://www.rfc-editor.org/rfc/rfc9530
