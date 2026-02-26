# Model Context Protocol (MCP)

The **Model Context Protocol** (MCP) is an open protocol for connecting large language model (LLM) applications to external **data sources** and **tools** through a standardized interface.

MCP defines a message-based architecture (using **JSON-RPC 2.0**) in which an LLM “host” application connects to one or more servers that expose resources and tool capabilities.

## Overview

### Motivation
Many LLM applications require bespoke connectors for each new system (e.g., file stores, ticketing systems, databases, developer tools). MCP proposes a common protocol to reduce integration fragmentation and make tool/data access more composable across applications.

### Architecture
The MCP specification describes three primary roles:

- **Hosts**: LLM applications that initiate and manage connections.
- **Clients**: connectors inside the host that implement the protocol.
- **Servers**: services that provide context and capabilities to the host.

Communication uses **stateful JSON-RPC 2.0** messages, with capability negotiation between client and server.

### Core concepts
The specification groups server-provided functionality into:

- **Resources**: contextual data made available to the host/model.
- **Prompts**: templated messages and workflows.
- **Tools**: callable functions the model can ask the host to invoke.

The spec also describes optional client-provided features that servers may request, including **sampling** (server-initiated LLM interactions), **roots** (boundary discovery for URIs/filesystems), and **elicitation** (requests for additional user information).

## Security and trust considerations
The MCP specification emphasizes that protocol-level interoperability can expose powerful capabilities (including arbitrary data access and code execution paths) and highlights principles such as **user consent and control**, **data privacy**, and **tool safety**. It notes that tool descriptions and annotations should be treated as untrusted unless obtained from a trusted server.

## Relationship to autonomous agent ecosystems
MCP is often discussed alongside “agentic” application patterns because it standardizes how an LLM application can:

- discover available tools and data sources,
- request tool execution through a controlled host runtime,
- and compose workflows across multiple systems.

In this sense, MCP is adjacent to agent gateways and tool routers (such as OpenClaw) that provide a control plane for tool invocation and automation.

## References
1. Anthropic, “Introducing the Model Context Protocol” (news post). https://www.anthropic.com/news/model-context-protocol
2. Model Context Protocol, “Specification” (version 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25

## External links
- MCP home: https://modelcontextprotocol.io/
- GitHub organization: https://github.com/modelcontextprotocol
