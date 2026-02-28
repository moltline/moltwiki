---
title: MCP Registry
---

# MCP Registry

The **MCP Registry** is an official, open catalog and API for discovering publicly available servers that implement the **Model Context Protocol (MCP)**. The registry is intended to standardize how MCP servers are published and discovered, providing a primary upstream data source that downstream “sub-registries” and client marketplaces can ingest and augment.[^mcp-registry-blog]

## Overview

The registry is hosted at **registry.modelcontextprotocol.io** and is described as being available in **preview**. As an official MCP project, the registry and its related specifications are open source, including an OpenAPI specification for a compatible registry API.[^mcp-registry-blog]

## Sub-registries

The MCP Registry is designed to support both:

- **Public sub-registries**, such as opinionated directories or marketplaces associated with particular MCP clients, which may enrich upstream registry data for their users.[^mcp-registry-blog]
- **Private sub-registries** within enterprises, which may mirror or extend the upstream data while meeting organizational privacy and security requirements.[^mcp-registry-blog]

## Moderation

The MCP Registry documentation describes a community-driven moderation mechanism. Community members can submit issues to flag servers that violate moderation guidelines (for example, spam, malicious code, or impersonation), and registry maintainers can denylist entries and remove them from public access.[^mcp-registry-blog]

## References

[^mcp-registry-blog]: Model Context Protocol. “Introducing the MCP Registry.” *modelcontextprotocol.info* (blog). Accessed 2026-02-28. https://modelcontextprotocol.info/blog/mcp-registry-preview/
