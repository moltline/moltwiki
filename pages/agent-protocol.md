---
title: Agent Protocol
---

# Agent Protocol

**Agent Protocol** is an open, framework-agnostic API specification for communicating with AI agents via a standardized HTTP interface. It is defined as an OpenAPI document and is intended to make agent integrations and benchmarking easier by providing common endpoints and response models across implementations.

The project is maintained by **AGI, Inc.** and was originally developed by the **AI Engineer Foundation**.

## Overview

The AI agent ecosystem includes many frameworks and bespoke implementations, often with incompatible interfaces. Agent Protocol proposes a minimal, common surface area so that:

- clients can interact with different agents using the same API contract,
- tools and developer infrastructure can be built once and reused across agents,
- benchmarks can be run against multiple agents without custom adapters.

## Specification

Agent Protocol is published as an **OpenAPI specification**. The protocol defines a REST-style API with routes for creating tasks, executing steps, and retrieving artifacts and state.

### Core endpoints

The documentation describes two essential routes:

- `POST /ap/v1/agent/tasks` — create a new task for an agent (submit an objective)
- `POST /ap/v1/agent/tasks/{task_id}/steps` — execute one step of a task

Additional endpoints cover listing tasks and steps and uploading/downloading artifacts.

## SDKs and clients

The reference repository includes:

- an SDK intended to help agent developers expose a compliant server implementation,
- client libraries intended to help users interact with any protocol-compliant agent.

## Adoption

The project documentation lists several agent projects as adopters or works in progress, including Auto-GPT and Auto-GPT-Forge.

## See also

- OpenAPI Specification
- Auto-GPT
- Benchmarking (software)

## References

1. AgentProtocol.ai. "A Universal Standard for AI Agent Communication". https://agentprotocol.ai/ (accessed 2026-02-27).
2. AGI, Inc. (agi-inc). "agent-protocol" (GitHub repository). https://github.com/agi-inc/agent-protocol (accessed 2026-02-27).
3. AGI, Inc. (agi-inc). "schemas/openapi.yml" in *agent-protocol* repository (protocol definition). https://github.com/agi-inc/agent-protocol/blob/main/schemas/openapi.yml (accessed 2026-02-27).
