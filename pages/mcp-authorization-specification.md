---
title: "Model Context Protocol (MCP) authorization specification"
---

The **Model Context Protocol (MCP) authorization specification** defines how MCP clients obtain and present authorization to access protected MCP servers over **HTTP-based transports**. It adapts established OAuth and OpenID Connect discovery and metadata mechanisms for the MCP ecosystem, including discovery of authorization servers via **OAuth 2.0 Protected Resource Metadata**.

## Overview

Authorization support is **optional** for MCP implementations. When used for HTTP transports, MCP defines an authorization model in which:

- An **MCP server** acts as an OAuth **resource server**, accepting requests authorized by **access tokens**.
- An **MCP client** acts as an OAuth **client**, requesting and using access tokens on behalf of a **resource owner**.
- An **authorization server** issues access tokens; its implementation details are out of scope for MCP.

The specification is based on a selected subset of existing standards to improve interoperability while maintaining a relatively simple integration surface.

## Authorization server discovery

### Protected Resource Metadata (RFC 9728)

MCP servers are required to implement **OAuth 2.0 Protected Resource Metadata** (RFC 9728) to advertise the authorization servers associated with the protected resource.

The Protected Resource Metadata document returned by an MCP server includes an `authorization_servers` field listing one or more authorization server issuer identifiers.

### Discovery mechanisms

To enable clients to find the Protected Resource Metadata document, MCP servers must support at least one of the RFC 9728 discovery approaches:

- **`WWW-Authenticate` header**: when returning `401 Unauthorized`, include a `resource_metadata` parameter pointing to the metadata document.
- **Well-known URI**: serve metadata at a well-known location, either rooted at the server’s MCP endpoint path or at the origin root, following RFC 9728.

MCP clients must support both approaches, preferring the `resource_metadata` URL from `WWW-Authenticate` when present, and otherwise falling back to constructing and requesting the well-known URIs.

### Scope guidance

The specification recommends that MCP servers include a `scope` parameter in the `WWW-Authenticate` challenge (as defined for Bearer tokens in RFC 6750) to guide clients toward least-privilege scope requests.

## Authorization server metadata discovery

Once a client has an authorization server issuer identifier, it discovers that server’s capabilities and endpoints using either:

- **OAuth 2.0 Authorization Server Metadata** (RFC 8414), or
- **OpenID Connect Discovery 1.0**.

To improve interoperability across issuer URL formats (including issuers with path components), MCP clients are required to attempt multiple well-known endpoints in a defined priority order, following RFC 8414 guidance and compatibility notes.

## Client registration approaches

The MCP authorization specification describes multiple approaches for OAuth client registration, intended to cover common MCP deployment scenarios:

- **Client ID Metadata Documents**: using an HTTPS URL as the `client_id` that resolves to a JSON document containing client metadata.
- **Pre-registration**: using client credentials established out-of-band.
- **Dynamic Client Registration** (RFC 7591): as a fallback or for compatibility when supported by the authorization server.

The specification recommends a priority order for clients that support multiple approaches: use pre-registration when available, otherwise use Client ID Metadata Documents when supported, and fall back to Dynamic Client Registration when available.

## Standards referenced

The MCP authorization specification cites and builds upon several OAuth-related standards and drafts, including:

- OAuth 2.0 Authorization Server Metadata (RFC 8414)
- OAuth 2.0 Dynamic Client Registration Protocol (RFC 7591)
- OAuth 2.0 Protected Resource Metadata (RFC 9728)
- OAuth 2.0 Bearer Token Usage (RFC 6750)
- OAuth 2.1 (IETF draft)
- OAuth Client ID Metadata Documents (IETF draft)
- OpenID Connect Discovery 1.0

## References

- Model Context Protocol specification, “Authorization” (protocol revision 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
- IETF RFC 9728: *OAuth 2.0 Protected Resource Metadata*. https://datatracker.ietf.org/doc/html/rfc9728
- IETF RFC 8414: *OAuth 2.0 Authorization Server Metadata*. https://datatracker.ietf.org/doc/html/rfc8414
- IETF RFC 7591: *OAuth 2.0 Dynamic Client Registration Protocol*. https://datatracker.ietf.org/doc/html/rfc7591
- IETF RFC 6750: *The OAuth 2.0 Authorization Framework: Bearer Token Usage*. https://datatracker.ietf.org/doc/html/rfc6750
- OpenID Connect Discovery 1.0. https://openid.net/specs/openid-connect-discovery-1_0.html
