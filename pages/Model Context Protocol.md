# Model Context Protocol

**Model Context Protocol (MCP)** is an open protocol for connecting large language model (LLM) applications ("hosts") to external tools and data sources via standardized interfaces. It is intended to reduce bespoke, per-integration connectors by providing a common protocol for exposing **resources**, **prompts**, and **tools** from servers to LLM applications, with capability negotiation and safety considerations.

## Overview

MCP defines a message-based protocol (using **JSON-RPC 2.0**) for communication between:

- **Hosts**: LLM applications that initiate connections.
- **Clients**: connectors inside the host that speak MCP.
- **Servers**: services that provide context and capabilities (for example, access to data or tool execution).

The MCP specification describes the protocol requirements and is published alongside reference schemas and SDKs.

## Architecture and features

### Server-provided features
MCP servers may expose:

- **Resources**: contextual data made available to the host/model.
- **Prompts**: templated messages or workflows.
- **Tools**: callable functions that the model can invoke.

### Client-provided features
MCP clients may expose features back to servers, including:

- **Sampling**: server-initiated requests for additional LLM interactions.
- **Roots**: server-initiated inquiries into filesystem/URI boundaries.
- **Elicitation**: server-initiated requests for additional information from users.

### Transport and state
The specification describes MCP as using **stateful connections** and **capability negotiation**. MCP messages use the JSON-RPC 2.0 format.

## Security and trust considerations

The MCP specification emphasizes that connecting LLM applications to arbitrary tools and data sources introduces security and safety risks (including data exfiltration and unsafe code execution paths). It highlights principles such as:

- **User consent and control** for data access and tool invocation.
- **Data privacy** protections and access controls.
- Treating **tool descriptions/annotations as untrusted** unless obtained from a trusted server.
- **Explicit approval** for LLM sampling requests and controls over what prompts are sent.

Because protocol-level enforcement is limited, implementers are expected to build consent, authorization, and auditing UI/flows into host applications.

## History

Anthropic announced MCP as an open-source standard for connecting AI assistants to external systems (for example, content repositories, business tools, and development environments), with local MCP server support in Claude Desktop and an open-source repository of MCP servers.

## References

- Model Context Protocol specification (authoritative requirements): https://modelcontextprotocol.io/specification/2025-11-25
- Anthropic announcement: "Introducing the Model Context Protocol": https://www.anthropic.com/news/model-context-protocol
- Google Cloud overview: "What is Model Context Protocol (MCP)?": https://cloud.google.com/discover/what-is-model-context-protocol
