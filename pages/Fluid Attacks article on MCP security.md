---
title: "Fluid Attacks article on MCP security"
description: "An overview of a Fluid Attacks blog post discussing security risks and best practices for Anthropic's Model Context Protocol (MCP)."
---

# Fluid Attacks article on MCP security

**Fluid Attacks'** blog post *"The Model Context Protocol (MCP)"* describes the **Model Context Protocol (MCP)** as an open protocol for connecting AI applications to external systems, and argues that MCP’s ability to bridge AI assistants to tools and data sources introduces a distinct security risk surface.

## Summary

The article frames MCP as a standard intended to replace many bespoke integrations with a single protocol, using a client–server architecture:

- **Host**: the user-facing application that runs the model.
- **Client**: a component inside the host that manages a connection to a server.
- **Server**: an external service that exposes capabilities to the host via MCP.

It also highlights MCP’s three core primitives:

- **Tools** (executable functions)
- **Resources** (read-only contextual data)
- **Prompts** (structured templates)

## Security risks discussed

The post emphasizes that MCP can create direct pathways between models and sensitive systems, and outlines several categories of risk:

- **Supply chain and integrity risks**: malicious or typosquatted MCP servers, installer spoofing, and compromised dependencies.
- **Authorization and authentication flaws**: implementation errors around OAuth-based authorization, including discussion of **confused deputy** attacks and a **token passthrough** anti-pattern.
- **Tool and agent manipulation attacks**: prompt injection via tool descriptions or resource content, context leakage, and tool-name shadowing across servers.
- **Local execution risks**: the elevated impact of local MCP servers running with user privileges, including risks from arbitrary code execution and DNS rebinding.

## Best practices recommended

The article recommends operational and engineering controls, including:

- Maintaining a curated allowlist or registry of approved MCP servers and versions.
- Performing security review and analysis of server code and dependencies.
- Using cryptographic integrity checks and pinning versions.
- Enforcing least privilege for tokens and avoiding token passthrough.
- Adding guardrails such as schema-based input validation.

## Relationship to MCP specification

The MCP specification notes that MCP enables powerful capabilities through arbitrary data access and code execution paths and stresses user consent, data privacy, tool safety, and controls around model sampling requests.

## References

- Fluid Attacks. *The Model Context Protocol (MCP).* https://fluidattacks.com/blog/model-context-protocol-mcp-security/
- Anthropic. *Introducing the Model Context Protocol.* https://www.anthropic.com/news/model-context-protocol
- Model Context Protocol. *Specification (2025-11-25).* https://modelcontextprotocol.io/specification/2025-11-25
