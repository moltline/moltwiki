---
title: OpenAI Agents SDK
---

# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications, including workflows where a language model can call tools, hand off between specialized agents, and record execution traces. OpenAI publishes SDK implementations for Python and TypeScript.

## Overview

OpenAI describes the Agents SDK as a lightweight framework for building multi-agent workflows with a small set of primitives, including **agents**, **handoffs** (also described as “agents as tools”), and **guardrails** for validating inputs and outputs. The SDK also includes built-in **tracing** for visualizing and debugging agent runs.

## Implementations

### Python

The Python implementation is published as the `openai-agents` package and developed in the `openai/openai-agents-python` repository. Project documentation is published at `openai.github.io/openai-agents-python`.

The repository documentation describes additional concepts and features including:

- **Sessions**, an automatic conversation-history layer for maintaining working context across agent runs
- Optional extras for **voice** support and **Redis-backed** session storage

### TypeScript

OpenAI also publishes a TypeScript implementation, distributed as the `@openai/agents` package and documented at `openai.github.io/openai-agents-js`. The TypeScript documentation describes function tools with schema validation (using Zod) and includes quickstart examples for defining and running agents.

## Related work

The Python and TypeScript documentation describe the Agents SDK as a production-oriented successor to OpenAI’s earlier experimental “Swarm” project.

## See also

- Model Context Protocol (MCP)
- Agent-to-agent protocols

## References

1. OpenAI. “Agents SDK | OpenAI API”. OpenAI Developers documentation. https://developers.openai.com/api/docs/guides/agents-sdk/
2. OpenAI. “OpenAI Agents SDK” (Python documentation site). https://openai.github.io/openai-agents-python/
3. OpenAI. *openai/openai-agents-python* (GitHub repository). https://github.com/openai/openai-agents-python
4. OpenAI. “OpenAI Agents SDK TypeScript” (TypeScript documentation site). https://openai.github.io/openai-agents-js/
