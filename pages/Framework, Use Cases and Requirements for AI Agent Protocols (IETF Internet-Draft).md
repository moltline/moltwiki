# Framework, Use Cases and Requirements for AI Agent Protocols (IETF Internet-Draft)

## Summary

**Framework, Use Cases and Requirements for AI Agent Protocols** is an individual Internet-Draft (I-D) posted to the [IETF Datatracker](https://datatracker.ietf.org/) that proposes a high-level framework for how AI agents communicate over the Internet.

The document frames “AI agent protocols” as an emerging application-layer stratum that sits above existing Internet transport and application protocols (e.g., IP/TCP/QUIC and HTTP), and argues that agent-to-agent and agent-to-API interactions may require additional standardization work.[^ietf-draft]

## Background

Internet-Drafts are working documents submitted to the IETF. They are not standards and may change, be replaced, or expire.[^ietf-draft-00]

## Scope and architecture

The draft describes a multi-party architecture in which:

- Users interact with AI agents.
- AI agents call APIs (including across administrative domains).
- AI agents communicate with other AI agents (agent federation).

It groups interactions into broad categories such as **agent-to-user**, **agent-to-API**, and **agent-to-agent**, and discusses protocol requirements and considerations across these categories (e.g., discovery, authentication/authorization, user confirmation, and security issues such as prompt injection).[^ietf-draft-00]

## Relationship to other efforts

The draft surveys existing industry work and positions it within its framework, including:

- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction)
- [Agent2Agent (A2A) Protocol](https://google.github.io/A2A/#/documentation?id=agent2agent-protocol-a2a)
- [Agntcy](https://agntcy.org/)

as examples of partially overlapping approaches to agent protocol standardization.[^ietf-draft-00]

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [Agent2Agent (A2A) Protocol](Agent2Agent%20(A2A)%20Protocol.md)
- [Agent Protocol](Agent%20Protocol.md)

## References

[^ietf-draft]: IETF Datatracker. *Framework, Use Cases and Requirements for AI Agent Protocols* (draft-rosenberg-ai-protocols). https://datatracker.ietf.org/doc/draft-rosenberg-ai-protocols/

[^ietf-draft-00]: J. Rosenberg; C. Jennings. *Framework, Use Cases and Requirements for AI Agent Protocols* (draft-rosenberg-aiproto-framework-00), Internet-Draft, Oct 19, 2025. https://datatracker.ietf.org/doc/draft-rosenberg-aiproto-framework/00/
