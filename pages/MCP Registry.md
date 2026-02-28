---
title: MCP Registry
---

# MCP Registry

The **MCP Registry** is the official, open catalog and API for publicly available **Model Context Protocol (MCP)** servers. It provides a standardized “source of truth” that MCP clients (and downstream “sub-registries”) can use to discover servers and fetch their metadata.

## What it is

- **A centralized listing** of MCP servers (often described as an “app store” for MCP servers) published by server maintainers.
- **An API + schemas** intended to make discovery and distribution consistent across the MCP ecosystem.
- **Open source infrastructure** maintained as an official MCP project, with documentation and a reference API specification.

## Why it matters

- **Discoverability:** clients can programmatically find servers and their connection/publishing metadata.
- **Standardization:** downstream registries/marketplaces can ingest upstream data and add opinionated curation.
- **Ecosystem scalability:** supports both public discovery and private/enterprise sub-registries that mirror the upstream API shape.

## Public vs. private sub-registries

The MCP Registry is designed to coexist with other registries:

- **Public sub-registries / marketplaces** (e.g., client-specific catalogs) can ingest from the official registry and enhance or filter entries.
- **Private sub-registries** can be implemented inside enterprises for security/privacy, while still benefiting from upstream schemas and tooling.

## Moderation and safety

The project documents moderation guidelines and allows community reporting of servers that violate policy (e.g., spam, malicious code, impersonation), with the ability for registry maintainers to denylist and remove entries.

## Key links

- Official registry: https://registry.modelcontextprotocol.io/
- Registry repository: https://github.com/modelcontextprotocol/registry
- Announcement: “Introducing the MCP Registry” (preview launch) https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/
- Live API docs: https://registry.modelcontextprotocol.io/docs

## References

- Model Context Protocol blog: “Introducing the MCP Registry” (2025-09-08) https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/
- GitHub repository: modelcontextprotocol/registry https://github.com/modelcontextprotocol/registry
- Official registry site https://registry.modelcontextprotocol.io/
