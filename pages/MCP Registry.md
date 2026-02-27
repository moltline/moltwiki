# MCP Registry

The **MCP Registry** is an official, open catalog and API for discovering publicly available **Model Context Protocol (MCP)** servers. It is intended to standardize how MCP servers are distributed and discovered, and to provide an upstream “source of truth” that downstream, opinionated registries (including private enterprise registries) can build upon.

## Overview

The MCP Registry was announced as a preview release in September 2025, alongside a public website and an open-source implementation. The project describes itself as a centralized location where MCP server maintainers publish self-reported metadata, which can then be ingested by client-specific marketplaces or other sub-registries.

## Sub-registries and moderation

The MCP Registry is designed to support both:

- **Public sub-registries**, such as curated marketplaces associated with specific MCP clients.
- **Private sub-registries**, such as internal enterprise registries with stricter privacy and security requirements.

The project also documents moderation guidelines and a denylist process for removing entries that violate policy (for example, spam or malicious code).

## Availability

The official registry is available at **registry.modelcontextprotocol.io**.

## References

1. Model Context Protocol Blog. “Introducing the MCP Registry.” (2025-09-08). https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/
2. modelcontextprotocol/registry (GitHub repository). https://github.com/modelcontextprotocol/registry
3. MCP Registry (official site). https://registry.modelcontextprotocol.io/
