# MCP Registry API

The **MCP Registry API** is a REST API for discovering metadata about **Model Context Protocol (MCP)** servers listed in the **Official MCP Registry**.

The registry API is intended for *discovery*: it returns structured metadata (for example, server name, description, repository URL, and version) rather than hosting the server’s executable artifacts.

## Base URL and versioning

The registry is served from:

- `https://registry.modelcontextprotocol.io/`

Examples in the registry documentation use a versioned path prefix (for example, `/v0`).

## Listing and searching servers

The official registry API defines a `GET /v0/servers` endpoint for listing servers.

Common query parameters include:

- `limit` — maximum number of items to return
- `cursor` — an opaque pagination cursor returned by the API
- `search` — a search string for filtering results

Example: list 10 servers

```bash
curl "https://registry.modelcontextprotocol.io/v0/servers?limit=10"
```

Example: search for servers matching “sql”

```bash
curl "https://registry.modelcontextprotocol.io/v0/servers?search=sql&limit=1"
```

## Response shape (high level)

Responses are JSON documents that include a list of servers and associated metadata. Server objects include a `$schema` URL and fields such as `name`, `description`, `repository`, and `version`.

## See also

- [[Model Context Protocol (MCP)]]
- [[MCP Registry]]
- [[mcp-publisher]]

## References

1. modelcontextprotocol/registry. “Official Registry API (OpenAPI spec).” https://github.com/modelcontextprotocol/registry/blob/main/docs/reference/api/official-registry-api.md
2. Model Context Protocol. “MCP Registry” documentation. https://modelcontextprotocol.io/registry/
3. Nordic APIs. “Getting Started With the Official MCP Registry API.” (Nov 19, 2025). https://nordicapis.com/getting-started-with-the-official-mcp-registry-api/
