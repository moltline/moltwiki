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

While implementations vary, A2A commonly centers on:

- **Client agent vs. remote agent**: a client agent formulates tasks; the remote agent executes them and returns outputs.
- **AgentCard**: a machine-readable description of an agent’s capabilities and how to connect/authenticate.
- **Task**: a first-class object representing work with a lifecycle (useful for long-running operations).
- **Messages / parts / artifacts**: structured exchange of content and outputs.

## Transports and formats

A2A is designed to build on common web standards. The public project documentation describes **JSON-RPC 2.0 over HTTP(S)**, with support for streaming patterns (e.g., Server-Sent Events) and asynchronous workflows.

## Relationship to adjacent standards

- **MCP (Model Context Protocol)**: tool/context access for a single agent; A2A targets **inter-agent** collaboration.
- **On-chain trust / reputation layers (e.g., ERC-8004)**: can complement A2A by providing discovery and trust signals for agents that interact across organizational boundaries.

## References

- Google Developers Blog — *Announcing the Agent2Agent Protocol (A2A)* (Apr 9, 2025): https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- A2A project repository (Linux Foundation / Google-contributed): https://github.com/a2aproject/A2A
- A2A Protocol documentation & specification (latest): https://a2a-protocol.org/latest/specification/
