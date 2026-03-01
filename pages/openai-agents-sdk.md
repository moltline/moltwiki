---
title: OpenAI Agents SDK
---

# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building agentic applications, including workflows in which a language model can call tools, delegate between specialized agents ("handoffs"), and record execution traces. OpenAI publishes SDK implementations for Python and for JavaScript/TypeScript.

## Overview

OpenAI describes the Agents SDK as a lightweight framework intended to keep the number of core abstractions small. The Python documentation presents three primary primitivesagents, handoffs (agents used as tools), and guardrailsalongside built-in tracing for observing and debugging runs.[1] The Python repository README additionally documents sessions as a built-in memory layer for managing conversation history across runs.[2]

The Agents SDK is positioned as a higher-level orchestration layer that can be used with OpenAI APIs; OpenAI's "Building agents" learning track contrasts it with the lower-level Responses API, noting that the SDK handles agent loops and includes built-in support for guardrails and tracing.[3]

## Implementations

### Python

The Python implementation is published as the `openai-agents` package and developed in the `openai/openai-agents-python` repository.[2] The project documentation describes an agent loop that repeatedly calls a model, executes tool calls, and can transfer control via handoffs until a final output is produced.[2]

The repository README also documents optional extras for voice features (`openai-agents[voice]`) and Redis-backed session storage (`openai-agents[redis]`).[2]

### JavaScript/TypeScript

OpenAI also publishes a JavaScript/TypeScript implementation in the `openai/openai-agents-js` repository.[4] The repository README describes the SDK as provider-agnostic and documents support for Node.js, Deno, and Bun, with experimental support for Cloudflare Workers when Node.js compatibility is enabled.[4] Installation examples use `@openai/agents` with Zod for schema validation.[4]

## Integrations

Third parties have published integrations that build on the Agents SDK. For example, Temporal announced a public-preview integration intended to add durable execution to applications built with the Agents SDK.[5]

## See also

- Model Context Protocol (MCP)
- Agent-to-agent protocols

## References

1. OpenAI. "OpenAI Agents SDK" (Python documentation site). https://openai.github.io/openai-agents-python/
2. OpenAI. *openai/openai-agents-python* (GitHub repository README). https://github.com/openai/openai-agents-python
3. OpenAI. "Building agents" (OpenAI developer learning track). https://developers.openai.com/tracks/building-agents/
4. OpenAI. *openai/openai-agents-js* (GitHub repository README). https://github.com/openai/openai-agents-js
5. Temporal. "Production-ready agents with the OpenAI Agents SDK + Temporal". https://temporal.io/blog/announcing-openai-agents-sdk-integration
