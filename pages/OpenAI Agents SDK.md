# OpenAI Agents SDK

The **OpenAI Agents SDK** is an open-source software development kit (SDK) for building *agentic* applications (programs that can call tools, run multi-step loops, and delegate work to other agents). OpenAI positions the Agents SDK as a production-oriented evolution of its earlier experimental project **Swarm**. The SDK is available for both Python and JavaScript/TypeScript.

## Overview

OpenAI describes the Agents SDK as a lightweight framework with a small set of primitives intended to make it easier to implement multi-agent workflows.

In the Python documentation, OpenAI highlights the following core concepts:

- **Agents**: LLM-based components configured with instructions and tools.
- **Handoffs** ("agents as tools"): a mechanism for delegating control from one agent to another.
- **Guardrails**: validation and safety checks applied to inputs and outputs.
- **Sessions**: built-in conversation history management across runs.
- **Tracing**: built-in instrumentation for observing and debugging agent runs.

## Notable features

According to the official documentation and repository README, the Agents SDK includes:

- An **agent loop** that repeatedly calls the model, executes tool calls, and stops when a final output is reached.
- **Function tools** with automatic schema generation and validation.
- **MCP server tool calling** support (integration with Model Context Protocol servers for tool invocation).
- **Session memory** for maintaining context across multiple runs.
- **Tracing** support intended to help visualize and debug agent flows.

## Implementations

OpenAI maintains multiple implementations:

- **Python**: published as the `openai-agents` package.
- **JavaScript/TypeScript**: a separate SDK repository.

## Relationship to Swarm

OpenAI’s earlier repository **Swarm** is described as educational/experimental; OpenAI notes it has been replaced by the Agents SDK.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [OpenClaw](OpenClaw.md)

## References

- OpenAI. *OpenAI Agents SDK (Python) documentation*.
  https://openai.github.io/openai-agents-python/
- GitHub: openai. *openai/openai-agents-python*.
  https://github.com/openai/openai-agents-python
- GitHub: openai. *openai/openai-agents-js*.
  https://github.com/openai/openai-agents-js
- GitHub: openai. *openai/swarm*.
  https://github.com/openai/swarm
