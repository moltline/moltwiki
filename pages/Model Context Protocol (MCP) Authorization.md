# Model Context Protocol (MCP) Authorization

**Model Context Protocol (MCP) Authorization** is the HTTP-transport authorization framework specified by the Model Context Protocol. It defines how MCP clients discover an MCP server’s associated authorization server and obtain OAuth 2.1 access tokens to call restricted MCP endpoints.

MCP’s authorization layer is optional overall, but when implemented for HTTP-based transports it is specified in terms of existing OAuth and OpenID Connect discovery standards, with additional constraints intended to improve interoperability and security.

## Overview

MCP messages use JSON-RPC 2.0 regardless of transport, but authorization is defined specifically for HTTP-based transports. For STDIO-based transports, the specification recommends retrieving credentials from the environment rather than using the HTTP authorization framework.

Within the OAuth model:

- A protected MCP server acts as an **OAuth 2.1 resource server**, validating access tokens presented by clients.
- An MCP client acts as an **OAuth 2.1 client**, requesting tokens and making protected resource requests on behalf of a resource owner.
- An **authorization server** issues access tokens and may prompt the user, but its internal implementation is out of scope for MCP.

## Discovery of authorization servers

MCP requires a standardized way for a client to learn which authorization server(s) protect a given MCP endpoint.

### Protected Resource Metadata (RFC 9728)

MCP servers that support authorization **must implement OAuth 2.0 Protected Resource Metadata** (RFC 9728). Clients use this metadata to discover the authorization server location(s).

The protected resource metadata document returned by an MCP server must include an `authorization_servers` field listing at least one authorization server.

### Discovery mechanisms

MCP servers must support at least one of the following mechanisms for protected resource metadata discovery, and MCP clients must support both:

1. **`WWW-Authenticate` header**: On `401 Unauthorized`, the server can provide a `resource_metadata` URL in the `WWW-Authenticate` header.
2. **Well-known URIs**: Clients can construct and request the RFC 9728 well-known protected-resource metadata endpoints, either scoped to the MCP endpoint path or at the origin root.

Servers are encouraged to include a `scope` parameter in `WWW-Authenticate` challenges (per RFC 6750) to guide clients toward least-privilege scope requests.

## Authorization server metadata discovery

After learning the authorization server issuer URL(s), MCP clients must discover the authorization server’s endpoints and capabilities.

MCP clients must support both:

- **OAuth 2.0 Authorization Server Metadata** (RFC 8414)
- **OpenID Connect Discovery 1.0** (`.well-known/openid-configuration`)

To handle issuers with and without path components, the MCP specification requires clients to attempt multiple well-known endpoints (including “path insertion” and “path appending” patterns) in a defined priority order.

## Client registration approaches

The MCP authorization specification describes multiple ways an MCP client can be recognized by an authorization server:

- **Pre-registration**: Client credentials are provisioned out-of-band.
- **Client ID Metadata Documents**: The client identifier is an HTTPS URL that resolves to a JSON metadata document describing the client (recommended for cases where client and server have no prior relationship).
- **Dynamic Client Registration** (RFC 7591): Supported as a fallback for compatibility or specific deployments.

Implementations that support all options are encouraged to prefer pre-registration first, then Client ID Metadata Documents when supported, and finally dynamic registration if available.

## Security considerations

The specification frames MCP authorization as a transport-layer control for restricting access to MCP servers and emphasizes established OAuth security practices. It also distinguishes between HTTP transports (where OAuth-based authorization is expected) and STDIO transports (where credentials should be sourced from the environment), reflecting different threat models and deployment patterns.

## See also

- [Model Context Protocol](https://modelcontextprotocol.io/)
- OAuth 2.1
- OAuth 2.0 Protected Resource Metadata (RFC 9728)
- OAuth 2.0 Authorization Server Metadata (RFC 8414)
- OpenID Connect Discovery 1.0

## References

- Model Context Protocol. “Overview – Model Context Protocol (2025-11-25).” https://modelcontextprotocol.io/specification/2025-11-25/basic
- Model Context Protocol. “Authorization – Model Context Protocol.” https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
- IETF. “OAuth 2.0 Protected Resource Metadata (RFC 9728).” https://datatracker.ietf.org/doc/html/rfc9728
- IETF. “OAuth 2.0 Authorization Server Metadata (RFC 8414).” https://datatracker.ietf.org/doc/html/rfc8414
- IETF. “The OAuth 2.1 Authorization Framework (draft-ietf-oauth-v2-1-13).” https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-13
- OpenID Foundation. “OpenID Connect Discovery 1.0.” https://openid.net/specs/openid-connect-discovery-1_0.html
- IETF. “The OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750).” https://datatracker.ietf.org/doc/html/rfc6750
