# Context7 MCP OAuth implementation (Upstash)

**Context7** is a documentation service that provides up-to-date library documentation inside AI coding assistants via the [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md). In 2025, Upstash published a technical deep-dive describing how Context7 implemented an OAuth-style authorization flow for its MCP server, including discovery via protected resource metadata, Dynamic Client Registration (DCR), and PKCE, plus interoperability issues encountered with real MCP clients. https://upstash.com/blog/mcp-oauth-implementation

## Background

MCP defines conventions for how clients (such as IDE-integrated assistants) connect to tool servers. For HTTP transports, MCP defines an optional authorization mechanism based on a subset of OAuth-related specifications (OAuth 2.1 draft, Authorization Server Metadata, Dynamic Client Registration, and Protected Resource Metadata). https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization

Context7 initially supported API keys, but moved toward OAuth-style authorization to reduce manual setup (copying keys into local MCP client configurations) and to support browser-based consent flows. https://upstash.com/blog/mcp-oauth-implementation

## Terminology mapping (OAuth ↔ MCP)

Upstash’s write-up maps standard OAuth roles to MCP components:

- **Resource owner**: the end user
- **Client**: the MCP client application (e.g., an IDE)
- **Resource server**: the MCP server
- **Authorization server**: the identity provider issuing tokens

## OAuth-style flow described by Upstash

The article breaks the flow into four phases, which line up with common OAuth 2.0/2.1 patterns:

1. **Discovery (authorization server discovery via resource metadata)**
   - The client attempts an unauthenticated request to the MCP server.
   - The server responds `401 Unauthorized` and uses the `WWW-Authenticate` header to point the client at a *Protected Resource Metadata* document (per RFC 9728). https://www.rfc-editor.org/rfc/rfc9728
2. **Dynamic client registration (DCR)**
   - The MCP client registers its redirect URIs at the authorization server and receives a `client_id` (per RFC 7591). https://www.rfc-editor.org/rfc/rfc7591
3. **Authorization (Authorization Code + PKCE)**
   - The user is redirected in a browser to grant consent.
   - The client uses PKCE to mitigate authorization-code interception for public clients (per RFC 7636). https://www.rfc-editor.org/rfc/rfc7636
4. **Token exchange**
   - The client exchanges the authorization code for an access token at the token endpoint.
   - The access token is then sent on subsequent MCP requests (typically using the `Authorization: Bearer ...` header).

### Discovery details (what “resource metadata” means)

In the Upstash flow, the MCP server advertises an `.well-known` URL for OAuth Protected Resource Metadata (e.g., `/.well-known/oauth-protected-resource`) via `WWW-Authenticate`. The metadata document includes (at minimum) the protected resource identifier and one or more `authorization_servers` values, which tell the client where to discover the authorization server’s endpoints. https://upstash.com/blog/mcp-oauth-implementation

MCP’s authorization specification for HTTP explicitly requires this discovery mechanism: MCP servers **MUST** implement OAuth 2.0 Protected Resource Metadata (RFC 9728), and MCP clients **MUST** use it for authorization server discovery. https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization

## Interoperability and implementation issues

The Upstash post emphasizes that implementing authorization for MCP in practice can require handling differences across MCP clients and OAuth implementations. Examples discussed include:

- **Redirect URI mismatches**: clients may register one redirect URI string but later use a slightly different one (e.g., `127.0.0.1` vs `localhost`), which breaks strict exact-match validation.
- **Repeated DCR**: some clients repeatedly perform dynamic registration instead of reusing a stored `client_id`.
- **Token endpoint client authentication expectations**: MCP clients are typically public clients, but implementations may differ in how they expect to authenticate at the token endpoint.

(See the Upstash post for concrete client-specific behaviors and examples.) https://upstash.com/blog/mcp-oauth-implementation

## Relationship to MCP authorization guidance

MCP’s authorization spec frames the goal as transport-level authorization for HTTP-based MCP servers, enabling clients to make requests “on behalf of resource owners.” It also notes that authorization is optional for MCP implementations, and that STDIO transports should instead retrieve credentials from the environment. https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization

## See also

- [Model Context Protocol (MCP) Authorization](Model%20Context%20Protocol%20(MCP)%20Authorization.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

- Upstash Blog: “Implementing MCP OAuth: A Technical Deep-Dive” (Context7 MCP server) — https://upstash.com/blog/mcp-oauth-implementation
- Model Context Protocol spec (Authorization, HTTP transport) — https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization
- RFC 9728: OAuth 2.0 Protected Resource Metadata — https://www.rfc-editor.org/rfc/rfc9728
- RFC 7591: OAuth 2.0 Dynamic Client Registration Protocol — https://www.rfc-editor.org/rfc/rfc7591
- RFC 7636: Proof Key for Code Exchange (PKCE) — https://www.rfc-editor.org/rfc/rfc7636
