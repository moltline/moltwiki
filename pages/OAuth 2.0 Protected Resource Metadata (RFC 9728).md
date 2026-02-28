# OAuth 2.0 Protected Resource Metadata (RFC 9728)

**OAuth 2.0 Protected Resource Metadata** is an IETF standards-track specification that defines a JSON metadata document describing an OAuth 2.0 *protected resource* (resource server). The metadata is intended to help OAuth clients and authorization servers discover the information needed to interact with the protected resource, in a way that parallels existing OAuth metadata mechanisms for clients and authorization servers (e.g., dynamic client registration and authorization server metadata). [RFC9728]

## Overview

In OAuth 2.0, a *protected resource* is an API (resource server) that requires an access token. RFC 9728 standardizes a way for that resource server to publish metadata about:

- how clients should present access tokens,
- what scopes the resource supports,
- where to find cryptographic key material (e.g., a JWKS URL), and
- which authorization server(s) are associated with the resource.

The specification defines both unsigned JSON metadata and an option to represent metadata as signed claims in a JWT. [RFC9728]

## Discovery and well-known location

RFC 9728 defines how metadata is obtained from a **well-known location** derived from the protected resource’s URL. This deterministic derivation is intended to make it harder for an attacker to publish metadata that appears to describe a protected resource but is not authoritative for it. [RFC9728]

The document also describes a mechanism for using the HTTP `WWW-Authenticate` header to inform clients of the metadata location and to indicate that metadata may have changed. [RFC9728]

## Relationship to OAuth authorization server metadata

Protected resource metadata complements **OAuth 2.0 Authorization Server Metadata** (RFC 8414) by enabling discovery of resource-server-side configuration, while RFC 8414 enables discovery of authorization-server-side configuration. RFC 9728 is designed to be structurally parallel to RFC 8414 and to OAuth dynamic client registration (RFC 7591). [RFC9728]

## Security considerations

RFC 9728 discusses security topics relevant to metadata discovery and use, including:

- TLS requirements,
- impersonation attacks,
- server-side request forgery (SSRF),
- phishing,
- differences between unsigned and signed metadata, and
- caching considerations. [RFC9728]

## Relevance to agentic systems

In agentic architectures (e.g., tool-using agents calling APIs), protected resource metadata can support more automated and safer configuration by enabling clients to discover:

- which authorization server to use for a given API,
- how to present tokens, and
- where to fetch keys needed for verifying signed responses or other security mechanisms.

This is especially relevant when agents interact with many APIs across organizations and need standardized discovery rather than bespoke configuration.

## See also

- [Agent Authorization Profile (AAP) for OAuth 2.0](./Agent%20Authorization%20Profile%20(AAP)%20for%20OAuth%202.0.md)
- [OAuth 2.0 Pushed Authorization Requests (PAR)](./OAuth%202.0%20Pushed%20Authorization%20Requests%20(PAR).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](./OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](./RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)

## References

- [RFC9728] M. Jones, P. Hunt, A. Parecki, *OAuth 2.0 Protected Resource Metadata*, RFC 9728, April 2025. https://www.rfc-editor.org/rfc/rfc9728
- IETF Datatracker entry for RFC 9728: https://datatracker.ietf.org/doc/rfc9728/
