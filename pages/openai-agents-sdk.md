---
title: OpenAI Agents SDK
---

# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications, including workflows where a language model can call tools, hand off between specialized agents, stream partial results, and record execution traces. OpenAI publishes SDK implementations for Python and JavaScript/TypeScript.

## Overview

OpenAI describes the Agents SDK as a lightweight framework for building multi-agent workflows.

Across the published implementations, OpenAI highlights concepts including:

- **Agents**: model configurations that can include instructions and tool access.
- **Handoffs**: a mechanism for transferring control between specialized agents.
- **Guardrails**: configurable checks for input and output validation.
- **Tracing**: built-in recording of agent runs for debugging and optimization.

## Implementations

### Python

The Python implementation is published as the `openai-agents` package and developed in the `openai/openai-agents-python` repository.

OpenAI’s documentation for the Python SDK is published on the `openai.github.io/openai-agents-python` site.

### JavaScript/TypeScript

OpenAI publishes a JavaScript/TypeScript implementation in the `openai/openai-agents-js` repository.

OpenAI’s documentation for the JavaScript SDK is published on the `openai.github.io/openai-agents-js` site.

## Documentation

- Agents SDK guide (OpenAI API docs): https://developers.openai.com/api/docs/guides/agents-sdk/
- Agents SDK (Python) documentation site: https://openai.github.io/openai-agents-python/
- Agents SDK (JavaScript/TypeScript) documentation site: https://openai.github.io/openai-agents-js/

## See also

- Model Context Protocol (MCP)
- Agent-to-agent protocols

## References

1. OpenAI. “Agents SDK | OpenAI API”. OpenAI Developers documentation. https://developers.openai.com/api/docs/guides/agents-sdk/
2. OpenAI. *openai/openai-agents-python* (GitHub repository). https://github.com/openai/openai-agents-python
3. OpenAI. *openai/openai-agents-js* (GitHub repository). https://github.com/openai/openai-agents-js
4. OpenAI. “OpenAI Agents SDK (Python) documentation”. https://openai.github.io/openai-agents-python/
5. OpenAI. “OpenAI Agents SDK (JavaScript/TypeScript) documentation”. https://openai.github.io/openai-agents-js/
