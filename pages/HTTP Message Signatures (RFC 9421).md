# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF standards-track mechanism for creating, encoding, and verifying **digital signatures** or **message authentication codes (MACs)** over selected components of an HTTP request or response, standardized in **RFC 9421 (February 2024)**. https://www.rfc-editor.org/rfc/rfc9421

Unlike transport security (e.g., TLS), HTTP Message Signatures operate at the **HTTP application layer**. This can be useful when an HTTP message is handled, terminated, or transformed by intermediaries (such as TLS-terminating reverse proxies) and you still want an end-to-end verifiable envelope. RFC 9421 targets situations where the message may be transformed by intermediaries before reaching the verifier. https://www.rfc-editor.org/rfc/rfc9421

## What RFC 9421 defines

RFC 9421 standardizes:

- **What can be signed**: a way to select HTTP message components covered by a signature.
  - HTTP **fields** (headers) and **trailer fields**. https://www.rfc-editor.org/rfc/rfc9421
  - **Derived components** (standardized computed values such as `@method` and `@target-uri`). https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **How the signature base is constructed**: a canonical construction process for the “signature base” over the selected components. https://www.rfc-editor.org/rfc/rfc9421
- **How signatures are carried on the wire**: two HTTP fields.
  - `Signature-Input` (declares the covered components and signature parameters)
  - `Signature` (carries the resulting signature value)

  https://www.rfc-editor.org/rfc/rfc9421
- **How to request signatures**: a mechanism to request that a signature be applied to a subsequent HTTP message in an exchange via the `Accept-Signature` field. https://www.rfc-editor.org/rfc/rfc9421

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

Because the signer chooses what to cover, verifiers typically enforce **application-specific requirements** (for example, “requests MUST sign `@method` and `@target-uri` and MUST include a content digest field”). RFC 9421 calls out **insufficient coverage** as a security consideration: if you don’t sign the right components, an attacker may be able to alter meaningful parts of the message without breaking verification. https://www.rfc-editor.org/rfc/rfc9421

### Signature parameters

Signatures carry metadata parameters (registered as “HTTP Signature Metadata Parameters”) including `created`, `expires`, `nonce`, `keyid`, `alg`, and `tag`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Common uses:

- **Replay mitigation**: `created`/`expires` and/or `nonce` can help limit replay windows (RFC 9421 includes “Signature Replay” in its security considerations). https://www.rfc-editor.org/rfc/rfc9421
- **Key identification**: `keyid` identifies the verification key, with `alg` optionally declaring the algorithm. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

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
- They **do not provide confidentiality**; use TLS (or another encryption layer) for secrecy. RFC 9421 notes this under privacy considerations. https://www.rfc-editor.org/rfc/rfc9421

### Signing message content (the body)

HTTP Message Signatures can cover headers and derived components, but they do not automatically cover the message body unless you include a field that commits to the content.

A common pattern is:

1) compute a digest of the content,
2) put it in the `Content-Digest` field, and
3) include `content-digest` among the covered components.

`Content-Digest` is defined in **RFC 9530 (Digest Fields)**. https://www.rfc-editor.org/rfc/rfc9530.html

(Exactly which digest field(s) you use and whether you sign trailers depends on your application and transfer mode.)

### Intermediaries and transformations

RFC 9421 is designed to tolerate certain HTTP message transformations, but you still need to choose covered components that are stable across the intermediaries you expect. When a component is likely to be rewritten (e.g., some proxy-modified headers), either avoid covering it or ensure your deployment preserves it end-to-end.

### A minimal “coverage policy” checklist

When designing a scheme with HTTP Message Signatures, decide and document:

- **Which derived components must be covered** (commonly `@method` and `@target-uri`). https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- **Which headers must be covered** (e.g., `content-digest` when there is content). https://www.rfc-editor.org/rfc/rfc9530.html
- **Replay protections** (e.g., require `created`/`expires` and/or `nonce`, and enforce clock skew and nonce storage rules). https://www.rfc-editor.org/rfc/rfc9421
- **Key discovery/selection** (what `keyid` means in your system and how verifiers retrieve the key). https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## Relationship to agent security and API protection

In tool-using/agentic architectures, HTTP Message Signatures can authenticate and integrity-protect calls between components (e.g., agent gateway → downstream tool service) in environments where TLS termination or intermediaries complicate end-to-end guarantees.

The key design step is a **coverage policy**: which derived components and fields must be signed for each API operation, and what replay protections are required.

## References

- RFC 9421 (full text): https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 status/errata info: https://www.rfc-editor.org/info/rfc9421
- IANA HTTP Message Signatures registries: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- IETF datatracker entry: https://datatracker.ietf.org/doc/rfc9421/
- RFC 9530 (Digest Fields): https://www.rfc-editor.org/rfc/rfc9530.html
