---
title: "Model Context Protocol (MCP)"
description: "An open protocol for connecting LLM applications to external tools and data sources via standardized JSON-RPC interfaces."
---

# Model Context Protocol (MCP)

The **Model Context Protocol (MCP)** is an open protocol for connecting LLM applications ("hosts") to external **servers** that provide **tools**, **resources** (context/data), and **prompts**. MCP aims to replace one-off integrations with a standardized interface for exposing capabilities and context to AI systems.

## What MCP standardizes

MCP defines a common way for applications to:

- share contextual information with language models
- expose tools/capabilities to AI systems
- compose integrations and workflows across different systems

The protocol uses **JSON-RPC 2.0** messages over a **stateful connection**, and includes capability negotiation between the parties involved.

## Roles in the architecture

MCP describes three primary roles:

- **Host**: the LLM application that initiates connections
- **Client**: the connector component within the host
- **Server**: the service that provides context and capabilities to the host/client

## Core feature types

Servers can expose:

- **Resources**: data/context for the user or model to use
- **Prompts**: templated messages and workflows
- **Tools**: functions the model can invoke

Clients may expose (to servers):

- **Sampling**: server-initiated requests for LLM interactions
- **Roots**: server inquiries about filesystem/URI boundaries
- **Elicitation**: server requests for additional user information

## Security considerations (high level)

Because MCP can enable arbitrary data access and tool execution paths, the specification emphasizes user consent and control, privacy protections, and explicit approval for tool invocation and any server-initiated sampling.

## Sources

- MCP specification (2025-11-25): https://modelcontextprotocol.io/specification/2025-11-25
- Anthropic announcement: https://www.anthropic.com/news/model-context-protocol
- GitHub repository (spec + schema): https://github.com/modelcontextprotocol/modelcontextprotocol
