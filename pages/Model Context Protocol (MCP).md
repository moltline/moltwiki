# Model Context Protocol (MCP)

The **Model Context Protocol** (**MCP**) is an open protocol for connecting AI applications ("hosts") to external data sources and tools via standardized interfaces. MCP uses **JSON-RPC 2.0** messages over stateful connections with **capability negotiation**, aiming to make integrations composable across an ecosystem of clients and servers—often compared (conceptually) to how the Language Server Protocol (LSP) standardized editor–language tooling integrations.

## Overview

MCP is designed to reduce the need for bespoke, per-tool connectors by providing a common protocol for:

- **Resources** (context and data made available to the host/model)
- **Tools** (functions that can be invoked by an AI system)
- **Prompts** (templated workflows/messages)

The specification describes roles commonly involved in an MCP connection:

- **Hosts**: LLM applications that initiate connections
- **Clients**: connectors within the host application
- **Servers**: services that provide context and capabilities

## Protocol characteristics

- **Message format**: JSON-RPC 2.0 messages
- **Connections**: stateful connections with capability negotiation
- **Feature sets**: servers may expose resources, prompts, and tools; clients may support features such as sampling, roots, and elicitation

## Specification evolution (selected changes)

MCP is versioned via dated specification revisions. Notable changes across 2025 revisions include:

- **2025-03-26**: Added an authorization framework based on **OAuth 2.1**; replaced the previous HTTP+SSE transport with a **Streamable HTTP** transport; added JSON-RPC batching; and introduced richer tool annotations (e.g., read-only vs destructive).
- **2025-06-18**: Removed JSON-RPC batching; added **structured tool output** and **resource links** in tool results; expanded the client/server interaction model with **elicitation**; strengthened OAuth guidance (e.g., treating MCP servers as OAuth resource servers and requiring **RFC 8707** resource indicators); and required an **MCP-Protocol-Version** header on subsequent HTTP requests after version negotiation.

These revisions reflect an emphasis on clarifying transport behavior and tightening security/authorization guidance for real-world deployments.

## Security and trust considerations

The MCP specification emphasizes that connecting models to arbitrary data access and code execution paths introduces security and safety risks. It highlights principles such as:

- **User consent and control** over data access and tool invocation
- **Data privacy** constraints on how resource data is exposed and transmitted
- **Tool safety** precautions for arbitrary code execution
- **Controls for model sampling** requests

## Ecosystem

Anthropic announced MCP alongside open-source repositories for the specification/SDKs and reference server implementations, and noted support for local MCP servers in Claude desktop applications.

## See also

- [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)
- [JSON-RPC 2.0](https://www.jsonrpc.org/specification)

## References

- Anthropic. "Introducing the Model Context Protocol." https://www.anthropic.com/news/model-context-protocol
- Model Context Protocol. "Specification" (2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol. "Key Changes" (2025-03-26). https://modelcontextprotocol.io/specification/2025-03-26/changelog
- Model Context Protocol. "Key Changes" (2025-06-18). https://modelcontextprotocol.info/specification/2025-06-18/changelog/
- modelcontextprotocol (GitHub organization). https://github.com/modelcontextprotocol
