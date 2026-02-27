# Model Context Protocol (MCP) Specification

The **Model Context Protocol (MCP) specification** defines the normative requirements for MCP, an open protocol for integrating large language model (LLM) applications with external data sources and tools.

MCP uses **JSON-RPC 2.0** messages over **stateful connections** and defines roles for **hosts**, **clients**, and **servers**, along with capability negotiation and a set of feature families (e.g., resources, prompts, tools). The specification also includes guidance on security and trust & safety considerations for implementers.

## Overview

The MCP specification is published on the Model Context Protocol website and is described as the **authoritative protocol requirements**, with normative language interpreted according to BCP 14 (RFC 2119 / RFC 8174).

The specification is stated to be based on a TypeScript schema (for example, `schema.ts` for a given dated version).

## Structure and concepts

The specification describes MCP as a protocol that standardizes how applications can:

- share contextual information with language models
- expose tools and capabilities to AI systems
- build composable integrations and workflows

It defines an architecture that distinguishes:

- **Hosts** (LLM applications that initiate connections)
- **Clients** (connectors within the host application)
- **Servers** (services that provide context and capabilities)

The document notes inspiration from the **Language Server Protocol (LSP)** in the sense of standardizing integrations across an ecosystem.

## Features

The specification groups capabilities into features that may be offered by servers and clients.

Servers may offer:

- **Resources** (context and data)
- **Prompts** (templated messages and workflows)
- **Tools** (functions that an AI model can execute)

Clients may offer:

- **Sampling** (server-initiated recursive LLM interactions)
- **Roots** (server-initiated inquiries into boundaries such as URIs or filesystem roots)
- **Elicitation** (server-initiated requests for additional information from users)

The specification also describes protocol utilities such as configuration, progress tracking, cancellation, error reporting, and logging.

## Security and trust considerations

The specification includes a security and trust & safety section emphasizing that MCP can enable arbitrary data access and code execution paths, and therefore implementers should address risks.

Examples of principles described include:

- **User consent and control** for data access and tool invocation
- **Data privacy** (e.g., obtaining explicit consent before exposing user data)
- **Tool safety** (treating tool descriptions and annotations as untrusted unless obtained from a trusted server)
- **LLM sampling controls** (explicit approval and user control over whether sampling occurs and what is sent)

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [Model Context Protocol (MCP) Authorization](Model%20Context%20Protocol%20(MCP)%20Authorization.md)
- [Enterprise-Grade Security for the Model Context Protocol (MCP)](Enterprise-Grade%20Security%20for%20the%20Model%20Context%20Protocol%20(MCP).md)

## References

- Model Context Protocol — Specification (dated version): https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol — BCP 14 normative language references:
  - RFC 2119: https://datatracker.ietf.org/doc/html/rfc2119
  - RFC 8174: https://datatracker.ietf.org/doc/html/rfc8174
  - BCP 14: https://datatracker.ietf.org/doc/html/bcp14
- Model Context Protocol — specification repository (schema reference): https://github.com/modelcontextprotocol/modelcontextprotocol
