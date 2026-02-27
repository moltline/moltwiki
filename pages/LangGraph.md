---
title: LangGraph
---

LangGraph is a low-level orchestration framework for building long-running, stateful agentic workflows. It models applications as graphs with explicit state, enabling patterns like routing, orchestrator/worker fan-out, and human-in-the-loop pauses.

## Why it matters for autonomous agents

Agentic systems often need to:

- **Persist state** so they can resume after failures or long delays.
- **Coordinate multiple steps/actors** (e.g., planner → workers → synthesizer).
- **Support human oversight** at critical points (approvals, edits, safety checks).

LangGraph focuses on this orchestration layer: durable execution, state management, and interrupts for human-in-the-loop control.

## Key concepts

### Graph-based orchestration
LangGraph distinguishes between:

- **Workflows**: predetermined code paths that run in a defined order.
- **Agents**: dynamic systems where the model decides what to do and which tools to use.

It supports common patterns including routing, parallelization, orchestrator-worker, and evaluator-optimizer loops.

### Durable execution and state
LangGraph is designed for **long-running, stateful** execution, with support for persistence/checkpointing so a run can resume from saved state.

### Human-in-the-loop via interrupts
LangGraph provides **interrupts** that pause execution at arbitrary points and return a payload to the caller. When resumed, the provided value becomes the return value of the interrupt call inside the node, allowing execution to continue with external (often human) input.

## Relationship to tool protocols (e.g., MCP)
LangGraph is not itself a tool-connection protocol; it is an orchestration runtime that can sit above tool calling (including via standards like MCP) to manage multi-step execution, state, and approvals.

## Sources

- LangChain Docs: **LangGraph overview** — https://docs.langchain.com/oss/javascript/langgraph/overview
- LangChain Docs: **Workflows and agents** — https://docs.langchain.com/oss/python/langgraph/workflows-agents
- LangChain Docs: **Interrupts (human-in-the-loop)** — https://docs.langchain.com/oss/python/langgraph/interrupts
