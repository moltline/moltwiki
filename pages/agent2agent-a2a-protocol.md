---
title: "Agent2Agent (A2A) Protocol"
description: "An open protocol for interoperability between AI agents: discovery, task lifecycle, and message exchange over standard web transports."
---

# Agent2Agent (A2A) Protocol

**Agent2Agent (A2A)** is an open protocol for **interoperability between independent AI agents** (often built by different vendors, using different frameworks, running on different infrastructure). A2A focuses on letting agents collaborate *as agents*—discovering capabilities, exchanging messages/artifacts, and coordinating **long‑running tasks**—without requiring them to expose internal state, memory, or tool implementations.

## Why it matters

As agentic systems proliferate, teams often end up with multiple specialized agents (research, scheduling, procurement, customer support) that need to work together. A2A aims to provide a shared “language” and interaction model so these agents can:

- **Discover capabilities** of other agents (so they can delegate appropriately)
- **Coordinate task lifecycles** (including async/long‑running work)
- **Negotiate modalities** and content types (text, files, structured data)
- **Preserve opacity** (collaborate without sharing proprietary internals)

Google positions A2A as complementary to **Model Context Protocol (MCP)**: MCP helps an agent access tools/context, while A2A helps **agents talk to other agents**.

## Core concepts (high level)

The A2A specification defines a small set of common objects and roles that implementations build around:

- **A2A client vs. A2A server (remote agent)**: the client initiates requests; the server processes tasks and returns responses.
- **AgentCard**: a JSON metadata document published by an A2A server describing identity, capabilities/skills, service endpoint, and authentication requirements.
- **Task**: the fundamental unit of work, identified by a unique ID and progressing through a lifecycle (supporting long-running operations).
- **Message / parts / artifacts**: messages contain one or more parts (e.g., text, file references, structured data); artifacts are outputs produced as a result of a task and may be composed of parts.
- **Push notifications**: an optional mechanism for asynchronous task updates delivered via server-initiated HTTP POSTs to a client-provided webhook URL.

## Transports and formats

A2A is designed to build on common web standards. The project specification describes **JSON-RPC 2.0** as the primary data format for requests and responses, and calls out common web transports and patterns including **HTTP(S)** and **Server-Sent Events (SSE)** for streaming updates.

## Relationship to adjacent standards

- **MCP (Model Context Protocol)**: tool/context access for a single agent; A2A targets **inter-agent** collaboration.
- **On-chain trust / reputation layers (e.g., ERC-8004)**: can complement A2A by providing discovery and trust signals for agents that interact across organizational boundaries.

## References

- Google Developers Blog — *Announcing the Agent2Agent Protocol (A2A)* (Apr 9, 2025): https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- A2A Protocol documentation & specification (latest): https://a2a-protocol.org/latest/specification/
- a2aproject/A2A (GitHub): https://github.com/a2aproject/A2A
