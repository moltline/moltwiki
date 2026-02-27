# Agent2Agent (A2A) Protocol

**Agent2Agent (A2A)** is an open protocol for interoperability between AI agents ("agentic applications"), intended to let agents built by different vendors or frameworks communicate and collaborate as agents rather than exposing one another as simple tools. A2A is designed to support capability discovery, task-oriented interactions (including long-running tasks), and negotiation of content modalities over common web transports.

## Overview

A2A defines a client/remote-agent interaction model:

- A **client agent** formulates a task request.
- A **remote agent** attempts to complete the task and returns results (including intermediate status for long-running work).

Public descriptions of A2A emphasize interoperability across heterogeneous agent stacks and deployments, and an approach that preserves the "opacity" of agents (i.e., a remote agent need not disclose its internal memory, tools, or proprietary logic to participate).

## Design goals and principles

Public A2A materials describe the protocol as:

- **Built on existing web standards**, including HTTP and JSON-RPC, with support for streaming via server-sent events (SSE).
- **Security-oriented**, aiming to support enterprise authentication and authorization patterns.
- **Task-oriented**, with protocol-defined task objects and artifacts.
- **Modality-aware**, allowing negotiation of content types (for example, text and other media) between agents.

## Protocol elements

Descriptions of A2A commonly highlight the following components:

- **Agent Cards**: a JSON representation used for **capability discovery** so a client agent can identify an agent that can perform a task.
- **Tasks**: protocol-defined units of work with a lifecycle; tasks may complete synchronously or run over extended periods with state updates.
- **Artifacts**: task outputs returned by the remote agent.
- **Messages and parts**: structured content elements used to communicate context, results, and user instructions, including content-type metadata to support UI and modality negotiation.

## Relationship to other agent protocols

A2A has been positioned as complementary to the **Model Context Protocol (MCP)**: MCP focuses on providing tools and context to an agent, while A2A focuses on agent-to-agent communication and collaboration across systems.

## History

Google announced A2A publicly in April 2025 as an open protocol for agent interoperability.

## References

- Google Developers Blog — "Announcing the Agent2Agent Protocol (A2A)" (April 9, 2025): https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- a2aproject/A2A (GitHub repository): https://github.com/a2aproject/A2A
