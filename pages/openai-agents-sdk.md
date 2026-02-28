---
title: OpenAI Agents SDK
---

# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications, including workflows where a language model can call tools, hand off between specialized agents, and record execution traces. OpenAI publishes SDK implementations for Python and JavaScript/TypeScript.

## Overview

OpenAI describes the Agents SDK as a lightweight framework for building multi-agent workflows. Core concepts described in the SDK documentation include agents (models configured with instructions and tools), handoffs (a specialized tool call for delegating control to another agent), guardrails for input validation and safety checks, sessions for managing conversation history across runs, and tracing for recording agent execution.

## Implementations

### Python

The Python implementation is published as the `openai-agents` package and developed in the `openai/openai-agents-python` repository.

### JavaScript/TypeScript

The JavaScript/TypeScript implementation is distributed as the `@openai/agents` package and documented on the OpenAI Agents SDK for TypeScript site.

## Features

### Agent loop

The TypeScript SDK includes a built-in agent loop that handles tool invocation, returns tool results to the model, and continues until a task is complete.

### Tracing

The SDK includes built-in tracing that records events during an agent run, including model generations, tool calls, handoffs, and guardrail checks. Traces can be exported and viewed in OpenAI's Traces dashboard.

## See also

- Model Context Protocol (MCP)
- Agent-to-agent protocols

## References

1. OpenAI. "Agents SDK | OpenAI API". OpenAI Developers documentation. https://developers.openai.com/api/docs/guides/agents-sdk/
2. OpenAI. "OpenAI Agents SDK TypeScript" (documentation). https://openai.github.io/openai-agents-js/
3. OpenAI. "Tracing | OpenAI Agents SDK" (documentation). https://openai.github.io/openai-agents-js/guides/tracing/
4. OpenAI. *openai/openai-agents-python* (GitHub repository). https://github.com/openai/openai-agents-python
