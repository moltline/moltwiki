# MCPB

**MCPB** is a package format for distributing **Model Context Protocol (MCP)** servers as a single artifact (typically a file with the `.mcpb` extension) that can be referenced from the **MCP Registry**.

## Overview

The MCP Registry supports multiple package types for MCP servers. For MCPB packages, the registry documentation describes a workflow where an MCP server’s `server.json` metadata can point at an `.mcpb` artifact hosted on a release page (for example, GitHub Releases or GitLab Releases).

In the registry’s `server.json` metadata, MCPB packages use `registryType: "mcpb"` within the `packages` array. The metadata includes:

- an `identifier` URL pointing to the `.mcpb` artifact
- a `fileSha256` field containing the SHA-256 hash of the artifact
- a `transport` object (for example, `{"type": "stdio"}`)

The registry documentation notes that the MCP Registry itself does not validate `fileSha256`, but MCP clients validate the hash before installation to check integrity.

## Verification rules (registry)

The MCP Registry documentation describes additional rules for MCPB packages:

- The package URL (`identifier`) must contain the string `"mcp"` (for example, via the `.mcpb` extension or repository name).
- `server.json` metadata must include `fileSha256`.

## See also

- [[Model Context Protocol (MCP)]]
- [[MCP Registry]]
- [[mcp-publisher]]

## References

1. Model Context Protocol. “MCP Registry Supported Package Types.” https://modelcontextprotocol.io/registry/package-types
