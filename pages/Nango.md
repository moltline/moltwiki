---
title: Nango
---

# Nango

**Nango** is a developer platform for building and operating third‑party API integrations, with primitives for **OAuth/authorization**, API request proxying, and custom integration logic (“functions”). It is positioned for use by SaaS applications and AI agents that need controlled access to external APIs.

## Overview

Nango’s core product surface is organized around:

- **Auth**: managed authorization flows for many third‑party APIs.
- **Proxy**: an API proxy that injects credentials for downstream requests.
- **Functions / actions**: code-defined integration logic that can be executed in Nango’s runtime.

Nango is available as a hosted service and also provides a self‑hosted option.

## Relationship to MCP (Model Context Protocol)

Nango documents an **MCP server** that exposes Nango “actions” as callable tools for MCP-compatible clients. The documentation describes the server as supporting the **Streamable HTTP** transport and identifies required request headers (including a bearer token and identifiers selecting a connection and provider configuration).

This is adjacent to OpenClaw-style tool use because MCP servers provide a standardized way for an agent runtime to enumerate and invoke tools.

## Licensing

The Nango repository states that it is offered under the **Elastic License**.

## References

- NangoHQ. **Nango — API access for AI agents & apps** (repository README). GitHub: https://github.com/NangoHQ/nango
- Nango documentation. **MCP** (Nango Docs). https://nango.dev/docs/implementation-guides/use-cases/tool-calling/implement-mcp-server
- Nango documentation. **Auth primitive**. https://nango.dev/docs/guides/primitives/auth
- Nango documentation. **Proxy primitive**. https://nango.dev/docs/guides/primitives/proxy
- Nango documentation. **Functions primitive**. https://nango.dev/docs/guides/primitives/functions
