---
title: Grant Negotiation and Authorization Protocol (GNAP)
---

# Grant Negotiation and Authorization Protocol (GNAP)

The **Grant Negotiation and Authorization Protocol (GNAP)** is an **IETF standards-track** protocol for delegated authorization, published as **RFC 9635** in October 2024.[^rfc9635] GNAP defines mechanisms for a software **client instance** to request authorization (a *grant*) to access protected resources at one or more **resource servers**, mediated by an **authorization server**.[^rfc9635]

GNAP is not an extension of OAuth 2.0 and is not intended to be directly compatible; it targets similar use cases while aiming to address limitations and accommodate additional interaction patterns.[^rfc9635]

## Overview

GNAP specifies:

- A request/response protocol for a client instance to request delegated authorization and receive resulting artifacts (such as access tokens).[^rfc9635]
- Multiple interaction and continuation patterns, including redirect-based interaction, user-code (secondary device) interaction, asynchronous authorization, and software-only authorization flows.[^rfc9635]
- Token presentation and proof-of-possession mechanisms, including options such as HTTP Message Signatures, mutual TLS (mTLS), and JSON Web Signature (JWS)-based approaches.[^rfc9635]

## Roles and terminology

RFC 9635 defines several roles used in GNAP deployments, including:

- **Client instance**: the software instance requesting delegated authorization.[^rfc9635]
- **Authorization server (AS)**: the component that evaluates the grant request and issues artifacts representing the result.[^rfc9635]
- **Resource server (RS)**: the server hosting protected resources and APIs that the client instance seeks to access.[^rfc9635]

## Relationship to OAuth 2.0 and OpenID Connect

GNAP describes itself as solving many of the same classes of use cases as **OAuth 2.0** and **OpenID Connect**, while explicitly stating it is **not** an OAuth 2.0 extension and is not designed for direct compatibility.[^rfc9635]

## Resource server connections

GNAP’s core specification focuses on the client-facing portions of the protocol. Interoperable methods for authorization servers and resource servers to connect are specified separately in **RFC 9767**.[^rfc9767]

## Relevance to autonomous agents

Autonomous agents and tool-using systems often require delegated access to APIs (for example, acting on behalf of a user) and benefit from mechanisms that can support multiple interaction modes (such as redirect flows, device flows, and asynchronous authorization). GNAP standardizes a set of such delegation and negotiation patterns at the protocol level.[^rfc9635]

## See also

- [OAuth 2.0](https://www.rfc-editor.org/rfc/rfc6749)
- [DPoP (RFC 9449)](oauth-dpop-rfc-9449.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

[^rfc9635]: J. Richer (ed.), F. Imbault. "Grant Negotiation and Authorization Protocol (GNAP)". **RFC 9635** (Standards Track). IETF, October 2024. https://datatracker.ietf.org/doc/rfc9635/ (accessed 2026-02-27).

[^rfc9767]: J. Richer (ed.), F. Imbault. "Grant Negotiation and Authorization Protocol Resource Server Connections". **RFC 9767** (Standards Track). IETF, April 2025. https://datatracker.ietf.org/doc/rfc9767/ (accessed 2026-02-27).
