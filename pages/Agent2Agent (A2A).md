# Agent2Agent (A2A)

**Agent2Agent (A2A)** is an open protocol for communication and interoperability between autonomous AI agents. It is designed to let agents built by different vendors and frameworks collaborate on tasks while keeping each agent’s internal tools, memory, and proprietary logic opaque.

The protocol was introduced by Google in 2025 and later placed under the governance of the Linux Foundation as an open source project.

## Overview

A2A standardizes how a **client agent** delegates work to a **remote agent** and receives results. The protocol focuses on agent-to-agent collaboration (as opposed to treating an agent as a simple tool call) and aims to support multi-agent workflows in enterprise settings.

A2A is described as complementary to Anthropic’s **Model Context Protocol (MCP)**, which standardizes how agents connect to external tools and context; A2A instead standardizes how agents communicate with each other.

## Design goals and principles

Google’s announcement described several design principles for A2A, including:

- **Building on existing standards** such as HTTP, Server-Sent Events (SSE), JSON, and JSON-RPC.
- **Security by default**, with enterprise authentication and authorization considerations.
- **Support for long-running tasks**, including status updates and notifications.
- **Modality agnosticism**, intended to support non-text modalities such as audio and video streaming.

## Core concepts

Implementations and documentation commonly describe the following concepts:

- **Agent discovery / capability discovery**: agents advertise capabilities via an **Agent Card** (a machine-readable description) so other agents can select an appropriate peer.
- **Task lifecycle**: interactions are organized around a protocol-defined **task** object which may complete immediately or run asynchronously; outputs may be represented as **artifacts**.
- **Message parts and UX negotiation**: messages can be composed of typed “parts” (e.g., text, structured data, media), enabling negotiation of formats and user-interface capabilities.

## Governance and ecosystem

In 2025, the Linux Foundation announced the **Agent2Agent Protocol Project**, describing A2A as a vendor-neutral open protocol for secure agent-to-agent communication and collaboration, with the A2A codebase hosted on GitHub.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

1. Google Developers Blog. *Announcing the Agent2Agent Protocol (A2A).* April 9, 2025. https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
2. a2aproject (GitHub). *Agent2Agent (A2A) Protocol.* https://github.com/a2aproject/A2A
3. The Linux Foundation. *Linux Foundation Launches the Agent2Agent Protocol Project to Enable Secure, Intelligent Communication Between AI Agents.* June 23, 2025. https://www.linuxfoundation.org/press/linux-foundation-launches-the-agent2agent-protocol-project-to-enable-secure-intelligent-communication-between-ai-agents
