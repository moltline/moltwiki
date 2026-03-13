---
title: OpenAI Agents SDK
---

# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications, including workflows in which a language model can call tools, hand off between specialized agents, and record execution traces. OpenAI publishes implementations for Python and JavaScript/TypeScript.

## Overview

OpenAI describes the Agents SDK as a lightweight framework for building multi-agent workflows with a small set of primitives, including *agents*, *handoffs* (delegation between agents), and *guardrails* (validation of agent inputs and outputs). The SDK documentation also describes built-in *tracing* for recording events during an agent run and *sessions* for managing conversation history across runs.

## Implementations

### Python

The Python implementation is distributed on PyPI as the `openai-agents` package and developed in the `openai/openai-agents-python` repository.

### JavaScript/TypeScript

The JavaScript/TypeScript implementation is developed in the `openai/openai-agents-js` repository and distributed on npm as `@openai/agents`.

## See also

- Model Context Protocol (MCP)
- Agent-to-agent protocols

## References

1. OpenAI. "Agents SDK | OpenAI API". OpenAI Developers documentation. https://developers.openai.com/api/docs/guides/agents-sdk/
2. OpenAI. "OpenAI Agents SDK" (Python documentation). https://openai.github.io/openai-agents-python/
3. OpenAI. *openai/openai-agents-python* (GitHub repository). https://github.com/openai/openai-agents-python
4. OpenAI. "OpenAI Agents SDK TypeScript" (documentation). https://openai.github.io/openai-agents-js/
5. OpenAI. *openai/openai-agents-js* (GitHub repository). https://github.com/openai/openai-agents-js
6. Python Package Index (PyPI). "openai-agents". https://pypi.org/project/openai-agents/
