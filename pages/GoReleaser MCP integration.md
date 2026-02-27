# GoReleaser MCP integration

**GoReleaser MCP integration** is an (experimental) feature in **GoReleaser** that can generate a **Model Context Protocol (MCP)** server manifest (`server.json`) and publish it to the **MCP Registry** as part of a release pipeline.

## Overview

GoReleaser is a release automation tool for building and distributing software artifacts. In GoReleaser v2.13, it introduced an **MCP** configuration section that can:

- generate a `server.json` manifest that conforms to the MCP server schema
- authenticate to the MCP Registry
- publish the manifest so an MCP server becomes discoverable to MCP clients

The GoReleaser documentation describes the MCP feature as **experimental**.

## Configuration

GoReleaser’s `mcp` configuration describes metadata that will be written into `server.json`, including:

- `name` (a unique server name, in reverse-DNS style)
- `title` and `description`
- `homepage`
- optional `repository` metadata
- one or more `packages` entries describing distribution and transport

The documentation shows package entries using `registry_type` values such as **npm** and **oci**, and transport types such as **stdio**.

## Publishing and validation

The MCP Registry is a metadata registry: it hosts MCP server metadata rather than the server’s package artifacts. The MCP Registry quickstart notes that the registry validates linkage between a server’s `server.json` metadata and the underlying package.

For npm packages, the quickstart describes adding an `mcpName` field to `package.json`, and requiring the `name` in `server.json` to match that `mcpName` value.

## Relationship to mcp-publisher

The MCP Registry quickstart describes **mcp-publisher** as the official CLI for publishing a `server.json` document to the registry. GoReleaser’s documentation notes that, when using its MCP integration, users do not need to install `mcp-publisher` or run it manually; GoReleaser performs generation and publishing as part of the release process.

## See also

- [[GoReleaser]]
- [[Model Context Protocol (MCP)]]
- [[MCP Registry]]
- [[mcp-publisher]]

## References

1. GoReleaser documentation. “Model Context Protocol (MCP) Server.” https://goreleaser.com/customization/mcp/
2. Model Context Protocol. “Quickstart: Publish an MCP Server to the MCP Registry.” https://modelcontextprotocol.io/registry/quickstart
