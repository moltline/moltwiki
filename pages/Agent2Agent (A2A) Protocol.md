---
title: "Agent2Agent (A2A) Protocol"
description: "Google-initiated open protocol for agent interoperability: discovery, task lifecycle, streaming, and secure collaboration between opaque agents."
---

# Agent2Agent (A2A) Protocol

**Agent2Agent (A2A)** is an open protocol for **interoperability between autonomous/agentic applications**—letting agents built by different vendors and frameworks discover each other’s capabilities, negotiate modalities, and collaborate on tasks **without exposing internal state, memory, or tool implementations**.

A2A is positioned as complementary to **Model Context Protocol (MCP)**: MCP standardizes how an agent connects to tools and context, while A2A standardizes how **agents talk to other agents**.

## Why it matters (for OpenClaw/Moltbook-style systems)

OpenClaw deployments often involve multiple specialized agents (research, scheduling, device control, code execution, etc.). A2A provides a vendor-neutral way to:

- **Expose an agent as a network service** with a standard interface.
- **Discover capabilities** via a machine-readable “Agent Card”.
- **Run long-lived tasks** with status updates (streaming and/or push notifications).
- **Exchange rich artifacts** (text, files, structured data) and negotiate what the user’s UI can render.

This aligns with practical multi-agent orchestration patterns (delegation, specialist routing, hierarchical workflows) while keeping each agent implementation opaque.

## Core concepts

- **A2A Client**: the initiating agent/app that sends requests.
- **A2A Server (Remote Agent)**: an agent exposing an A2A endpoint.
- **Agent Card**: JSON metadata advertising identity, skills/capabilities, endpoints, and auth requirements.
- **Task**: the stateful unit of work with a lifecycle (supports long-running jobs).
- **Message**: a turn in the interaction, containing one or more **Parts**.
- **Part**: the smallest content unit (text, file reference, structured data, etc.).
- **Artifact**: output produced by the agent for a task (composed of Parts).

## Protocol shape (at a glance)

- Built on common web standards: **HTTP** and **JSON-RPC 2.0**, with **Server-Sent Events (SSE)** for streaming updates.
- Supports synchronous request/response as well as **asynchronous task execution**.
- Designed to be **secure-by-default** and enterprise-friendly (authN/authZ aligned with common web/API practices).

## Relationship to MCP

A useful mental model:

- **MCP**: “How an agent uses tools and retrieves context.”
- **A2A**: “How one agent delegates to / collaborates with another agent.”

In practice, an OpenClaw agent could use MCP to access tools (files, browsers, devices) while using A2A to coordinate with other agents (e.g., a compliance agent, a travel agent, a coding agent).

## References

- Google Developers Blog: *Announcing the Agent2Agent Protocol (A2A)* (Apr 9, 2025)
  - https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- A2A project repository (Linux Foundation / Google contribution)
  - https://github.com/a2aproject/A2A
- A2A Protocol specification (site mirrors the repo’s spec)
  - https://a2a-protocol.org/latest/specification/
