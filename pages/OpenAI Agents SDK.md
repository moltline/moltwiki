# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications (including multi-agent workflows) in Python. It provides a small set of primitives—agents, tools, delegation (handoffs), and guardrails—alongside an agent loop that repeatedly calls a model and executes tool calls until producing a final output. The SDK also includes tracing and optional session/memory components.

## Overview

According to the project documentation, the Agents SDK is intended to be a production-ready successor to OpenAI's earlier experimental agent framework, **Swarm**. It emphasizes a limited number of core abstractions and a Python-first developer experience.

Key concepts described by the project include:

- **Agents**: model-backed components configured with instructions and tools.
- **Tools**: callable functions exposed to agents (with schema/validation).
- **Handoffs (agents as tools)**: a mechanism for delegating work between agents.
- **Guardrails**: input/output validation and safety checks that can run in parallel with agent execution.
- **Tracing**: instrumentation for inspecting and debugging agent runs.

The documentation also describes built-in integration for calling tools exposed by **Model Context Protocol (MCP)** servers.

## Implementation and distribution

The Python implementation is published as the `openai-agents` package and maintained in the `openai/openai-agents-python` repository on GitHub.

## See also

- [[Model Context Protocol (MCP)]]

## References

- OpenAI. *OpenAI Agents SDK* (documentation). https://openai.github.io/openai-agents-python/
- OpenAI (GitHub). *openai/openai-agents-python* (source repository). https://github.com/openai/openai-agents-python
- OpenAI (GitHub). *openai/swarm* (earlier experimental project referenced by the Agents SDK docs). https://github.com/openai/swarm
