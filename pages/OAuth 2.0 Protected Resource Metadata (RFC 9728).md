# OAuth 2.0 Protected Resource Metadata (RFC 9728)

**OAuth 2.0 Protected Resource Metadata** is an IETF Standards Track specification that defines a JSON metadata document a protected resource (resource server) can publish so that OAuth 2.0 clients and authorization servers can discover information needed to interact with that resource.

The document is published at a **well-known** location derived from the protected resource’s URL, and can optionally be provided as **signed metadata** using a JSON Web Token (JWT).

## Overview

OAuth deployments often require clients to know resource-specific details such as:

- Which **authorization server(s)** protect a resource
- Which **scopes** are relevant
- How to validate **audience restrictions** and avoid token misuse
- Where to find **keys** (e.g., a JWK Set URL) for verifying signed artifacts

RFC 9728 defines a standard metadata format and retrieval mechanism so these details can be discovered consistently, similar in spirit to **OAuth Authorization Server Metadata** (RFC 8414).

## Metadata publication and discovery

### Well-known resource metadata

A protected resource publishes metadata at a deterministic, well-known URL derived from the resource identifier. This design is intended to make it difficult for an attacker to publish metadata that appears to describe a resource they do not control.

RFC 9728 also defines a mechanism for using `WWW-Authenticate` challenges to indicate the resource metadata location to clients.

### Unsigned and signed metadata

RFC 9728 supports two ways to convey metadata:

- **Unsigned JSON** metadata published by the protected resource.
- **Signed metadata** represented as claims in a **JWT**, where the issuer vouches for the metadata values.

Signed metadata can be useful when metadata needs an integrity guarantee beyond HTTPS transport, or when metadata is distributed via intermediaries.

## Relationship to other OAuth discovery mechanisms

RFC 9728 is complementary to other OAuth discovery and metadata specifications:

- **RFC 8414 (OAuth 2.0 Authorization Server Metadata)**: describes how clients discover authorization server endpoints and capabilities.
- **RFC 7591 (OAuth 2.0 Dynamic Client Registration Protocol)**: defines how clients register with authorization servers, including client metadata.

In typical use, a client first discovers **resource metadata** (RFC 9728) to learn which authorization server(s) protect the resource, then discovers **authorization server metadata** (RFC 8414) to learn endpoints needed to obtain tokens.

## Security considerations (selected)

RFC 9728 includes security considerations related to:

- **Impersonation attacks** (publishing misleading metadata for a resource)
- **Audience-restricted access tokens** (ensuring tokens are bound to the intended resource)
- **Server-Side Request Forgery (SSRF)** risks during metadata retrieval
- **Phishing** and other client UX pitfalls
- **Caching** and metadata freshness

## See also

- [OAuth 2.0 Authorization Server Metadata (RFC 8414)](https://datatracker.ietf.org/doc/rfc8414/)
- [OAuth 2.0 Dynamic Client Registration Protocol (RFC 7591)](https://datatracker.ietf.org/doc/rfc7591/)

## Sources

- IETF Datatracker: *RFC 9728 — OAuth 2.0 Protected Resource Metadata* (April 2025) — https://datatracker.ietf.org/doc/rfc9728/
- RFC Editor: *RFC 9728* — https://www.rfc-editor.org/info/rfc9728
