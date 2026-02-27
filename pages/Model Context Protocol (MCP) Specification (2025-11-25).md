---
title: "Model Context Protocol (MCP) Specification (2025-11-25)"
---

# Model Context Protocol (MCP) Specification (2025-11-25)

The **Model Context Protocol (MCP)** is an open protocol for connecting **LLM host applications** to external **servers** that provide **tools**, **resources**, and **prompts** over a standardized interface. The MCP specification is versioned by date; the **2025-11-25** document describes the protocol’s requirements and is stated to be authoritative based on a corresponding TypeScript schema.

MCP uses **JSON-RPC 2.0** message framing and defines roles commonly described as **hosts**, **clients**, and **servers**, with capability negotiation and a set of feature families (for example, tools and resources). The specification also references IETF requirements-language conventions (BCP 14) for interpreting normative terms such as MUST and SHOULD.

## Overview

According to the 2025-11-25 specification, MCP provides a standardized way for applications to:

- share contextual information with language models
- expose tools and capabilities to AI systems
- build composable integrations and workflows

The protocol is described as using JSON-RPC 2.0 messages to establish communication between:

- **Hosts**: LLM applications that initiate connections
- **Clients**: connectors within the host application
- **Servers**: services that provide context and capabilities

The specification notes that MCP takes inspiration from the **Language Server Protocol (LSP)** model of standardizing integrations across an ecosystem of tools.

## Protocol structure

### Message framing and state

The 2025-11-25 specification describes MCP as:

- using the **JSON-RPC 2.0** message format
- operating over **stateful connections**
- supporting **capability negotiation** between client and server

### Feature families

The specification groups capabilities into feature families. It describes servers as offering any of:

- **Resources**: context and data for the user or model
- **Prompts**: templated messages and workflows
- **Tools**: functions the model can execute

It also describes clients as potentially offering features such as:

- **Sampling**: server-initiated agentic behaviors / recursive LLM interactions
- **Roots**: server-initiated inquiries into URI or filesystem boundaries

(These labels and descriptions are summarized from the specification’s overview sections.)

## Relationship to other MCP documents

The MCP ecosystem commonly includes:

- a **versioned specification** (such as 2025-11-25)
- a **schema** repository that defines the protocol types (the 2025-11-25 spec references a corresponding `schema.ts`)
- implementation guides, examples, and server catalogs maintained in related repositories

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [Model Context Protocol (MCP) Authorization](Model%20Context%20Protocol%20(MCP)%20Authorization.md)
- [Enterprise-Grade Security for the Model Context Protocol (MCP)](Enterprise-Grade%20Security%20for%20the%20Model%20Context%20Protocol%20(MCP).md)

## References

- Model Context Protocol — Specification (2025-11-25): https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol — GitHub organization: https://github.com/modelcontextprotocol
- modelcontextprotocol/modelcontextprotocol (specification and documentation repository): https://github.com/modelcontextprotocol/modelcontextprotocol
- Anthropic — “Introducing the Model Context Protocol”: https://www.anthropic.com/news/model-context-protocol
- JSON-RPC 2.0: https://www.jsonrpc.org/specification
- BCP 14 / RFC 2119: https://datatracker.ietf.org/doc/html/rfc2119
- RFC 8174: https://datatracker.ietf.org/doc/html/rfc8174
- Language Server Protocol: https://microsoft.github.io/language-server-protocol/
