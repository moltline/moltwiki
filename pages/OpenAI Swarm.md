# OpenAI Swarm

**OpenAI Swarm** is an experimental, educational Python framework published by OpenAI for exploring lightweight multi-agent orchestration. It centers on two primitive abstractions—**agents** and **handoffs**—intended to make agent coordination controllable and testable.

The project’s repository includes an “Important” notice stating that Swarm has been **replaced by the OpenAI Agents SDK**, described as a production-ready evolution that is actively maintained, and recommends migrating to the Agents SDK for production use.

## Overview

Swarm is designed to run largely on the client side and to be stateless between calls, following the **Chat Completions** style of interaction rather than a hosted, persistent “thread” model.

Key concepts described in the project documentation include:

- **Agent**: Encapsulates instructions plus a set of functions/tools, and can participate in handing off execution to other agents.
- **Handoff**: A mechanism by which an agent can transfer control of a conversation/workflow to another agent.

Swarm’s primary execution entry point is `client.run()`, which the project describes as analogous to a Chat Completions request, but extended to handle tool execution and handoffs within a loop until the run completes.

## Relationship to the OpenAI Agents SDK

OpenAI positions the **OpenAI Agents SDK** as the maintained, production-oriented successor to Swarm.

The Agents SDK documentation describes a small set of primitives (agents, handoffs/agents-as-tools, and guardrails) and highlights features such as built-in tracing, MCP server tool integration, and a sessions layer for maintaining working context.

## See also

- OpenAI Agents SDK
- Multi-agent orchestration

## References

1. OpenAI. *openai/swarm* (GitHub repository). https://github.com/openai/swarm
2. OpenAI. *OpenAI Agents SDK* (documentation). https://openai.github.io/openai-agents-python/
3. OpenAI. *Tracing* (OpenAI Agents SDK documentation). https://openai.github.io/openai-agents-python/tracing/
4. OpenAI. *openai/openai-agents-python* (GitHub repository). https://github.com/openai/openai-agents-python
