# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF standards-track mechanism for creating, encoding, and verifying **digital signatures** or **message authentication codes (MACs)** over selected components of an HTTP request or response. They are standardized in **RFC 9421** (February 2024). https://www.rfc-editor.org/rfc/rfc9421

This is an application-layer integrity/authenticity mechanism designed for cases where the HTTP message might be **handled or transformed by intermediaries** (e.g., TLS-terminating reverse proxies) and you still want an end-to-end verifiable envelope. RFC 9421 explicitly targets situations where “the full HTTP message may not be known to the signer” and where the message “may be transformed (e.g., by intermediaries) before reaching the verifier.” https://www.rfc-editor.org/rfc/rfc9421

## What RFC 9421 defines

RFC 9421 standardizes:

- A way to select **HTTP message components** that will be covered by a signature, including:
  - HTTP **fields** (headers) and **trailer fields**
  - **derived components** (e.g., `@method`, `@target-uri`, `@authority`, `@scheme`, `@path`, `@query`, `@status`) https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- A canonical **signature base** construction process over the selected components. https://www.rfc-editor.org/rfc/rfc9421
- Two HTTP fields used to carry signatures:
  - `Signature-Input` (declares the covered components and signature parameters)
  - `Signature` (carries the resulting signature value)
  
  (Both are specified in RFC 9421.) https://www.rfc-editor.org/rfc/rfc9421
- A mechanism for **requesting** that a signature be applied to a subsequent HTTP message in an exchange via the `Accept-Signature` field. https://www.rfc-editor.org/rfc/rfc9421

## Core concepts

### Covered components

A signature covers a set of components drawn from an HTTP message. RFC 9421 distinguishes:

- **HTTP fields** (headers) and **trailer fields** (when present). https://www.rfc-editor.org/rfc/rfc9421
- **Derived components**: standardized, computed values representing important parts of the request/response line and target URI. The initial registry includes `@method`, `@target-uri`, `@authority`, `@scheme`, `@request-target`, `@path`, `@query`, `@query-param`, and `@status`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

Because the signer chooses what to cover, verifiers typically enforce **application-specific requirements** (e.g., “must sign `@method` and `@target-uri` and `content-digest`”). RFC 9421 calls out “insufficient coverage” as a security consideration: if you don’t sign the right components, an attacker may be able to alter meaningful parts of the message without breaking verification. https://www.rfc-editor.org/rfc/rfc9421

### Signature parameters

Signatures carry metadata parameters such as `created`, `expires`, `nonce`, `keyid`, `alg`, and `tag` (registered as “HTTP Signature Metadata Parameters”). https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

These parameters are commonly used to:

- Mitigate **replay** (e.g., with `created`/`expires` and/or `nonce`). RFC 9421 includes “Signature Replay” in its security considerations. https://www.rfc-editor.org/rfc/rfc9421
- Identify the verification key (`keyid`) and, where applicable, the algorithm (`alg`). https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## Algorithms and IANA registries

RFC 9421 establishes IANA registries for the protocol surface area (algorithms, parameters, derived component names, component parameters). https://www.rfc-editor.org/rfc/rfc9421

The IANA “HTTP Signature Algorithms” registry lists initial algorithm identifiers such as `rsa-pss-sha512`, `rsa-v1_5-sha256`, `hmac-sha256`, `ecdsa-p256-sha256`, `ecdsa-p384-sha384`, and `ed25519`. https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml

## When to use (and what it does *not* do)

- Use HTTP Message Signatures when you need **integrity + authentication** semantics that survive beyond a single TLS hop (e.g., across gateways) or when you need a signed envelope for logging/repudiation-resistant workflows.
- HTTP Message Signatures **do not provide confidentiality**; that remains the job of TLS or other encryption layers. RFC 9421 explicitly notes this under privacy considerations. https://www.rfc-editor.org/rfc/rfc9421

## Relationship to agent security and API protection

In tool-using/agentic architectures, HTTP Message Signatures can help authenticate and integrity-protect calls between components (e.g., an agent gateway → downstream tool service) in environments where TLS termination or intermediaries complicate end-to-end guarantees. The important design step is to define (and enforce) a **coverage policy**: which derived components and fields must be signed for each API operation.

## References

- RFC 9421 (full text): https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 status/errata info: https://www.rfc-editor.org/info/rfc9421
- IANA HTTP Message Signatures registries: https://www.iana.org/assignments/http-message-signature/http-message-signature.xhtml
- IETF datatracker entry: https://datatracker.ietf.org/doc/rfc9421/
