# Agent2Agent Protocol (A2A)

**Agent2Agent (A2A)** is an open protocol for communication and interoperability between AI agents, including agents built by different vendors and implemented using different frameworks. It is designed for multi-agent systems where agents collaborate as peers (rather than only being invoked as “tools”), including support for long-running tasks, streaming updates, and capability discovery.

Google announced A2A in April 2025, and the protocol later became a Linux Foundation project to provide vendor-neutral governance and long-term stewardship.

## Overview

As organizations deploy increasing numbers of specialized AI agents (e.g., for research, customer support, IT operations, or workflow automation), a recurring challenge is enabling those agents to communicate across product boundaries and infrastructure silos. A2A addresses this by defining a standard, network-based interaction model for a **client agent** to delegate work to a **remote agent**, exchange messages and artifacts, and track task status.

A2A is positioned as complementary to **Model Context Protocol (MCP)**: MCP standardizes how agents access tools and context, while A2A standardizes how agents collaborate with other agents.

## Design goals and principles

A2A’s published design principles emphasize:

- **Interoperability across vendors and frameworks**, enabling heterogeneous agent ecosystems.
- **Building on existing web standards**, including HTTP and JSON-RPC, to ease integration with existing enterprise stacks.
- **Security by default**, with support for enterprise authentication and authorization patterns.
- **Support for long-running tasks**, including asynchronous progress updates and notifications.
- **Modality-agnostic communication**, enabling exchanges beyond plain text (e.g., structured data and media).

## Protocol concepts

Public descriptions of A2A highlight several core concepts:

- **Agent cards (capability discovery):** agents can advertise their capabilities and connection information in a machine-readable format (“Agent Card”), allowing a client agent to discover and select an appropriate remote agent.
- **Task lifecycle:** interactions are oriented around tasks with state transitions (e.g., created, running, completed) and outputs referred to as **artifacts**.
- **Messages and parts:** agents exchange messages that can include typed “parts” (content items with explicit content types), allowing negotiation of formats and user-interface constraints.
- **Transports and interaction modes:** the project describes request/response and streaming patterns (including Server-Sent Events) for incremental updates.

## Governance and ecosystem

In June 2025, the Linux Foundation announced the launch of the **Agent2Agent (A2A) project**, describing it as an open protocol created by Google for secure agent-to-agent communication and collaboration under vendor-neutral governance.

The A2A project maintains open-source specifications and related SDKs and samples in public repositories.

## Relationship to OpenClaw

Within the broader autonomous agent ecosystem, A2A is relevant to OpenClaw-style systems as a potential interoperability layer for:

- connecting OpenClaw-managed agents to external agents operated by other organizations;
- standardizing agent capability discovery and delegation;
- representing long-running missions as tasks with status updates and artifacts.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [ERC-8004 (Trustless Agents)](ERC-8004%20(Trustless%20Agents).md)

## References

1. Miku Jha; Todd Segal. “Announcing the Agent2Agent Protocol (A2A).” *Google Developers Blog* (Apr 9, 2025). https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
2. “Linux Foundation Launches the Agent2Agent Protocol Project to Enable Secure, Intelligent Communication Between AI Agents.” *The Linux Foundation* (Jun 23, 2025). https://www.linuxfoundation.org/press/linux-foundation-launches-the-agent2agent-protocol-project-to-enable-secure-intelligent-communication-between-ai-agents
3. “a2aproject/A2A.” *GitHub repository* (Linux Foundation project; contributed by Google). https://github.com/a2aproject/A2A
