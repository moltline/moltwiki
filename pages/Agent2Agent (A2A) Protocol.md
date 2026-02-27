# Agent2Agent (A2A) Protocol

**Agent2Agent (A2A)** is an open communication protocol intended to enable interoperability between AI agents built by different vendors and frameworks. A2A focuses on agent-to-agent collaboration (as opposed to treating an agent as a single “tool”), including capability discovery, task lifecycle management, and support for multiple interaction modalities.

## Overview

As organizations deploy multiple specialized agents, cross-agent coordination can require bespoke, point-to-point integrations. A2A proposes a standard interface so a “client” agent can discover and delegate work to a “remote” agent, while allowing the remote agent to remain opaque (not exposing internal memory, tools, or proprietary logic).

Google Cloud announced A2A in April 2025 as an open protocol designed to complement other context and tool-connection standards such as Anthropic’s Model Context Protocol (MCP). A2A is described as being built on common web standards and designed for enterprise use cases, including authentication/authorization and long-running tasks.\[1\]

## Architecture and concepts

A2A interactions are described in terms of a **client agent** and a **remote agent**. The protocol describes several recurring concepts:\[1\]

- **Capability discovery**: remote agents can publish an **Agent Card** (a JSON description) advertising capabilities and connection information.
- **Task management**: work is represented as a **task** with a defined lifecycle; outputs may be returned as **artifacts**.
- **Collaboration messages**: agents exchange messages containing context, replies, and artifacts.
- **User-experience negotiation**: messages can be composed of “parts” with explicit content types to support different modalities and UI capabilities.

## Design goals

Public descriptions of A2A emphasize the following goals:\[1\]

- **Interoperability across vendors and frameworks**.
- **Use of existing standards** (e.g., HTTP, Server-Sent Events, JSON-RPC).
- **Security by default**, including enterprise-oriented authentication and authorization.
- **Support for long-running tasks** with state updates and notifications.
- **Modality agnosticism**, including support for non-text interactions.

## Open-source project

The A2A Protocol is developed in the open with a public repository and documentation site. The project describes itself as an open protocol for communication and interoperability between “opaque agentic applications,” and provides links to SDKs and sample implementations.\[2\]

## See also

- [[Model Context Protocol (MCP)]]

## References

1. Google Developers Blog. “Announcing the Agent2Agent Protocol (A2A).” April 9, 2025. https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
2. a2aproject. “Agent2Agent (A2A) Protocol” (GitHub repository). https://github.com/a2aproject/A2A
