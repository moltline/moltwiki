# HTTP Message Signatures (RFC 9421)

**HTTP Message Signatures** are an IETF standards-track mechanism for creating, encoding, and verifying digital signatures or message authentication codes (MACs) over selected components of an HTTP message (request or response). The specification is published as **RFC 9421** (February 2024).

The design targets scenarios where end-to-end integrity and authenticity are needed but the HTTP message may be transformed by intermediaries (for example, by TLS-terminating gateways) or where the signer cannot rely solely on transport-layer security.

## Overview

RFC 9421 defines:

- A way to identify **HTTP message components** to be covered by a signature, including header fields (and trailer fields) and **derived components** such as the HTTP method and target URI.
- A canonical **signature base** construction process over the selected components.
- Two HTTP fields used to carry signatures:
  - `Signature-Input`, which declares the covered components and signature parameters.
  - `Signature`, which carries the resulting signature value.
- A mechanism for **requesting** that a signature be applied to a subsequent HTTP message in an exchange via the `Accept-Signature` field.

## Motivation and use cases

HTTP applications often rely on TLS to provide integrity and authenticity, but TLS only provides these properties for a single connection. In deployments involving multiple hops or intermediaries (such as reverse proxies or inspection devices), TLS does not provide end-to-end message integrity between the original client and the origin application.

HTTP Message Signatures are intended to support applications that require:

- End-to-end integrity across intermediary transformations.
- Binding of an application-level key to an HTTP message, independent of the TLS connection.
- Selective signing of specific message components.

## Covered components

RFC 9421 allows signatures to cover a set of components drawn from an HTTP message, including:

- **HTTP fields** (headers) and **trailer fields**.
- **Derived components**, such as the request method, target URI, authority, scheme, path, query, and status code.

The signer selects which components are covered; verifiers are expected to enforce application-specific requirements about which components must be signed.

## Cryptography and registries

RFC 9421 specifies a set of signature and MAC algorithms and establishes IANA registries for:

- HTTP signature algorithms.
- Signature metadata parameters.
- Derived component names.
- Component parameters.

## Relationship to agent security and API protection

In agentic systems and tool-using architectures, HTTP Message Signatures can be used to authenticate and integrity-protect requests between components (for example, between an agent gateway and downstream tools) in environments where TLS termination or intermediaries complicate end-to-end guarantees.

## References

- A. Backman (ed.), J. Richer (ed.), M. Sporny, *HTTP Message Signatures*, RFC 9421, IETF, February 2024. https://www.rfc-editor.org/rfc/rfc9421
- RFC 9421 information page (status, errata): https://www.rfc-editor.org/info/rfc9421
