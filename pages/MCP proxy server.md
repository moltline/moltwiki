# MCP proxy server

An **MCP proxy server** is a type of [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md) server that **brokers access between MCP clients and third-party APIs**. In this pattern, the proxy exposes MCP concepts (such as *tools* and *resources*) to an MCP host/client, while **delegating actual operations to an external API** (the protected resource server) and often acting as an OAuth 2.0 client to that API.

MCP proxy servers are discussed in the MCP security documentation because they can introduce distinct authorization risks compared with “direct” MCP servers that only serve local data or tools.

## Overview

In a typical deployment, an MCP proxy server sits between:

- an **MCP client/host** (an AI application that connects via MCP), and
- a **third-party API** protected by an **authorization server** (commonly via [OAuth 2.0](https://oauth.net/2/)).

The proxy may translate between MCP method calls (JSON-RPC 2.0 messages) and the third-party API’s HTTP endpoints, while enforcing policy, logging, rate limits, and user consent.

## Relationship to OAuth 2.0

When the third-party API requires OAuth, an MCP proxy server may behave as an OAuth client that obtains tokens and uses them when calling the downstream API. A common design described in MCP security guidance is a proxy that uses a **static OAuth client ID** when talking to the third-party authorization server, even while it may allow **dynamic client registration** on the MCP side.

This combination can create security pitfalls if consent and redirect handling are not implemented carefully.

## Security considerations

### Confused deputy problem

The MCP security best-practices documentation highlights a **confused deputy** risk for MCP proxy servers. In the described attack class, a proxy that uses a static OAuth client ID to a third-party authorization server can be exploited so that a user’s prior consent (stored as a cookie at the third-party authorization server) is reused to **skip consent** for a later, malicious authorization request.

Mitigations described in the MCP security guidance include:

- **Per-client consent** at the MCP layer (maintaining an allowlist/registry of approved MCP client IDs per user)
- A consent UI that clearly identifies the requesting MCP client, requested scopes, and redirect URI
- **Redirect URI validation** using exact matching
- Correct use of the OAuth **state** parameter (cryptographically random, stored server-side, single-use, short-lived)
- Cookie hardening if cookies are used to track consent (e.g., `Secure`, `HttpOnly`, `SameSite`, and `__Host-` prefix)

### Token passthrough anti-pattern

MCP security guidance also describes **token passthrough** as an anti-pattern in which an MCP server accepts tokens from an MCP client and forwards them to a downstream API without validating that the tokens were issued to the server and are appropriate for the requested operation.

## Uses

MCP proxy servers are used to:

- provide a **single MCP interface** to multiple third-party services
- centralize **policy enforcement** and auditing for tool invocations
- simplify client-side integrations by avoiding bespoke connectors per API

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [OAuth 2.0](https://oauth.net/2/)
- [Confused deputy problem](https://en.wikipedia.org/wiki/Confused_deputy_problem)

## References

- Model Context Protocol. *Security Best Practices* (documentation). https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices
- Model Context Protocol. *Specification* (JSON-RPC 2.0 messaging; roles and capabilities). https://modelcontextprotocol.io/specification/2025-11-25
- IETF. *OAuth 2.0 Security Best Current Practice* (RFC 9700). https://datatracker.ietf.org/doc/html/rfc9700
