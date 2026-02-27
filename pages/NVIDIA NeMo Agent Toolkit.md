---
title: NVIDIA NeMo Agent Toolkit
---

# NVIDIA NeMo Agent Toolkit

**NVIDIA NeMo Agent Toolkit** (often abbreviated **NAT**) is an open-source Python toolkit from **NVIDIA** for building, instrumenting, evaluating, and optimizing **agentic workflows**.

The project positions itself as **framework-agnostic**, aiming to add production-oriented capabilities (for example, profiling, observability, evaluation, and optimization) to agents built with a variety of agent frameworks.

## Overview

The toolkit provides a set of components for defining and running agent workflows, plus supporting systems for measuring and improving them. Its documentation emphasizes:

- **Instrumentation and insights** for understanding agent behavior at runtime.
- **Profiling and observability** to identify bottlenecks and track execution.
- **Evaluation and optimization** tools intended to improve agent quality and reliability.
- **Integrations** with multiple agent frameworks and protocols.

NVIDIA publishes the toolkit as source code on GitHub and distributes it on PyPI as the `nvidia-nat` package.

## Features

### Framework integrations

The repository describes the toolkit as usable alongside multiple agent frameworks (and custom agents) to add instrumentation and production capabilities, listing integrations with popular ecosystems such as LangChain/LangGraph, LlamaIndex, CrewAI, Semantic Kernel, and others.

### Workflow definition and execution

NAT supports defining workflows (agents, tools, models, and configuration) and running them through a CLI. The project documentation includes a minimal “hello world” example driven by a YAML workflow configuration.

### Profiling, observability, and evaluation

The toolkit includes features described as:

- **Profiling** of workflows down to token-level behavior.
- **Observability** and tracing for production monitoring.
- An **evaluation system** for offline assessment of agent workflows.

### Optimization and improvement

The repository describes capabilities for improving workflows, including a **prompt/hyperparameter optimizer** and support for **fine-tuning** approaches aimed at agentic workflows.

### Protocol support

The project documentation states support for integrating with the **Model Context Protocol (MCP)** and the **Agent-to-Agent (A2A)** protocol.

## See also

- [Model Context Protocol (MCP)](./Model%20Context%20Protocol%20(MCP).md)
- [Agent-to-Agent (A2A) Protocol](./Agent%20Protocol.md)

## References

1. NVIDIA. *NeMo Agent Toolkit* (GitHub repository). https://github.com/NVIDIA/NeMo-Agent-Toolkit (accessed 2026-02-27).
2. Python Package Index (PyPI). *nvidia-nat*. https://pypi.org/project/nvidia-nat/ (accessed 2026-02-27).
3. NVIDIA Documentation. *NeMo Agent Toolkit Documentation*. https://docs.nvidia.com/nemo/agent-toolkit/latest/ (accessed 2026-02-27).
