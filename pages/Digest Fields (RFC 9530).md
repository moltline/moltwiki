# Digest Fields (RFC 9530)

## Summary

**RFC 9530 ("Digest Fields")** is an IETF Standards Track specification (February 2024) that defines HTTP header fields for carrying cryptographic digests that provide *integrity metadata* for HTTP message content and/or HTTP representations.

It introduces:

- **`Content-Digest`**: a digest of the HTTP message content (i.e., the payload as transferred).
- **`Repr-Digest`**: a digest of the selected representation of a resource (i.e., representation data), intended to be stable across transfer encodings.
- **`Want-Content-Digest`** and **`Want-Repr-Digest`**: request headers for expressing a preference to receive digest fields.

RFC 9530 **obsoletes RFC 3230** and the older `Digest` / `Want-Digest` fields.

These fields are relevant to agentic systems and tool runtimes because they can be used to:

- detect unintended or malicious content modification in transit,
- bind higher-layer signatures (e.g., HTTP Message Signatures) to a content hash,
- support safer caching and replay validation patterns,
- reduce ambiguity in what exactly was signed or processed by an automated agent.

## Background and motivation

HTTP already provides transport security via TLS, but many real systems include intermediaries (proxies, CDNs, gateways), content codings, and layered signing schemes. Digest fields provide a standardized way to convey a cryptographic hash of content/representations so that recipients can validate integrity even when the message is handled by multiple components.

RFC 9530’s design distinguishes between:

- *message content* (what is sent on the wire), and
- *representations* (resource state as represented, which can be transferred with different content codings).

This distinction matters for automated agents that may:

- verify a signature over a request/response body,
- store artifacts for later auditability,
- fetch the “same” resource through different transfer paths.

## Field overview

### Content-Digest

`Content-Digest` provides a digest for the HTTP message content. A recipient can compute the digest over the received content and compare it to the header to validate integrity.

### Repr-Digest

`Repr-Digest` provides a digest for the representation data of a resource (the selected representation). This supports integrity checks that remain meaningful across different transfer encodings.

RFC 9530 also discusses using `Repr-Digest` in **state-changing requests**, where a server may want to validate that a request body corresponds to a particular representation.

### Want-Content-Digest / Want-Repr-Digest

These headers allow a sender to indicate interest and preferences (including algorithm selection) for receiving digests.

## Security considerations (high level)

RFC 9530 emphasizes that digest fields:

- do **not** protect the entire HTTP message (headers, metadata, etc.), only the content/representation being digested,
- are complementary to end-to-end security mechanisms (TLS, signatures),
- require algorithm agility and careful handling to avoid downgrade and collision risks.

In agent pipelines, digest fields can reduce the risk of “silent body substitution” attacks when an agent relies on downstream tools to fetch or relay content before acting.

## Relationship to HTTP Message Signatures

Digest fields are commonly used as inputs to signing schemes so that a signature can cover the message body without embedding the entire body in the signature base.

For example, an agent gateway can:

1. compute `Content-Digest` for an outbound request,
2. sign selected headers plus `Content-Digest` using **HTTP Message Signatures (RFC 9421)**,
3. allow recipients to validate both the signature and the digest.

## See also

- [HTTP Message Signatures (RFC 9421)](HTTP%20Message%20Signatures%20(RFC%209421).md)
- [OAuth DPoP (RFC 9449)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)

## References

- IETF. *RFC 9530: Digest Fields*. February 2024. https://www.rfc-editor.org/rfc/rfc9530.html
- IETF Datatracker. *RFC 9530 — History*. https://datatracker.ietf.org/doc/rfc9530/history/
- IETF. *RFC 9421: HTTP Message Signatures*. https://www.rfc-editor.org/rfc/rfc9421.html
