# Model Context Protocol (MCP) Spec Updates from June 2025 (Auth0)

**Model Context Protocol (MCP) Spec Updates from June 2025** is an Auth0 blog post (published 2025) that summarizes security- and authorization-related changes in the MCP specification released on June 18, 2025. The post highlights MCP’s alignment with OAuth roles, the use of OAuth metadata discovery, and the requirement for OAuth Resource Indicators to reduce access-token misuse across servers.

## Background

MCP is a protocol for connecting AI applications to external tools and services. MCP’s authorization mechanism is optional, but when used over HTTP transports, the specification defines an OAuth-based flow for clients to access protected MCP servers on behalf of a resource owner.

## Topics covered in the Auth0 post

### MCP servers as OAuth resource servers

The post notes that the June 18, 2025 MCP spec clarifies that a protected MCP server acts as an OAuth resource server and can advertise associated authorization servers using OAuth Protected Resource Metadata.

### Authorization server discovery via OAuth metadata

According to the MCP authorization specification, MCP servers must implement OAuth 2.0 Protected Resource Metadata (RFC 9728) and clients must use it to discover authorization servers; authorization servers must publish OAuth Authorization Server Metadata (RFC 8414) and clients must use that metadata to determine endpoints and capabilities.

### Resource Indicators (RFC 8707)

The Auth0 post emphasizes the spec’s requirement that MCP clients implement OAuth Resource Indicators (RFC 8707) by including a `resource` parameter in authorization and token requests. This binds access tokens to an intended audience (the target MCP server) and is intended to mitigate token “mis-redemption” (using a token at the wrong resource).

## Reception

The post is an example of third-party commentary on MCP’s security direction and is frequently cited in discussions of securing MCP servers and clients with OAuth.

## References

- Auth0. "Model Context Protocol (MCP) Spec Updates from June 2025." (2025). https://auth0.com/blog/mcp-specs-update-all-about-auth/
- Model Context Protocol. "Authorization" (Specification, June 18, 2025). https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization
- IETF. "OAuth 2.0 Protected Resource Metadata" (RFC 9728). https://datatracker.ietf.org/doc/html/rfc9728
- IETF. "OAuth 2.0 Authorization Server Metadata" (RFC 8414). https://datatracker.ietf.org/doc/html/rfc8414
- IETF. "Resource Indicators for OAuth 2.0" (RFC 8707). https://www.rfc-editor.org/rfc/rfc8707.html
