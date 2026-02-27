# mcp-publisher

**mcp-publisher** is a command-line tool for publishing **Model Context Protocol (MCP)** server metadata (via a `server.json` document) to the **MCP Registry**.

## Overview

The MCP Registry is described as a *metadata registry* (a “metaregistry”): it hosts structured metadata about MCP servers, while the server’s distributable artifacts are hosted in external package registries (for example, npm). The registry quickstart describes **mcp-publisher** as the official CLI used to:

- generate a `server.json` template (`mcp-publisher init`)
- authenticate to the registry (`mcp-publisher login`)
- publish metadata to the registry (`mcp-publisher publish`)

The quickstart also describes a validation linkage between registry metadata and the underlying package: for npm packages, the registry expects an `mcpName` field in `package.json`, and the `name` in `server.json` must match it.

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
2. modelcontextprotocol/registry. “MCP Registry” (README). https://github.com/modelcontextprotocol/registry
3. Homebrew Formulae. “mcp-publisher.” https://formulae.brew.sh/formula/mcp-publisher
