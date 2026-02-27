---
title: Open Agent Specification (Agent Spec)
description: A framework-agnostic, declarative configuration language for describing agents and agentic workflows (Oracle).
---

# Open Agent Specification (Agent Spec)

**Open Agent Specification (Agent Spec)** is an open, framework-agnostic **configuration language** for describing **agents** and **agentic systems** (including structured workflows) in a portable way.

The project’s goal is to decouple *agent design* (what components exist; how they are configured; what semantics they imply) from *agent execution* (the runtime/framework actually running them), so the same agent/system description can be serialized (e.g., JSON/YAML) and executed by compatible runtimes/adapters.

## What it defines

Agent Spec models common building blocks used in agentic systems, including two primary runnable component types:

- **Agents**: conversational, tool-using LLM-based assistants (e.g., ReAct-style agents)
- **Flows**: structured, workflow-like processes made of connected nodes

## Ecosystem positioning

Agent Spec is positioned as a *design/configuration* standard that can complement other interoperability work:

- Protocols such as **MCP** (tool/resource provisioning) and **A2A** (inter-agent communication) focus on runtime connectivity.
- **Agent Spec** focuses on a standardized representation of the agent/workflow itself, intended to improve portability, consistency, and evaluation.

## Reference implementation and tooling

Oracle maintains:

- **PyAgentSpec**: a Python SDK for creating Agent Spec-compliant configurations and serializing them to JSON/YAML.
- **WayFlow**: described as a reference runtime for loading/executing Agent Spec configurations.

## Why it matters

- **Portability**: describe agents once and run them on multiple compatible runtimes/adapters.
- **Reliability and repeatability**: explicit specifications can reduce “hidden” framework defaults and make behavior more comparable.
- **Evaluation readiness**: standardized representations make it easier to test and compare implementations across frameworks.

## References

- Oracle GitHub repository: https://github.com/oracle/agent-spec
- Documentation (development): https://oracle.github.io/agent-spec/development/
