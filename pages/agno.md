---
title: Agno
---

# Agno

**Agno** is an open-source framework and runtime for building and operating *agentic software* (LLM-based agents, multi-agent teams, and structured workflows) as production services. The project describes three main layers: a developer framework for composing agents with tools and memory, a stateless runtime intended for horizontally scalable serving, and a control-plane UI ("AgentOS") for testing and monitoring deployed agents.[^agno-readme]

## Overview

Agno positions itself as a production-oriented stack for agents:

- **Framework layer**: primitives for defining agents, teams, and workflows, including integrations (e.g., tool connectors) and features such as memory/knowledge and guardrails.[^agno-readme]
- **Runtime layer**: a server component described as a stateless, session-scoped backend (implemented with FastAPI) intended to run agent systems as APIs.[^agno-readme]
- **Control plane**: a web UI called **AgentOS** for connecting to a running runtime endpoint to test agents, view traces, and manage configurations.[^agno-readme]

The repository includes example projects and a cookbook of patterns intended to demonstrate single-agent and multi-agent systems built on the same architecture.[^agno-readme]

## Architecture (as described by the project)

Agno emphasizes operational concerns that arise when agents run as long-lived or tool-using processes (e.g., streaming responses, user/session isolation, approvals, and auditing). The project documentation and README highlight:

- **Session-scoped execution** and per-user/per-session isolation
- **Tracing and auditability** as first-class runtime features
- **Approval workflows / human-in-the-loop** controls for higher-risk actions
- **Database-backed persistence** for sessions, memory, knowledge, and traces (depending on configuration)[^agno-readme]

## Relationship to MCP

Agno includes tooling for using **Model Context Protocol (MCP)** servers as tool providers (e.g., via an MCP tools integration), and its README demonstrates connecting an agent to an MCP server URL for grounded tool access.[^agno-readme]

## History

The GitHub organization also hosts a repository named **phidata**, and community references describe a transition in branding from *Phidata* to *Agno*.[^phidata-repo]

## References

[^agno-readme]: Agno (GitHub repository), *agno-agi/agno: Build, run, manage agentic software at scale.* https://github.com/agno-agi/agno

[^phidata-repo]: Phidata (GitHub repository), *agno-agi/phidata.* https://github.com/agno-agi/phidata
