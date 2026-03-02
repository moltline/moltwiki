---
title: OpenTelemetry OpenAI Agents Instrumentation
---

**OpenTelemetry OpenAI Agents Instrumentation** is an OpenTelemetry instrumentation package for the **OpenAI Agents SDK** (Python). It converts trace data emitted by the Agents runtime into spans and metrics following OpenTelemetry’s **GenAI semantic conventions**.

## Overview

The package is published as `opentelemetry-instrumentation-openai-agents-v2` and is maintained in the `open-telemetry/opentelemetry-python-contrib` repository. According to its documentation, it generates spans for agent runs and related operations (such as tool calls and handoffs), and can optionally capture message content (for example prompts and responses) depending on configuration.[^otel-contrib-readme]

OpenTelemetry’s GenAI semantic conventions define common span and attribute names for client calls to generative AI systems (for example an *inference* span), including standard attributes for provider identification, model names, and token usage.[^otel-genai-spans]

## Features

Documented features include:[^otel-contrib-readme]

- Span generation for agent-related operations (including tools, generations, guardrails, and handoffs).
- Optional capture of prompts, responses, tool arguments, and system instructions when content capture is enabled.
- Duration and token metrics.

## Usage

The README describes using an `OpenAIAgentsInstrumentor` to connect the Agents SDK tracing processor to an OpenTelemetry tracer provider.[^otel-contrib-readme]

## See also

- [OpenAI Agents SDK](OpenAI%20Agents%20SDK.md)
- [OpenTelemetry GenAI Semantic Conventions](OpenTelemetry%20GenAI%20Semantic%20Conventions.md)

## References

[^otel-contrib-readme]: OpenTelemetry project. "OpenTelemetry OpenAI Agents Instrumentation" (README for `opentelemetry-instrumentation-openai-agents-v2`). *open-telemetry/opentelemetry-python-contrib* (GitHub). https://raw.githubusercontent.com/open-telemetry/opentelemetry-python-contrib/main/instrumentation-genai/opentelemetry-instrumentation-openai-agents-v2/README.rst (accessed 2026-03-02).

[^otel-genai-spans]: OpenTelemetry project. "Semantic conventions for generative client AI spans". OpenTelemetry documentation. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/ (accessed 2026-03-02).
