# Langfuse

**Langfuse** is an open-source observability platform for applications built with large language models (LLMs). It is commonly used to collect and inspect **traces** (end-to-end runs) and **spans** (individual steps) from agentic workflows, and to support evaluation workflows (e.g., offline dataset evaluation and online monitoring).

## Overview

Langfuse provides a web UI and APIs for:

- Tracing: capturing structured execution data for LLM calls and tool invocations.
- Monitoring: analyzing latency and usage-related metrics over time.
- Evaluation: organizing datasets and scoring outputs to measure quality.

## Relationship to agent runtimes and tracing standards

Many agent frameworks and SDKs emit traces in terms of traces/spans, often aligned with OpenTelemetry concepts. Langfuse can ingest trace data via OpenTelemetry pipelines and/or framework-specific integrations.

### Example: OpenAI Agents SDK instrumentation

The OpenAI Agents SDK includes built-in tracing that records events such as model generations, tool calls, guardrails, and handoffs, and exposes concepts like **traces** and **spans** for a workflow run.

Third-party OpenTelemetry instrumentation can bridge OpenAI Agents SDK traces into Langfuse. For example, Langfuse documentation describes using an OpenInference OpenAI Agents instrumentation package that exports OpenTelemetry spans to Langfuse.

## See also

- [OpenAI Agents SDK Tracing](OpenAI%20Agents%20SDK%20Tracing.md)

## References

- Langfuse guide: “Example - Tracing and Evaluation for the OpenAI-Agents SDK” (accessed 2026-03-01): https://langfuse.com/guides/cookbook/example_evaluating_openai_agents
- OpenAI Agents SDK documentation: “Tracing” (accessed 2026-03-01): https://openai.github.io/openai-agents-python/tracing/
- OpenAI Agents SDK repository (accessed 2026-03-01): https://github.com/openai/openai-agents-python
