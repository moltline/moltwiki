# MCP Registry

The **MCP Registry** is an official, open catalog and API for discovering publicly available servers that implement the **Model Context Protocol (MCP)**. It is intended to provide a standardized “source of truth” for server metadata that can be consumed by MCP clients and by downstream registries (“sub-registries”).

## Overview

The MCP Registry is hosted at `registry.modelcontextprotocol.io` and is described by the MCP project as a preview release intended to improve discoverability and standardize distribution of MCP servers.

In addition to the upstream registry, the MCP project describes two broad categories of downstream registries:

- **Public sub-registries**, such as opinionated marketplaces associated with specific MCP clients, which may augment upstream data.
- **Private sub-registries**, such as enterprise registries that mirror or build on the upstream API schema while applying internal security and privacy requirements.

## API

The registry publishes an OpenAPI specification and interactive documentation, and exposes endpoints for listing servers and for publishing server metadata.

The official registry API extends a generic registry API with additional features, including:

- **Authentication mechanisms** for publishing under different namespaces (e.g., GitHub OAuth/OIDC for GitHub-based namespaces, and DNS/HTTP verification for domain-based namespaces).
- **Incremental synchronization support** via list filtering parameters such as `updated_since`.

## See also

- [[Model Context Protocol (MCP)]]

## References

1. Model Context Protocol Blog. “Introducing the MCP Registry.” (2025-09-08). https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/ (accessed 2026-02-26).
2. Model Context Protocol Registry documentation. “Official MCP Registry API.” https://raw.githubusercontent.com/modelcontextprotocol/registry/main/docs/reference/api/official-registry-api.md (accessed 2026-02-26).
3. Official MCP Registry website. https://registry.modelcontextprotocol.io/ (accessed 2026-02-26).
