---
title: Digest Fields (RFC 9530)
---

# Digest Fields (RFC 9530)

**Digest Fields** are HTTP header fields for carrying **integrity digests** (hashes) of HTTP message content or representations. They are standardized in **RFC 9530 (February 2024)**, which defines the `Content-Digest` and `Repr-Digest` fields, along with preference fields (`Want-Content-Digest`, `Want-Repr-Digest`) that let a sender indicate interest in receiving those digests.[^rfc9530]

RFC 9530 obsoletes **RFC 3230** (which defined the older `Digest` and `Want-Digest` fields).[^rfc9530]

## Overview

Digest fields are primarily used to provide **end-to-end integrity** signals at the HTTP layer:

- `Content-Digest` commits to the bytes of the **HTTP message content** (the payload/body) as transmitted.[^rfc9530]
- `Repr-Digest` commits to the bytes of a **representation** (a resource representation), which is useful when the representation can be obtained independently of the current message content (for example via content negotiation or a separate retrieval).[^rfc9530]

Because digests are carried in headers, they can be combined with other HTTP-layer integrity and authentication mechanisms—most notably **HTTP Message Signatures (RFC 9421)**—by signing the digest header rather than attempting to sign the body directly.[^rfc9530][^rfc9421]

## Defined fields

### `Content-Digest`

`Content-Digest` conveys one or more digests of the message content using registered hash algorithms.[^rfc9530]

Typical uses include:

- detecting accidental corruption or malicious tampering of the payload in transit (subject to deployment details and threat model),[^rfc9530]
- providing a stable value to be **covered by an HTTP Message Signature**, enabling integrity protection for the content via a signed header.[^rfc9530][^rfc9421]

### `Repr-Digest`

`Repr-Digest` conveys a digest of a **representation** of the resource, which can differ from the exact bytes carried in the current message body (for example, if content codings or partial representations are involved).[^rfc9530]

### Preference fields

`Want-Content-Digest` and `Want-Repr-Digest` allow a sender to express a preference for receiving the corresponding digest fields in responses.[^rfc9530]

## Relationship to HTTP Message Signatures

HTTP Message Signatures (RFC 9421) sign selected **HTTP fields** and **derived components**. To bind a signature to the message body, a common pattern is:

1. compute `Content-Digest` over the message content,
2. include the `Content-Digest` header,
3. include `Content-Digest` among the covered components in `Signature-Input`.

This approach makes the signed envelope commit to the content while staying within the RFC 9421 model (signing headers/derived components).[^rfc9530][^rfc9421]

## See also

- [HTTP Message Signatures (RFC 9421)](HTTP%20Message%20Signatures%20%28RFC%209421%29.md)

## References

[^rfc9530]: IETF. *RFC 9530: Digest Fields*. February 2024. https://www.rfc-editor.org/rfc/rfc9530
[^rfc9421]: IETF. *RFC 9421: HTTP Message Signatures*. February 2024. https://www.rfc-editor.org/rfc/rfc9421
