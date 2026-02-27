---
title: OpenAI Agents SDK tracing
---

# OpenAI Agents SDK tracing

**OpenAI Agents SDK tracing** is a built-in observability feature of the OpenAI Agents SDK that records structured telemetry about an agent run, including model generations, tool calls, handoffs, and guardrail activity. Tracing data is organized into **traces** (end-to-end workflows) composed of nested **spans** (timed operations), and can be viewed in OpenAI's Traces dashboard.

## Overview

The Agents SDK enables tracing by default and captures a chronological record of events that occur during a workflow execution. A trace typically corresponds to a single run of an agent workflow, while spans represent individual operations within that run, such as a single LLM generation or a function tool invocation.

Tracing can be disabled globally via an environment variable or per-run via configuration. For organizations using OpenAI APIs under a Zero Data Retention (ZDR) policy, tracing is not available.

## Data model

### Traces

In the Agents SDK, a **trace** represents a single end-to-end workflow execution. Documented trace properties include:

- **workflow_name**: a logical name for the workflow or application.
- **trace_id**: a unique identifier for the trace.
- **group_id**: an optional identifier used to associate multiple traces (for example, across a conversation).
- **disabled**: whether the trace should be recorded.
- **metadata**: optional key–value metadata.

### Spans

A **span** represents a timed operation within a trace. Spans include start and end timestamps and can form a hierarchy using a parent span identifier. Span payloads ("span data") vary by operation type (for example, agent execution, model generation, or tool execution).

## Default instrumentation

The SDK's default tracing behavior wraps common operations in spans, including:

- Runner execution (e.g., calls to run methods)
- agent execution
- LLM generations
- function tool calls
- guardrails
- handoffs
- audio transcription and speech synthesis operations (when used)

By default, the trace is named "Agent workflow", but the name and other properties can be configured.

## Creating traces and spans

The SDK provides APIs to create higher-level traces that encompass multiple agent runs, typically by using a trace context manager. Spans are generally created automatically by the SDK, but custom spans can be created to record application-specific operations.

The current trace and current span are tracked using Python context variables (contextvars), enabling compatibility with concurrent execution patterns.

## Configuration and privacy controls

### Disabling tracing

Tracing can be disabled:

- Globally by setting the environment variable `OPENAI_AGENTS_DISABLE_TRACING=1`.
- For a single run via the run configuration option `RunConfig.tracing_disabled`.

### Sensitive data capture

Some spans may include potentially sensitive data, such as model inputs/outputs and tool call inputs/outputs. The Agents SDK documents configuration options to control whether such sensitive content is included in traces, including `RunConfig.trace_include_sensitive_data`. Audio tracing can similarly include raw audio data unless disabled via voice pipeline configuration.

## Export and processing

The Agents SDK documents a tracing architecture based on a trace provider and trace processors that batch and export spans. Developers can add additional trace processors to receive trace data, or replace the default processors to customize export destinations and behavior.

## References

- OpenAI Agents SDK documentation: Tracing. https://openai.github.io/openai-agents-python/tracing/ (accessed 2026-02-27)
- OpenAI Agents SDK documentation: Spans reference. https://openai.github.io/openai-agents-python/ref/tracing/spans/ (accessed 2026-02-27)
- OpenAI Agents SDK documentation: RunConfig reference (tracing options). https://openai.github.io/openai-agents-python/ref/run/ (accessed 2026-02-27)
