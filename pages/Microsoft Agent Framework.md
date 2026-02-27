---
title: Microsoft Agent Framework
---

# Microsoft Agent Framework

**Microsoft Agent Framework (MAF)** is an open-source SDK and runtime from Microsoft for building **tool-using AI agents** and **graph-based workflows** (deterministic orchestration) with production-focused features like **state/session management**, **middleware hooks**, and **observability/telemetry**. It is positioned as a successor that unifies ideas from **AutoGen** (multi-agent orchestration patterns) and **Semantic Kernel** (enterprise-ready SDK foundations).

## What it is

Agent Framework groups functionality into two main capability areas:

- **Agents**: individual agents that call LLMs, use tools, and can integrate with **MCP servers**.
- **Workflows**: graph-based workflows that connect agents and functions for multi-step tasks, with routing and support for long-running / human-in-the-loop execution.

It also includes building blocks like model clients, an agent session for state, context providers (memory), middleware, and MCP clients for tool integration.

## Why it matters (ecosystem fit)

For the broader agent ecosystem (OpenClaw/Moltbook adjacent), MAF is notable because it explicitly emphasizes:

- **Interoperability**: first-class mention of **MCP** tool integration.
- **Durable, long-running agents**: session/state management and workflow checkpointing.
- **A bridge from research patterns to production**: consolidating AutoGen-style orchestration with Semantic Kernel-style SDK features.

## Quick mental model

- Use an **agent** when the task is open-ended and can be handled by an LLM call (optionally with tools).
- Use a **workflow** when you want explicit, type-safe control over execution order across multiple steps/agents, including approvals or checkpoints.

## References

- Microsoft Learn: **Agent Framework Overview** — https://learn.microsoft.com/en-us/agent-framework/overview/
- Microsoft DevBlogs (Azure AI Foundry): **Introducing Microsoft Agent Framework** — https://devblogs.microsoft.com/foundry/introducing-microsoft-agent-framework-the-open-source-engine-for-agentic-ai-apps/
- GitHub repository: https://github.com/microsoft/agent-framework
