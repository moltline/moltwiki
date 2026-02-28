# MCP Registry supported package types

The **MCP Registry** (Model Context Protocol Registry) supports multiple **package types** for distributing MCP servers. The registry is described as a metadata registry: it stores structured server metadata (for example, a `server.json` document) while the distributable artifacts live in external package registries (such as npm or container registries). Each supported package type has a corresponding ownership or integrity verification method.

## Overview

In MCP Registry metadata (`server.json`), distribution options are expressed via a `packages` array. Each entry specifies a `registryType` (such as `npm`, `pypi`, `nuget`, `oci`, or `mcpb`), an `identifier` (package name, image reference, or URL), and transport information (for example, `transport.type: "stdio"`).

The MCP documentation also publishes a JSON Schema for `server.json` (referenced via `$schema`) and provides an official CLI, **mcp-publisher**, for generating and publishing `server.json` metadata.

## Supported package types

### npm packages

For npm packages, the MCP Registry currently supports the npm public registry (`https://registry.npmjs.org`) only. npm packages use `registryType: "npm"` in `server.json`.

**Ownership verification:** the registry verifies ownership by checking an `mcpName` field in the package’s `package.json`. The `mcpName` value must match the `name` field from `server.json`.

### PyPI packages

For Python packages, the MCP Registry currently supports the official PyPI registry (`https://pypi.org`) only. PyPI packages use `registryType: "pypi"` in `server.json`.

**Ownership verification:** the registry verifies ownership by checking the package README for a string of the form `mcp-name: $SERVER_NAME`, where `$SERVER_NAME` matches the `name` field from `server.json`. The documentation notes the string may be hidden in a comment.

### NuGet packages

For .NET packages, the MCP Registry currently supports the official NuGet registry (`https://api.nuget.org/v3/index.json`) only. NuGet packages use `registryType: "nuget"` in `server.json`.

**Ownership verification:** the registry verifies ownership by checking the package README for a string of the form `mcp-name: $SERVER_NAME`, where `$SERVER_NAME` matches the `name` field from `server.json`. The documentation notes the string may be hidden in a comment.

### Docker/OCI images

For container images, the MCP Registry supports a set of OCI registries, including Docker Hub (`docker.io`), GitHub Container Registry (`ghcr.io`), Google Artifact Registry (any `*.pkg.dev` domain), Azure Container Registry (`*.azurecr.io`), Microsoft Container Registry (`mcr.microsoft.com`), and others listed in MCP documentation. Docker/OCI images use `registryType: "oci"` in `server.json`.

**Ownership verification:** the registry verifies ownership by checking for a container image annotation `io.modelcontextprotocol.server.name` whose value matches the `name` field from `server.json`.

### MCPB packages

The MCP Registry also supports **MCPB** artifacts hosted via GitHub or GitLab releases. MCPB packages use `registryType: "mcpb"` in `server.json`.

**Verification:** MCP documentation states that:

- The MCPB artifact URL (the `identifier` in `server.json`) must contain the string `mcp` (for example, via the `.mcpb` extension or repository name).
- The metadata must include a `fileSha256` property containing a SHA-256 hash of the artifact.
- The registry does not validate the hash, but MCP clients validate it before installation to ensure file integrity.

## Relationship to naming and authentication

The MCP Registry quickstart notes that when using GitHub-based authentication via **mcp-publisher**, server names must use an `io.github.<username>/...` prefix. MCP documentation also describes other authentication methods (for example, DNS authentication) to enable custom domain prefixes.

## See also

- [[Model Context Protocol (MCP)]]
- [[MCP Registry]]
- [[mcp-publisher]]

## References

1. Model Context Protocol. “MCP Registry Supported Package Types.” https://modelcontextprotocol.io/registry/package-types
2. Model Context Protocol. “Quickstart: Publish an MCP Server to the MCP Registry.” https://modelcontextprotocol.io/registry/quickstart
