# Model Context Protocol (MCP) 2025-11-25 specification update

The **Model Context Protocol (MCP) 2025-11-25 specification update** is a dated release of the MCP specification published on **25 November 2025**. MCP is an open protocol for integrating LLM applications ("hosts") with external tools and data sources ("servers") over JSON-RPC 2.0.

## Overview

The 2025-11-25 document describes MCP’s base protocol (JSON-RPC message format, stateful connections, and capability negotiation) and the primary feature categories servers can expose to clients:

- **Resources** (context and data)
- **Prompts** (templated workflows)
- **Tools** (invocable functions)

It also describes client features that servers may request, including **sampling**, **roots**, and **elicitation**.

## Identity and authorization-related changes discussed in secondary coverage

Secondary coverage of the 2025-11-25 release highlighted identity and authorization topics relevant to deploying MCP in enterprise settings, including:

- Use of **OAuth 2.0 Client ID Metadata Documents (CIMD)** as a way for MCP clients (including AI agents) to identify themselves via a URL they control.
- Discussion of **authorization extensions** and enterprise governance patterns for agent access.
- Emphasis on explicit user consent and safer local-server execution practices.

## Security and trust considerations

The 2025-11-25 specification includes a dedicated section on **security and trust & safety**, emphasizing user consent and control, data privacy, tool safety, and controls around server-initiated LLM sampling.

## References

- Model Context Protocol. *Specification (2025-11-25).* Model Context Protocol. https://modelcontextprotocol.io/specification/2025-11-25
- Auth0. *MCP November 2025 Spec Update: CIMD, XAA, and Security.* Auth0 Blog. https://auth0.com/blog/mcp-november-2025-specification-update/
