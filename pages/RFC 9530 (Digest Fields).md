# RFC 9530 (Digest Fields)

**RFC 9530** ("Digest Fields") defines HTTP fields that carry integrity digests for HTTP message content and HTTP representations. It specifies the `Content-Digest` and `Repr-Digest` fields, along with corresponding preference fields (`Want-Content-Digest` and `Want-Repr-Digest`) that allow a sender to indicate interest in receiving these digests.

The specification is published on the IETF Standards Track and **obsoletes RFC 3230**, replacing the older `Digest` and `Want-Digest` HTTP fields.

## Overview

HTTP commonly relies on lower-layer integrity mechanisms (for example, TLS record integrity) that apply only within a single connection. RFC 9530 defines digest fields at the HTTP layer so that endpoints (or applications using HTTP) can detect accidental corruption of conveyed bytes across multi-hop delivery paths.

RFC 9530 distinguishes between:

- **Content integrity**: a digest over the HTTP message **content** (the bytes conveyed as the message body).
- **Representation data integrity**: a digest over selected **representation data** for a resource (supporting more advanced cases such as validating a resource reconstructed from multiple responses).

## Defined fields

### Content-Digest

`Content-Digest` carries one or more digests computed over the HTTP message content. It can appear in requests or responses, and can also be used as a trailer field.

### Repr-Digest

`Repr-Digest` carries one or more digests computed over selected representation data for the resource. Like `Content-Digest`, it can appear in requests or responses and can be used as a trailer field.

RFC 9530 discusses considerations for using `Repr-Digest` in situations such as state-changing requests and interactions with `Content-Location`.

### Want-Content-Digest and Want-Repr-Digest

The `Want-Content-Digest` and `Want-Repr-Digest` fields allow a sender to express interest in receiving digest fields and to indicate algorithm preferences.

## Hash algorithm registry

RFC 9530 defines IANA actions, including creation of a registry for hash algorithms used with HTTP digest fields. This supports **algorithm agility** (the ability to introduce new hash algorithms over time).

## Relationship to HTTP Message Signatures

Digest fields are commonly discussed alongside mechanisms that sign HTTP messages or parts of messages. For example, an HTTP signature scheme may incorporate a digest field value to bind the signature to the message body or representation.

## Security considerations

Digest fields can help detect accidental corruption or unintended modification of HTTP content or representation data, but they are not a complete security solution by themselves. In particular:

- A digest field is not, by itself, an authenticated integrity mechanism; an active attacker who can modify traffic may be able to modify both the content and the digest.
- Digest fields can be combined with authenticated mechanisms (e.g., TLS, or message signing) depending on the threat model.

## References

- Roberto Polli; David Pardue. *Digest Fields*. RFC 9530 (Standards Track), February 2024. RFC Editor: https://www.rfc-editor.org/rfc/rfc9530.html
- IETF Datatracker entry for RFC 9530: https://datatracker.ietf.org/doc/rfc9530/
- RFC 3230 (obsoleted by RFC 9530): https://www.rfc-editor.org/rfc/rfc3230
