# OpenTelemetry OpenAI Agents Instrumentation

**OpenTelemetry OpenAI Agents Instrumentation** is an official OpenTelemetry Python instrumentation package for the **OpenAI Agents SDK** (the `openai-agents` Python package). It converts trace data produced by the Agents runtime into **OpenTelemetry GenAI semantic conventions** and can export traces to OpenTelemetry backends (e.g., via OTLP exporters). It also supports optional capture of message content and publishing duration/token metrics.

## Overview

The OpenAI Agents SDK includes a built-in tracing surface (traces and spans for agent runs, tool calls, handrails/guardrails, and handoffs). The OpenTelemetry instrumentation package attaches to that tracing surface and emits OpenTelemetry spans that follow the GenAI semantic conventions.

In practice, this enables teams to observe agent workflows using existing OpenTelemetry tooling (collectors, trace backends, dashboards), and to correlate agent traces with infrastructure telemetry.

## Features

According to the package documentation, the instrumentation:

- Generates spans for agents, tools, generations, guardrails, and handoffs using OpenTelemetry GenAI semantic conventions.
- Can capture prompts, responses, tool arguments, and system instructions when content capture is enabled.
- Publishes duration and token metrics for operations.
- Provides environment-variable configuration for metadata overrides and for disabling or reducing telemetry.

## Usage

A typical setup is:

1. Configure an OpenTelemetry tracer provider and exporter (for example, OTLP).
2. Call `OpenAIAgentsInstrumentor().instrument(...)` to wire the Agents SDK tracing into OpenTelemetry.

The project documentation includes an example that configures an OTLP exporter and instruments an agent run.

## Configuration

The instrumentation exposes configuration via keyword arguments and environment variables, including:

- Content capture mode (via `OTEL_INSTRUMENTATION_GENAI_CAPTURE_MESSAGE_CONTENT` or `OTEL_INSTRUMENTATION_OPENAI_AGENTS_CAPTURE_CONTENT`).
- Metrics capture toggle (`OTEL_INSTRUMENTATION_OPENAI_AGENTS_CAPTURE_METRICS`).
- A `gen_ai.system` override (`OTEL_INSTRUMENTATION_OPENAI_AGENTS_SYSTEM`).

## Related pages

- [OpenAI Agents SDK](openai-agents-sdk.md)
- [OpenTelemetry GenAI Semantic Conventions](OpenTelemetry%20GenAI%20Semantic%20Conventions.md)

## References

- OpenTelemetry Python Contrib repository: [open-telemetry/opentelemetry-python-contrib](https://github.com/open-telemetry/opentelemetry-python-contrib)
- Instrumentation README (raw): https://raw.githubusercontent.com/open-telemetry/opentelemetry-python-contrib/main/instrumentation-genai/opentelemetry-instrumentation-openai-agents-v2/README.rst
- Package on PyPI: https://pypi.org/project/opentelemetry-instrumentation-openai-agents-v2/
- OpenTelemetry GenAI semantic conventions: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
- OpenAI Agents SDK tracing docs: https://openai.github.io/openai-agents-python/tracing/
