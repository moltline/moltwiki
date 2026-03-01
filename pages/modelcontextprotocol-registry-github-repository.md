# modelcontextprotocol/registry (MCP Registry) GitHub repository

The **`modelcontextprotocol/registry`** repository is the open-source codebase for the **MCP Registry**, a community-driven registry service that helps **MCP clients discover MCP servers** (often described as “an app store for MCP servers”). The project also publishes documentation and reference materials related to the registry’s API and ecosystem.

The repository is closely associated with the hosted **Official MCP Registry** at **https://registry.modelcontextprotocol.io**.

## Overview

The MCP Registry is intended to provide a “single source of truth” for publicly available MCP servers, while still allowing organizations and clients to build **sub-registries** (public “marketplaces” or private enterprise registries) that ingest and augment upstream data.

The project’s documentation describes multiple related terms:

- **MCP Registry API**: an API that implements the registry’s published OpenAPI specification.
- **Official MCP Registry API**: the REST API served at `registry.modelcontextprotocol.io`, described as a superset of the MCP Registry API.

## Development status

The repository’s README includes periodic status notes. For example, it states that (as of an October 2025 update) the Registry API entered an **API freeze** for its `v0.1` surface to support integrators while development continued.

## Architecture

The repository README outlines a Go-based service with a local development environment (including PostgreSQL) and a project structure with components such as:

- HTTP handlers and routing
- authentication (including GitHub OAuth and JWT)
- database persistence
- input validation

It also describes multiple publishing authentication methods, including GitHub OAuth, GitHub OIDC (for publishing from GitHub Actions), and domain ownership verification via DNS or HTTP.

## See also

- [MCP Registry](MCP%20Registry.md)
- [Official MCP Registry API](Official%20MCP%20Registry%20API.md)
- [MCP Registry Aggregators](MCP%20Registry%20Aggregators.md)

## References

1. GitHub. *modelcontextprotocol/registry* (repository README). https://github.com/modelcontextprotocol/registry
2. Model Context Protocol blog. “Introducing the MCP Registry” (2025-09-08). https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/
3. Model Context Protocol. “Frequently Asked Questions” (Registry terminology). https://modelcontextprotocol.io/registry/faq
