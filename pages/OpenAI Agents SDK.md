# OpenAI Agents SDK

The **OpenAI Agents SDK** is a software development kit for building *agentic* applications—programs that use large language models (LLMs) together with tools and orchestration logic to complete tasks. OpenAI publishes Agents SDK implementations for Python and JavaScript/TypeScript.

## Overview

OpenAI describes the Agents SDK as a lightweight, production-oriented framework with a small number of primitives for constructing multi-step and multi-agent workflows. Its documentation describes primitives such as:

- **Agents** (LLMs equipped with instructions and tools)
- **Handoffs** (using agents as tools to delegate work to other agents)
- **Guardrails** (validation of agent inputs and outputs)

The Agents SDK documentation also describes features including a built-in agent loop for tool invocation, function tools with schema generation and validation, integration with the Model Context Protocol (MCP) for calling tools exposed by MCP servers, and built-in tracing for observing agentic workflows.

## Implementations

OpenAI maintains separate repositories for:

- **Python**: `openai-agents-python`
- **JavaScript/TypeScript**: `openai-agents-js`

## Relationship to Swarm

OpenAI’s Agents SDK documentation describes it as a production-ready upgrade of OpenAI’s earlier agent experimentation project **Swarm**.

## References

1. OpenAI — *OpenAI Agents SDK documentation (Python)*. https://openai.github.io/openai-agents-python/
2. GitHub (OpenAI) — *openai/openai-agents-python*. https://github.com/openai/openai-agents-python
3. GitHub (OpenAI) — *openai/openai-agents-js*. https://github.com/openai/openai-agents-js
4. OpenAI Developers — *Agents SDK guide*. https://developers.openai.com/api/docs/guides/agents-sdk/
5. GitHub (OpenAI) — *openai/swarm* (Swarm project). https://github.com/openai/swarm
