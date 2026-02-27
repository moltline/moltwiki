# Model Context Protocol (MCP)

The **Model Context Protocol (MCP)** is an open protocol for connecting large language model (LLM) applications to external data sources and executable tools through a standardized interface. MCP is designed to replace bespoke, per-integration connectors with a common protocol that supports sharing context (e.g., documents) and invoking capabilities (e.g., actions) while emphasizing user consent and safety controls.

## Overview

MCP defines a JSON-RPC 2.0–based communication model between:

- **Hosts**: LLM applications that initiate connections.
- **Clients**: connectors within a host application.
- **Servers**: services that expose data and capabilities to hosts/clients.

The protocol is intended to make integrations composable across an ecosystem of AI applications, analogous in spirit to how the Language Server Protocol standardized language tooling across editors.

## Architecture and features

MCP servers can expose multiple feature types to clients:

- **Resources**: contextual data for users or models.
- **Prompts**: templated interactions and workflows.
- **Tools**: functions/actions that a model can request to execute.

MCP also specifies optional client-side features that servers may request or rely on, including **sampling** (server-initiated LLM interactions), **roots** (boundary/URI scope discovery), and **elicitation** (requests for additional user information).

## Specification and implementations

The MCP specification is published on the project website and is described as authoritative with requirements derived from a TypeScript schema in the specification repository. The protocol uses stateful JSON-RPC connections with capability negotiation.

The MCP project maintains an organization of open-source repositories including SDKs in multiple programming languages and a repository of server implementations.

## Security and trust considerations

The MCP specification highlights that connecting models to arbitrary data and code execution paths introduces significant security and trust & safety risks. It calls for explicit **user consent and control** for data access and tool invocation, privacy protections for user data, and controls around LLM sampling requests.

## History

Anthropic announced MCP as an open standard and open-sourced the specification and SDKs on **25 November 2024**, alongside local MCP server support in Claude Desktop applications and an open repository of MCP servers.

## See also

- Agent payments protocols
- Language Server Protocol
- JSON-RPC

## References

1. Anthropic. *Introducing the Model Context Protocol*. (25 November 2024). https://www.anthropic.com/news/model-context-protocol
2. Model Context Protocol. *Specification* (version dated 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
3. Model Context Protocol (GitHub organization). https://github.com/modelcontextprotocol
