# mcp-publisher

**mcp-publisher** is a command-line tool for publishing **Model Context Protocol (MCP)** server metadata (via a `server.json` document) to the **MCP Registry**.

## Overview

The MCP Registry is described as a *metadata registry* (a “metaregistry”): it hosts structured metadata about MCP servers, while a server’s distributable artifacts are hosted in external package registries (for example, npm). The registry quickstart describes **mcp-publisher** as the official CLI used to:

- generate a `server.json` template (`mcp-publisher init`)
- authenticate to the registry (`mcp-publisher login`)
- publish metadata to the registry (`mcp-publisher publish`)

The quickstart also describes a validation linkage between registry metadata and the underlying package. For npm packages, this includes:

- adding an `mcpName` field to `package.json`
- ensuring the `name` in `server.json` matches the `mcpName` in `package.json`

## server.json schema and package metadata

The quickstart’s example `server.json` includes a `$schema` URL and fields such as `name`, `description`, `repository`, `version`, and a `packages` array. The example package entry includes a `registryType` (e.g., `npm`), an `identifier` (the package name), a `version`, and a `transport` (e.g., `{ "type": "stdio" }`). The example also shows an optional `environmentVariables` array for documenting required configuration (including marking variables as secrets).

## Authentication and naming

The registry documentation notes that the authentication method determines the required namespace format for your server name in `server.json`:

- **GitHub-based authentication** requires names of the form `io.github.username/*` or `io.github.orgname/*`.
- **Domain-based authentication** requires names of the form `com.example.*/*` (reverse-DNS).

## Commands

The registry quickstart shows `mcp-publisher --help` with a command set including:

- `init` — create a `server.json` template
- `login` / `logout` — manage registry authentication
- `publish` — publish `server.json` to the registry

(Exact behavior and flags may vary by version.)

## Distribution

The MCP documentation describes installing **mcp-publisher** via a pre-built binary or Homebrew. Homebrew distributes it as the `mcp-publisher` formula.

## See also

- [[Model Context Protocol (MCP)]]
- [[MCP Registry]]

## References

1. Model Context Protocol. “Quickstart: Publish an MCP Server to the MCP Registry.” https://modelcontextprotocol.io/registry/quickstart
2. Model Context Protocol. “How to Authenticate When Publishing to the Official MCP Registry.” https://modelcontextprotocol.io/registry/authentication
3. modelcontextprotocol/registry. “MCP Registry” (README). https://github.com/modelcontextprotocol/registry
4. Homebrew Formulae. “mcp-publisher.” https://formulae.brew.sh/formula/mcp-publisher
