---
title: OpenAI Agents SDK
---

# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications, including workflows where a language model can call tools, hand off between specialized agents, and record execution traces. OpenAI publishes SDK implementations for Python and JavaScript/TypeScript.

OpenAI's documentation describes a small set of primitives—agents, handoffs, guardrails, and sessions—plus built-in tracing for debugging and monitoring agent runs.

## Overview

OpenAI describes the Agents SDK as a lightweight framework for building multi-agent workflows. In the Python implementation, core concepts include agents, handoffs (a specialized tool call for transferring control between agents), guardrails for input/output validation, sessions for managing conversation history, and tracing for recording agent runs.

## Implementations

### Python

The Python implementation is published as the `openai-agents` package and developed in the `openai/openai-agents-python` repository.

### JavaScript/TypeScript

OpenAI publishes a JavaScript/TypeScript implementation as the npm package `@openai/agents`, documented on the `openai-agents-js` site.

## See also

- Model Context Protocol (MCP)
- Agent-to-agent protocols

## References

1. OpenAI. "Agents SDK | OpenAI API". OpenAI Developers documentation. https://developers.openai.com/api/docs/guides/agents-sdk/
2. OpenAI. "OpenAI Agents SDK TypeScript" (documentation site). https://openai.github.io/openai-agents-js/
3. OpenAI. "Tracing | OpenAI Agents SDK" (TypeScript docs). https://openai.github.io/openai-agents-js/guides/tracing/
4. OpenAI. *openai/openai-agents-python* (GitHub repository). https://github.com/openai/openai-agents-python
5. PyPI. "openai-agents" (package index page). https://pypi.org/project/openai-agents/
6. npm. "@openai/agents" (package page). https://www.npmjs.com/package/@openai/agents
