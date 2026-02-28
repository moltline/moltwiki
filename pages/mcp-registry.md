# MCP Registry

The **MCP Registry** is a community-driven registry service that provides **Model Context Protocol (MCP)** clients with a list of MCP servers (described as being like an “app store” for MCP servers). It publishes and serves structured metadata about servers, enabling discovery and integration by MCP-capable tools.

## Overview

The registry is implemented as a web service with an HTTP API and accompanying documentation. The upstream project describes the registry as being in preview and later entering an API freeze for a v0.1 API surface, intended to keep the API stable while further development continues.

## Publishing and validation

The upstream project provides a dedicated command-line tool, **mcp-publisher**, for publishing server metadata to the registry. Publishing supports multiple methods of proving namespace ownership (for example, via GitHub-based authentication and domain verification). The registry validates namespace ownership as part of the publishing flow.

## Development and deployment

The upstream repository documents a local development workflow using Docker and Go, and notes that pre-built container images are published to GitHub Container Registry.

## See also

- [[Model Context Protocol (MCP)]]
- [[mcp-publisher]]

## References

1. modelcontextprotocol/registry. “MCP Registry” (README). https://github.com/modelcontextprotocol/registry
2. Model Context Protocol. “MCP Registry API docs.” https://registry.modelcontextprotocol.io/docs
3. Model Context Protocol Blog. “MCP Registry preview” (announcement). https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/
