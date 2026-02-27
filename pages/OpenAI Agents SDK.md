# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications (including multi-agent workflows) in Python. It provides a small set of primitives—agents, tools, delegation (handoffs), and guardrails—alongside an agent loop that repeatedly calls a model and executes tool calls until producing a final output. The SDK also includes tracing and optional session/memory components.

## Overview

According to the project documentation, the Agents SDK is intended to be a production-ready successor to OpenAI's earlier experimental agent framework, **Swarm**. It emphasizes a limited number of core abstractions and a Python-first developer experience.

Key concepts described by the project include:

- **Agents**: model-backed components configured with instructions, tools, guardrails, and handoffs.
- **Tools**: callable functions exposed to agents (with schema/validation), including both Python function tools and tools exposed by **Model Context Protocol (MCP)** servers.
- **Handoffs (agents as tools)**: a mechanism for delegating work between agents for specialized tasks.
- **Guardrails**: configurable input/output validation and safety checks that can run in parallel with agent execution.
- **Sessions**: optional persistent memory for maintaining conversation history across agent runs.
- **Tracing**: built-in instrumentation for inspecting, debugging, and monitoring agent runs.
- **Realtime agents**: optional support for building voice agents (e.g., interruption detection and context management).

The documentation also describes built-in integration for calling tools exposed by **Model Context Protocol (MCP)** servers.

## Implementation and distribution

The Python implementation is published as the `openai-agents` package and maintained in the `openai/openai-agents-python` repository on GitHub. OpenAI also maintains a JavaScript/TypeScript Agents SDK with separate documentation.

## Release and compatibility notes

The project documents a release policy based on a 0.Y.Z versioning scheme, with minor releases (Y) used for breaking changes and patch releases (Z) for non-breaking changes.

Documented breaking-change notes include:

- **0.10.0**: Added an opt-in WebSocket transport mode for OpenAI Responses API usage, including a reusable `responses_websocket_session()` helper.
- **0.9.0**: Dropped support for Python 3.9; narrowed `Agent.as_tool()` return typing to `FunctionTool`; added configurable timeouts for function tools.
- **0.8.0**: Changed execution of synchronous function tools to run on worker threads via `asyncio.to_thread(...)`; made local MCP tool failure handling configurable.
- **0.7.0**: Made nested handoff history opt-in; changed default `reasoning.effort` for certain models.
- **0.4.0**: Dropped support for `openai` Python package v1.x; requires `openai` v2.x.

Recent releases (GitHub) include:

- **0.10.2 (2026-02-26)**: Fixes for tracing (reattaching resumed traces without duplicate trace starts; sanitizing oversized tracing span payloads), requiring approval for callable MCP policies when the agent is omitted, and exposing model request IDs on raw responses.\[1\]

## See also

- [[Model Context Protocol (MCP)]]

## References

- OpenAI. *OpenAI Agents SDK (Python)* (documentation). https://openai.github.io/openai-agents-python/
- OpenAI. *Release process/changelog* (Agents SDK docs). https://openai.github.io/openai-agents-python/release/
- OpenAI (GitHub). *openai/openai-agents-python* (source repository). https://github.com/openai/openai-agents-python
- OpenAI (GitHub). *Releases* (openai-agents-python). https://github.com/openai/openai-agents-python/releases
- OpenAI (GitHub). *Release v0.10.2* (openai-agents-python). https://github.com/openai/openai-agents-python/releases/tag/v0.10.2 \[1\]
- OpenAI. *Agents SDK | OpenAI API* (guide/entry point). https://developers.openai.com/api/docs/guides/agents-sdk/
- OpenAI (GitHub). *openai/swarm* (earlier experimental project referenced by the Agents SDK docs). https://github.com/openai/swarm
- OpenAI. *OpenAI Agents SDK (JavaScript/TypeScript)* (documentation). https://openai.github.io/openai-agents-js
