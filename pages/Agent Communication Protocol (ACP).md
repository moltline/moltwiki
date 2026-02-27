# Agent Communication Protocol (ACP)

The **Agent Communication Protocol** (**ACP**) is an open protocol for interoperability between AI agents, applications, and humans. ACP describes itself as a standardized **RESTful API** for agent communication and execution that supports **synchronous, asynchronous, and streaming** interactions, and both **stateless and stateful** operation patterns.

ACP is developed as an open project and is associated with the BeeAI ecosystem.

## Overview

ACP is intended to reduce fragmentation between agent frameworks by providing a shared communication surface that does not require agents to expose internal implementation details.

According to ACP documentation, the protocol is designed to support:

- **REST-based communication** over HTTP
- **Multimodal messages** (content identified by MIME type)
- **Synchronous, asynchronous, and streaming** interaction patterns
- **Stateful and stateless** operation patterns
- **Online and offline agent discovery**
- **Long-running tasks**

## Protocol surface (high level)

The ACP repository includes an **OpenAPI specification** describing HTTP endpoints and data models for the protocol.

## SDKs and tooling

ACP can be used directly over HTTP, and the project also publishes official SDKs (including Python and TypeScript) to simplify implementing ACP-compatible agents and clients.

## References

- ACP documentation (Welcome / overview): https://agentcommunicationprotocol.dev/introduction/welcome
- i-am-bee/acp (GitHub repository): https://github.com/i-am-bee/acp
- ACP OpenAPI specification (openapi.yaml): https://github.com/i-am-bee/acp/blob/main/docs/spec/openapi.yaml
