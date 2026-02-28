# OAuth 2.0 Protected Resource Metadata (RFC 9728)

## Summary

**OAuth 2.0 Protected Resource Metadata (RFC 9728)** defines a standard JSON metadata document that an OAuth 2.0 client (and/or an authorization server) can fetch to learn how to interact with a particular **protected resource** (i.e., resource server / API). It is designed to parallel **OAuth Authorization Server Metadata** (RFC 8414) and to help clients discover resource-server capabilities and the relevant authorization server(s).

In practice, this supports more interoperable, less “out-of-band” configuration for clients that need to call APIs protected by OAuth 2.0.

## Where the metadata lives

RFC 9728 defines a well-known location derived from the protected resource’s URL:

- `/.well-known/oauth-protected-resource`

A client uses the protected resource’s origin/URL to deterministically construct that metadata URL, then fetches a JSON document describing the resource.

## What the metadata contains (high level)

The protected resource metadata document can include, among other fields:

- The protected resource identifier(s)
- Supported authorization server(s) for the resource
- Resource capabilities and requirements (e.g., what token types / methods are expected)
- Optional human-readable information
- An option for **signed** metadata (JWT-based) in addition to unsigned/self-asserted metadata

(Exact field names and processing rules are defined by RFC 9728.)

## Relationship to other OAuth discovery specifications

RFC 9728 is intended to be structurally parallel to:

- **RFC 8414** (OAuth 2.0 Authorization Server Metadata), which lets clients discover authorization-server endpoints and capabilities.
- **RFC 7591** (OAuth 2.0 Dynamic Client Registration Protocol), which defines a way for clients to register and provide client metadata.

Together, these specs help reduce hard-coded configuration by enabling standardized discovery of both authorization servers and protected resources.

## Security considerations (selected)

Because resource metadata can influence where clients send users, tokens, or requests, RFC 9728 discusses several security topics, including:

- TLS requirements for metadata retrieval
- Impersonation and phishing risks
- SSRF considerations when fetching metadata
- Differences between unsigned and signed metadata
- Caching and freshness considerations

Refer to the RFC’s Security Considerations section for details.

## Sources

- RFC 9728 (RFC Editor): https://www.rfc-editor.org/info/rfc9728
- RFC 9728 (HTML): https://www.rfc-editor.org/rfc/rfc9728.html
- RFC 9728 (IETF Datatracker): https://datatracker.ietf.org/doc/rfc9728/
