# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit for building agentic applications and multi-agent workflows in Python. It provides primitives for defining agents with instructions and tools, coordinating handoffs between agents, adding guardrails, and recording execution traces for debugging and monitoring.

## Overview

The SDK is distributed as the `openai-agents` Python package and documented at `openai.github.io/openai-agents-python`. According to its documentation, the SDK is intended as a production-ready successor to OpenAI’s earlier experimental project **Swarm**.

## Concepts

The SDK’s documentation describes a small set of core primitives:

- **Agents**: language models configured with instructions and tools.
- **Tools**: callable functions and integrations that agents can invoke.
- **Handoffs (agents as tools)**: a mechanism for transferring control from one agent to another.
- **Guardrails**: input/output validation checks that can run alongside an agent loop.
- **Sessions**: a persistence layer for maintaining working context across runs.
- **Tracing**: built-in instrumentation that records events such as model generations, tool calls, handoffs, and guardrail checks.

## Tracing

The tracing system records an end-to-end **trace** composed of **spans** representing timed operations (for example, a model generation or tool call). The documentation states that tracing is enabled by default, can be disabled via configuration or environment variables, and includes controls for whether potentially sensitive inputs/outputs are captured.

## Interoperability

The SDK documentation describes support for integrating tool calling via the **Model Context Protocol (MCP)**, allowing agents to invoke MCP servers using the same surface as function tools.

## See also

- [[Model Context Protocol (MCP)]]
- [[Agent2Agent (A2A)]]

## References

- OpenAI Agents SDK documentation: https://openai.github.io/openai-agents-python/
- Tracing (OpenAI Agents SDK): https://openai.github.io/openai-agents-python/tracing/
- Source repository (openai/openai-agents-python): https://github.com/openai/openai-agents-python
