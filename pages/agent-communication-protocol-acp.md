---
title: "Agent Communication Protocol (ACP)"
---

# Agent Communication Protocol (ACP)

The **Agent Communication Protocol (ACP)** is an open standard intended to enable interoperability between AI agents, applications, and humans via a standardized, REST-style API. ACP has been positioned as a protocol layer for agent-to-agent communication and discovery across heterogeneous agent frameworks and deployments.

## Overview

ACP describes a set of HTTP endpoints and data models for interacting with agents, including discovering available agents and initiating agent runs. Documentation for ACP emphasizes support for synchronous and asynchronous interactions, streaming responses, and the ability to exchange multimodal content through MIME-typed message parts.

ACP has been associated with the BeeAI ecosystem as a reference implementation and surrounding tooling.

## Governance and ecosystem

ACP documentation describes the protocol as an open standard developed under the Linux Foundation AI & Data program alongside BeeAI, with an intent to provide community-driven governance.

An IBM explainer notes that ACP has been discussed in relation to other emerging interoperability protocols (such as the Model Context Protocol (MCP)), and includes a note that ACP work has merged with the A2A effort under the Linux Foundation umbrella.

## Technical characteristics

Documentation and reference materials for ACP highlight the following characteristics:

- **REST-based communication** using standard HTTP patterns
- **Message parts labeled by MIME type** to support arbitrary modalities
- **Asynchronous-first execution model** with support for long-running tasks and streaming
- **Agent discovery**, including online discovery via endpoints and documentation describing offline discovery via embedded metadata

## References

1. Agent Communication Protocol documentation, “Welcome / What is ACP?” https://agentcommunicationprotocol.dev/introduction/welcome
2. IBM, “Agent Communication Protocol (ACP)”. https://www.ibm.com/think/topics/agent-communication-protocol
3. GitHub repository: i-am-bee/acp, “Agent Communication Protocol (ACP)”. https://github.com/i-am-bee/acp
