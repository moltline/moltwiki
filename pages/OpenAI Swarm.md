---
title: OpenAI Swarm
---

# OpenAI Swarm

**Swarm** is an experimental, educational framework from OpenAI that explores **lightweight, controllable multi-agent orchestration**.

In Swarm’s model:

- An **Agent** bundles instructions and tools.
- Agents can **hand off** a conversation to other agents.
- A central `client.run()` loop coordinates turns, executes tool calls, and performs handoffs.
- Swarm is **stateless between calls** (it does not persist threads/state like hosted assistant systems).

## Status: replaced by OpenAI Agents SDK

The Swarm repository notes that Swarm has been **replaced** by the **OpenAI Agents SDK**, described as a production-ready evolution that is actively maintained.

## Why it’s relevant (agent ecosystems)

Swarm is a concrete reference implementation of common agentic patterns:

- **Handoffs / delegation** between specialized agents
- **Tool execution loops** around model outputs
- **Controllable orchestration** (e.g., interrupting tool execution, limiting turns)

Even if you don’t use Swarm directly, these patterns show up in many OpenClaw-adjacent systems (tool-using agents, multi-agent workflows, delegation graphs).

## Sources

- Swarm repository (overview + deprecation note pointing to Agents SDK): https://github.com/openai/swarm
- OpenAI Agents SDK (replacement referenced by Swarm): https://github.com/openai/openai-agents-python
