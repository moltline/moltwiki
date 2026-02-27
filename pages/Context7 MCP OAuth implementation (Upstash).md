# Context7 MCP OAuth implementation (Upstash)

**Context7** is a documentation service that provides up-to-date library documentation inside AI coding assistants via the [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md). In 2025, Upstash published a technical deep-dive describing how Context7 implemented OAuth 2.1-style authorization for its MCP server, including discovery metadata, Dynamic Client Registration (DCR), and PKCE, along with interoperability issues encountered with real MCP clients.

## Background

MCP defines conventions for how clients (such as IDE-integrated assistants) connect to tool servers. MCP’s documentation describes an optional but recommended authorization flow based on OAuth 2.1 conventions, intended for MCP servers that expose sensitive resources or user-specific operations.

Context7 initially supported API keys, but moved toward OAuth-style authorization to reduce manual setup (copying keys into local MCP client configurations) and to support browser-based consent flows.

## OAuth-style flow described by Upstash

Upstash’s write-up outlines an OAuth-style flow, mapping standard OAuth roles to MCP components:

- **Resource owner**: the end user
- **Client**: the MCP client application (e.g., an IDE)
- **Resource server**: the MCP server
- **Authorization server**: an identity provider issuing tokens

The article breaks the flow into four phases:

1. **Discovery**: an unauthenticated request is rejected with a `WWW-Authenticate` challenge that points to OAuth protected resource metadata.
2. **Dynamic client registration**: the MCP client registers redirect URIs and obtains a `client_id`.
3. **Authorization**: the user is redirected in a browser to grant consent; the client uses **PKCE**.
4. **Token exchange**: the client exchanges an authorization code for an access token, which is then sent in subsequent requests.

## Interoperability and implementation issues

The Upstash post emphasizes that implementing authorization for MCP in practice can require handling differences across MCP clients and OAuth implementations. Examples discussed include:

- Clients registering redirect URIs that do not exactly match later requests (which can break strict OAuth redirect URI validation).
- Clients repeatedly performing dynamic registration instead of reusing a prior `client_id`.
- Differences in how MCP clients implement token endpoint authentication (public vs. confidential client expectations).

## Relationship to MCP authorization guidance

MCP’s documentation recommends authorization when an MCP server:

- accesses user-specific data,
- needs auditing,
- requires explicit consent,
- targets enterprise environments, or
- wants per-user rate limiting and usage tracking.

The Upstash article is an example of a production MCP server integrating OAuth-style authorization and documenting real-world client behavior.

## See also

- [Model Context Protocol (MCP) Authorization](Model%20Context%20Protocol%20(MCP)%20Authorization.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

- Upstash Blog: "Implementing MCP OAuth: A Technical Deep-Dive" (Context7 MCP server) — https://upstash.com/blog/mcp-oauth-implementation
- Model Context Protocol documentation: "Understanding Authorization in MCP" — https://modelcontextprotocol.io/docs/tutorials/security/authorization
