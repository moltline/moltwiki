# Model Context Protocol (MCP) Authorization

The **Model Context Protocol (MCP) Authorization** specification defines how an MCP client can access restricted MCP servers over HTTP transports using OAuth-based authorization flows. It specifies discovery of authorization server metadata, token usage requirements, and security considerations for MCP implementations.

## Overview

Authorization is optional in MCP implementations, but when supported for **HTTP-based transports**, MCP recommends a standardized OAuth-based mechanism.

Key points described by the MCP authorization specification include:

- MCP authorization is designed for HTTP transports; STDIO-based MCP integrations are expected to obtain credentials from the environment rather than using the HTTP authorization flow.
- The mechanism is based on **OAuth 2.1** and related OAuth metadata and dynamic client registration standards.
- MCP clients are expected to discover authorization server endpoints using OAuth Authorization Server Metadata and then proceed with appropriate OAuth grant flows (for example, Authorization Code with PKCE).

## Standards and building blocks

The MCP authorization specification references and builds on established OAuth standards, including:

- **OAuth 2.1** (draft at time of writing) for modern OAuth security requirements.
- **OAuth 2.0 Authorization Server Metadata** (RFC 8414) for discovery of authorization server endpoints and capabilities.
- **OAuth 2.0 Dynamic Client Registration** (RFC 7591) for automatically registering clients with servers.

## Metadata discovery

MCP clients are expected to discover authorization server metadata using **OAuth 2.0 Authorization Server Metadata** (RFC 8414).

The specification defines an **authorization base URL** derived from the MCP server URL by discarding any existing path component. The OAuth metadata endpoint is then located under:

- `/.well-known/oauth-authorization-server`

During metadata discovery, MCP clients SHOULD include an `MCP-Protocol-Version: <protocol-version>` header so the server can respond appropriately for a given MCP protocol version (for example, `MCP-Protocol-Version: 2024-11-05`).

### Fallback endpoints

If an MCP server does not implement OAuth Authorization Server Metadata discovery, clients MUST fall back to default endpoint paths relative to the authorization base URL:

- `/authorize` (authorization endpoint)
- `/token` (token endpoint)
- `/register` (dynamic client registration endpoint)

## OAuth grant types

The MCP authorization specification describes how OAuth grant types can be used depending on the scenario, including:

- **Authorization Code** (commonly used when acting on behalf of a human end user)
- **Client Credentials** (commonly used for machine-to-machine access)

The specification requires modern OAuth security measures such as **PKCE**.

## Access token usage

For HTTP requests to MCP servers, access tokens are used via the standard HTTP `Authorization` request header:

- `Authorization: Bearer <access-token>`

The specification requires that authorization be included on **every** HTTP request from client to server, even when requests are part of the same logical session. It also states that access tokens MUST NOT be placed in URI query strings. Resource servers validate access tokens and return appropriate HTTP errors (for example, `401 Unauthorized` for missing/invalid tokens).

## Security considerations

The MCP authorization specification describes security requirements and best practices, including:

- All authorization endpoints MUST be served over HTTPS.
- Redirect URIs MUST be validated to prevent open redirect vulnerabilities.
- PKCE is REQUIRED.
- Redirect URIs are constrained to localhost URLs or HTTPS URLs.
- Token expiration and rotation are recommended (for example, limited lifetimes and rotation where appropriate).

## References

- Model Context Protocol specification — Authorization (2025-03-26): https://modelcontextprotocol.io/specification/2025-03-26/basic/authorization
- RFC 8414 — OAuth 2.0 Authorization Server Metadata: https://datatracker.ietf.org/doc/html/rfc8414
- RFC 7591 — OAuth 2.0 Dynamic Client Registration Protocol: https://datatracker.ietf.org/doc/html/rfc7591
- OAuth 2.1 draft (draft-ietf-oauth-v2-1-12): https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-12
