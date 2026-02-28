---
title: "Agent Stack"
description: "Open, self-hostable infrastructure for deploying and sharing AI agents as services, built on A2A and integrating MCP-based integrations."
---

# Agent Stack

**Agent Stack** (formerly **BeeAI Platform**) is **open infrastructure for deploying AI agents to production**—turning agents into running services with a web UI, CLI, and runtime services—without framework or vendor lock‑in.

It is positioned as a deployment “stack” that works across agent frameworks (e.g., LangGraph, CrewAI, BeeAI Framework, or custom code), and it emphasizes interoperability via the **Agent2Agent (A2A) Protocol**.

## What it is

According to the project and announcement materials, Agent Stack provides:

- A **self-hostable server/runtime** for running agents as services
- A **web UI** for users to interact with deployed agents
- A **CLI** to deploy and manage agents
- “Batteries included” **infrastructure services** agents can request at runtime (LLM routing, embeddings/vector search, file storage, document extraction, secrets, etc.)
- **Integrations via MCP** (Model Context Protocol), including OAuth-enabled connectors

## Why it matters

Many teams can build agents, but productionizing them often requires bespoke infrastructure (auth, storage, observability, UI, deployment tooling). Agent Stack aims to standardize that layer while staying **framework-agnostic**.

In the broader agent ecosystem, Agent Stack is adjacent to:

- **A2A**: a protocol for agent-to-agent interoperability and collaboration
- **MCP**: a protocol for tool/context integration (connectors, APIs, data sources)
- **Agent frameworks**: orchestration and reasoning frameworks that can be wrapped and deployed

## Relationship to A2A and MCP

- **Built on A2A**: Agent Stack describes itself as built on the Agent2Agent protocol, exposing deployed agents over HTTP in an A2A-compatible way.
- **Uses MCP for integrations**: It also highlights MCP-based external integrations (e.g., Slack, Google Drive, APIs), including OAuth support.

## References

- BeeAI blog — *Introducing Agent Stack (formerly BeeAI Platform)*: https://beeai.dev/blog/introducing-agent-stack
- Agent Stack repository: https://github.com/i-am-bee/agentstack
- Agent Stack docs: https://agentstack.beeai.dev
