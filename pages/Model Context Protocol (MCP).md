# Model Context Protocol (MCP)

The **Model Context Protocol** (**MCP**) is an open protocol for connecting AI/LLM applications to external data sources and tools through a standardized interface. It defines a client–server architecture (with “hosts” initiating connections) and uses JSON-RPC 2.0 messages to exchange context, prompts, and tool invocations.\[1\]

Anthropic announced MCP as an open standard intended to reduce the need for bespoke, per-integration connectors by providing a single protocol for “secure, two-way connections” between AI tools and data systems.\[2\]

**Type:** Open protocol / integration standard  
**Status:** Active  
**Website:** https://modelcontextprotocol.io  
**Specification:** https://modelcontextprotocol.io/specification/2025-11-25  
**Repository:** https://github.com/modelcontextprotocol/modelcontextprotocol

## Overview

MCP standardizes how applications can:

- Share contextual information with language models
- Expose tools and capabilities to AI systems
- Build composable integrations and workflows\[1\]

The specification describes three main roles:\[1\]

- **Hosts:** LLM applications that initiate connections
- **Clients:** connectors within the host application
- **Servers:** services that provide context and capabilities

## Protocol and features

The MCP base protocol uses **JSON-RPC 2.0** over stateful connections, including capability negotiation between client and server.\[1\]

The specification groups server-provided features into:\[1\]

- **Resources** (context and data)
- **Prompts** (templated messages/workflows)
- **Tools** (functions the model can execute)

It also defines optional client-provided features such as **sampling**, **roots**, and **elicitation**.\[1\]

## Security considerations

The specification notes that MCP can enable powerful capabilities (including arbitrary data access and code execution paths) and emphasizes user consent and control, data privacy, and safe tool invocation as key security principles for implementers.\[1\]

## History

Anthropic introduced MCP as an open standard and announced open-sourced specification/SDKs, local server support in Claude Desktop apps, and a repository of MCP servers.\[2\]

## See also

- Agent2Agent (A2A) Protocol
- A2UI

## References

1. Model Context Protocol — “Specification” (version 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
2. Anthropic. “Introducing the Model Context Protocol.” https://www.anthropic.com/news/model-context-protocol

## External links

- Model Context Protocol (GitHub organization). https://github.com/modelcontextprotocol
