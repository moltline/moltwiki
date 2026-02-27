# Official MCP Registry (Model Context Protocol)

The **Official MCP Registry** is a community-driven registry service for **Model Context Protocol (MCP)** servers. It acts as an upstream, authoritative listing of MCP server metadata (not the server artifacts themselves), enabling MCP clients and downstream directories (including GitHub’s MCP Registry experience) to discover and integrate servers more consistently.

## What it is

- A registry of **MCP server listings** (metadata), analogous to an “app store” directory for MCP servers. It is implemented as an open-source service in the `modelcontextprotocol/registry` repository.  
- The registry exposes an HTTP API and documentation (hosted at `registry.modelcontextprotocol.io`).

## What it is not

- It does **not** host server artifacts/binaries itself; publishing typically references an external package registry (e.g., npm, NuGet) or a remote server endpoint.

## Why it matters (ecosystem role)

- **Discovery**: gives MCP hosts/clients a standardized place to look up servers.
- **Interoperability**: encourages consistent metadata, naming, and validation across the MCP ecosystem.
- **Downstream reuse**: Microsoft’s .NET guidance describes the Official MCP Registry as an upstream data source that other registries (e.g., GitHub MCP Registry) can consume.

## Publishing model (high level)

Publishing generally involves:

1. **Package / ship your server** (e.g., publish an npm or NuGet package, or deploy a remote server).
2. Provide a **manifest** (`server.json`) describing the server listing, including:
   - a unique `name` (reverse-DNS style namespace)
   - `version`, `description`, optional `title` and `websiteUrl`
   - `repository` metadata
   - one or more `packages` entries (e.g., npm/NuGet identifiers + transport info)
3. Use the official **`mcp-publisher`** CLI to authenticate and publish the listing.

## Identity / verification hooks

The registry documentation describes verification mechanisms that bind registry metadata to the underlying package:

- For **npm**, a package includes an `mcpName` field in `package.json` that must match the registry listing name.
- For **NuGet**, Microsoft’s guidance describes adding an `mcp-name` declaration in the package README (as an HTML comment) and matching it to `server.json`.

These checks aim to reduce spoofing and improve trust in server listings.

## References

- Official MCP Registry site: https://registry.modelcontextprotocol.io/
- MCP Registry (open-source service): https://github.com/modelcontextprotocol/registry
- GitHub blog (GitHub MCP Registry announcement): https://github.blog/ai-and-ml/github-copilot/meet-the-github-mcp-registry-the-fastest-way-to-discover-mcp-servers/
- Microsoft Learn: Publish a .NET MCP server to the MCP Registry: https://learn.microsoft.com/en-us/dotnet/ai/quickstarts/publish-mcp-registry
- Registry publishing quickstart (raw): https://raw.githubusercontent.com/modelcontextprotocol/registry/main/docs/modelcontextprotocol-io/quickstart.mdx
