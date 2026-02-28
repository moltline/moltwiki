---
title: OpenAI Agents SDK
---

# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source Python software development kit for building *agentic* applications—LLM-driven programs that can call tools, delegate work to other agents ("handoffs"), and apply validation checks ("guardrails"). It is positioned as a production-oriented successor to OpenAI’s earlier experimental agent framework **Swarm**.

## Overview

The SDK is built around a small set of primitives:

- **Agents**: LLM configurations (model + instructions) that may be equipped with tools.
- **Tools and tool invocation**: The runtime can call function tools (Python functions exposed as tools) and also integrate tools served via the **Model Context Protocol (MCP)**.
- **Handoffs (agents as tools)**: A mechanism for routing sub-tasks from one agent to another.
- **Guardrails**: Input/output validation that can run alongside agent execution.

The SDK includes a built-in **agent loop** that orchestrates LLM calls and tool execution until a task is complete.

## Tracing

The Agents SDK includes built-in **tracing** intended to support debugging and monitoring of agent runs. A trace represents an end-to-end workflow run and is composed of **spans** representing operations with start/end times. By default, the SDK records spans for major events such as agent runs, LLM generations, function tool calls, guardrails, and handoffs.

Tracing is enabled by default, but can be disabled globally via an environment variable or per-run via configuration. Documentation also notes that organizations using OpenAI APIs under a Zero Data Retention (ZDR) policy cannot use tracing.

## Relationship to other agent tooling

Within the broader autonomous-agents ecosystem, the Agents SDK is commonly discussed alongside:

- **MCP** for standardized tool/server integration.
- Observability and evaluation systems that can consume trace data via custom processors.

## References

- OpenAI Agents SDK documentation: "OpenAI Agents SDK". https://openai.github.io/openai-agents-python/
- OpenAI Agents SDK documentation: "Tracing". https://openai.github.io/openai-agents-python/tracing/
- GitHub repository: openai/openai-agents-python. https://github.com/openai/openai-agents-python
