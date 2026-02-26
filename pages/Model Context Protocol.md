# Model Context Protocol

The **Model Context Protocol (MCP)** is an open protocol for connecting AI applications (such as chat assistants and agent frameworks) to external tools and data sources through a standardized interface. MCP is intended to make tool and data integrations more portable across model providers and client applications, while supporting security boundaries between an AI client and the systems it can access.

## Overview

MCP defines a client–server architecture in which an AI application (the *client*) connects to one or more *MCP servers* that expose capabilities such as tools (actions), resources (retrievable content), and prompts (reusable instruction templates). In typical deployments, MCP servers run locally or in a controlled environment and act as adapters to third-party APIs, databases, file systems, developer tools, or internal services.

Anthropic introduced MCP as an open standard for building “secure, two-way connections” between AI tools and data sources. A dedicated specification and schema are maintained in the MCP project repositories, alongside reference implementations and a registry-style collection of example servers.

## Design goals

Commonly stated goals of MCP include:

- **Interoperability**: enabling a single integration to be reused across multiple AI clients that implement the protocol.
- **Separation of concerns**: allowing tool- and data-access logic to live in MCP servers rather than being embedded in each AI application.
- **Security and control**: supporting deployments where sensitive credentials and data remain within a controlled boundary (for example, on a user’s machine or within an organization’s network), with the AI client accessing only the exposed interface.

## Protocol model

While specific features depend on the version of the specification, MCP is generally described in terms of:

- **Clients**: AI applications that discover and call capabilities.
- **Servers**: processes that advertise available capabilities and execute requests.
- **Capabilities**:
  - **Tools** (invocable actions),
  - **Resources** (content that can be fetched or streamed), and
  - **Prompts** (templates and reusable prompt components).

MCP documentation describes a standardized method for describing available capabilities and exchanging messages between the client and server.

## Ecosystem

The MCP organization maintains:

- a repository containing the protocol specification and schemas;
- a repository of reference and community MCP servers; and
- public documentation hosted on the MCP website.

MCP has been adopted as an integration layer by various AI developer tools and agent frameworks, particularly in “local-first” assistant setups where tool access is mediated through local services.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)

## References

- Anthropic, “Introducing the Model Context Protocol”. https://www.anthropic.com/news/model-context-protocol
- Model Context Protocol specification repository. https://github.com/modelcontextprotocol/modelcontextprotocol
- Model Context Protocol documentation, “Specification”. https://modelcontextprotocol.io/specification/
- Model Context Protocol servers repository. https://github.com/modelcontextprotocol/servers
