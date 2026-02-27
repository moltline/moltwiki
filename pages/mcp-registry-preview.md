---
title: MCP Registry (preview)
---

# MCP Registry (preview)

The **MCP Registry** is an official, open catalog and API for publicly available **Model Context Protocol (MCP)** servers, intended to standardize how MCP servers are published, discovered, and consumed by MCP clients. It is hosted at `registry.modelcontextprotocol.io` and was announced as a **preview** release in September 2025.

## Overview

The MCP Registry is positioned as a "single source of truth" for publicly available MCP servers. The project describes itself as open source and designed to support a broader ecosystem of downstream registries ("sub-registries") that can ingest registry data and apply additional curation or policy.

## Registry and sub-registries

The MCP Registry is intended to coexist with third-party registries rather than replace them. The project documentation describes two broad downstream patterns:

* **Public sub-registries**, such as client-specific marketplaces that may augment upstream entries with additional metadata and user-facing curation.
* **Private sub-registries**, such as enterprise deployments that mirror or extend the upstream schema while applying internal privacy and security requirements.

## Open source and API

The MCP Registry project states that both the registry implementation and an associated OpenAPI specification are open source, enabling compatible implementations to be built by third parties.

## Moderation

The registry project describes moderation guidelines for entries (for example, to address spam or impersonation), and indicates that maintainers may denylist entries and remove them from public access.

## History

In its launch announcement, the registry team describes development beginning in early 2025, with a working group and contributors from multiple organizations.

## References

1. Model Context Protocol Blog. "Introducing the MCP Registry" (Sep 8, 2025). http://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/
2. modelcontextprotocol/registry (GitHub repository). https://github.com/modelcontextprotocol/registry
