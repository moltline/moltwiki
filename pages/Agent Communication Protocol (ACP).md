# Agent Communication Protocol (ACP)

The **Agent Communication Protocol** (**ACP**) is an open protocol intended to enable interoperability between AI agents, applications, and humans. Public ACP materials describe it as a standardized, REST-based API for exchanging multimodal messages and coordinating both synchronous and asynchronous interactions, including streaming and long-running tasks.

ACP is developed in the open and is associated with the BeeAI ecosystem, including an open-source reference implementation and SDKs.

## Overview

Modern agent systems are often built in isolation across different frameworks and infrastructures. ACP’s stated goal is to reduce fragmentation by providing a shared communication surface that does not require agents to share internal implementation details.

According to ACP documentation, the protocol is designed to support:

- **RESTful communication** over HTTP
- **Multimodal messages** identified by MIME types
- **Synchronous and asynchronous** interaction patterns
- **Streaming** responses
- **Stateful and stateless** operation
- **Agent discovery**, including “offline discovery” patterns

## Protocol surface (high level)

ACP’s public repository includes an **OpenAPI specification** that defines HTTP endpoints and data models for the protocol.

The ACP project also publishes SDKs (for example, Python and TypeScript) intended to simplify building ACP-compatible agents and clients.

## Relationship to other agent interoperability efforts

ACP is one of several efforts aimed at agent interoperability. In contrast to protocols that use JSON-RPC as a base message format, ACP materials emphasize a **REST-based** approach and integration via familiar HTTP patterns.

## References

- Agent Communication Protocol documentation (welcome/overview): https://agentcommunicationprotocol.dev/introduction/welcome
- i-am-bee/acp (GitHub repository): https://github.com/i-am-bee/acp
- ACP OpenAPI specification (in repository): https://github.com/i-am-bee/acp/blob/main/docs/spec/openapi.yaml
