---
title: MCP Registry
description: Official registry and API for discovery and publication of Model Context Protocol (MCP) servers.
---

# MCP Registry

The **MCP Registry** is an official registry service and API for publishing and discovering **Model Context Protocol (MCP)** servers. It provides a centralized catalog intended to improve server discoverability for MCP clients, while enabling downstream **sub-registries** (public or private) to ingest, filter, and augment registry data. The registry project and its API specification are open source.

## Overview

MCP servers expose tools and resources to MCP clients. The MCP Registry is designed to act as a “single source of truth” for *publicly available* servers, and to standardize how servers are distributed and discovered across the ecosystem. The registry is available at **https://registry.modelcontextprotocol.io/** and provides documentation and API endpoints for clients and server maintainers.

## Sub-registries

The MCP Registry is intended to coexist with other catalogs and marketplaces. It supports the idea of downstream registries that:

- Build **public** “marketplaces” that apply opinionated curation for specific clients or audiences.
- Provide **private** enterprise registries that mirror upstream data while applying internal security and compliance requirements.

## Moderation

The registry includes a community-driven moderation process. Community members can flag servers that violate moderation guidelines (for example, spam, malicious code, or impersonation), and maintainers can denylist entries and remove them from public access.

## Publishing and authentication

The registry repository documents multiple authentication mechanisms for publishing entries, including GitHub-based authentication and domain-ownership verification methods. It also describes namespace ownership validation for published server identifiers.

## History

In September 2025, the MCP project announced a preview launch of the MCP Registry and described it as an official registry for MCP servers.

## See also

- [[Model Context Protocol (MCP)]]

## References

1. Model Context Protocol. “Introducing the MCP Registry.” *modelcontextprotocol.info* (blog). https://modelcontextprotocol.info/blog/mcp-registry-preview/ (accessed 2026-02-27).
2. modelcontextprotocol. “modelcontextprotocol/registry.” *GitHub repository*. https://github.com/modelcontextprotocol/registry (accessed 2026-02-27).
3. Model Context Protocol. “Official MCP Registry.” https://registry.modelcontextprotocol.io/ (accessed 2026-02-27).
