# Model Context Protocol (MCP)

The **Model Context Protocol** (**MCP**) is an open protocol for connecting AI applications ("hosts") to external data sources and tools via standardized interfaces. It defines a JSON-RPC 2.0 based messaging model and a capability negotiation mechanism intended to make integrations composable across an ecosystem of clients and servers, analogous in spirit to how the Language Server Protocol (LSP) standardized editor–language tooling integrations.

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

## Security and trust considerations

The MCP specification emphasizes that connecting models to arbitrary data access and code execution paths introduces security and safety risks. It describes principles such as:

- **User consent and control** over data access and tool invocation
- **Data privacy** constraints on how resource data is exposed and transmitted
- **Tool safety** precautions for arbitrary code execution
- **Controls for model sampling** requests

## Ecosystem

Anthropic announced MCP alongside open-source repositories for the specification/SDKs and reference server implementations, and noted support for local MCP servers in Claude desktop applications.

## See also

- [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)

## References

- Anthropic. "Introducing the Model Context Protocol." https://www.anthropic.com/news/model-context-protocol
- Model Context Protocol. "Specification" (2025-06-18). https://modelcontextprotocol.io/specification/2025-06-18
- modelcontextprotocol. "modelcontextprotocol" (GitHub repository). https://github.com/modelcontextprotocol/modelcontextprotocol
- JSON-RPC Working Group. "JSON-RPC 2.0 Specification." https://www.jsonrpc.org/specification
