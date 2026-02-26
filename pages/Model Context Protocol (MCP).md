# Model Context Protocol (MCP)

The **Model Context Protocol** (MCP) is an open protocol that standardizes how large language model (LLM) applications connect to external **data sources** and **tools** through a message-based interface. MCP uses **JSON-RPC 2.0** over stateful connections, with capability negotiation between participants.

## Overview

### Motivation
LLM applications often need custom integrations for each new system (e.g., file stores, ticketing systems, databases, developer tools). MCP proposes a common protocol to reduce integration fragmentation and make tool and data access more composable across applications.[2]

### Architecture
The MCP specification describes three primary roles:[2]

- **Hosts**: LLM applications that initiate connections.
- **Clients**: connectors within the host application.
- **Servers**: services that provide context and capabilities.

MCP takes inspiration from the **Language Server Protocol** (LSP) in its goal of standardizing an ecosystem interface for adding capabilities to many host applications.[2]

### Core concepts
Servers can expose three main feature types:[2]

- **Resources**: contextual data for the user or model.
- **Prompts**: templated messages and workflows.
- **Tools**: functions the AI model can request to execute.

Clients may optionally offer features that servers can request, including:[2]

- **Sampling**: server-initiated model interactions.
- **Roots**: server-initiated inquiries into URI or filesystem boundaries.
- **Elicitation**: server-initiated requests for additional user information.

## Protocol details

### Message types
All MCP messages follow **JSON-RPC 2.0**. The base protocol defines **requests**, **responses** (success or error), and **notifications** (one-way messages without an ID).[3]

### Schema
The specification is defined authoritatively by a TypeScript schema, with an automatically generated JSON Schema also provided for tooling and validation.[3]

## Security and trust considerations
The MCP specification emphasizes that interoperability can expose powerful capabilities (including arbitrary data access and code execution paths), and highlights principles such as **user consent and control**, **data privacy**, and **tool safety**.[2] It also notes that tool descriptions (including annotations) should be treated as untrusted unless obtained from a trusted server.[2]

## Adoption and ecosystem
Anthropic announced MCP as an open-source standard for building secure, two-way connections between AI assistants and systems where data lives, and referenced support in Claude Desktop along with open repositories of MCP servers and SDKs.[1]

## References
1. Anthropic, “Introducing the Model Context Protocol”. https://www.anthropic.com/news/model-context-protocol
2. Model Context Protocol, “Specification” (version 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
3. Model Context Protocol, “Overview (Base protocol)” (version 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25/basic

## External links
- MCP home: https://modelcontextprotocol.io/
- GitHub organization: https://github.com/modelcontextprotocol
