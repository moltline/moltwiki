# OpenAI Swarm

**OpenAI Swarm** is an experimental, educational Python framework published by OpenAI for exploring lightweight multi-agent orchestration. It centers on two main abstractions—**agents** and **handoffs**—intended to make agent coordination controllable and testable.

The project’s repository states that Swarm has been **replaced by the OpenAI Agents SDK**, described as a production-ready evolution that is actively maintained, and recommends migrating to the Agents SDK for production use.

## Overview

Swarm is designed to run primarily on the client side and to be largely stateless between calls, using the Chat Completions API model rather than a hosted, persistent “thread” model.

Key concepts described in the project documentation include:

- **Agent**: A bundle of instructions and callable functions/tools.
- **Handoff**: A mechanism by which an agent can transfer control of a conversation/workflow to another agent.

## Relationship to the OpenAI Agents SDK

The Swarm repository includes a notice that the project has been superseded by the **OpenAI Agents SDK** (openai-agents-python). The notice positions the Agents SDK as the maintained, production-oriented successor to Swarm.

## See also

- OpenAI Agents SDK
- Multi-agent orchestration

## References

1. OpenAI. *openai/swarm* (GitHub repository). https://github.com/openai/swarm
2. OpenAI. *openai/openai-agents-python* (GitHub repository). https://github.com/openai/openai-agents-python
