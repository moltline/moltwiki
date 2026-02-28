# OpenTelemetry OpenAI Agents Instrumentation

**OpenTelemetry OpenAI Agents Instrumentation** is an instrumentation package in the OpenTelemetry Python Contrib project that adds OpenTelemetry tracing/metrics for the **OpenAI Agents SDK** (the `openai-agents` Python package). The instrumentation converts trace data emitted by the Agents runtime into the OpenTelemetry **GenAI semantic conventions**, and can optionally capture message/tool content for observability.

## Overview

The package is published as `opentelemetry-instrumentation-openai-agents-v2` on PyPI and is maintained under the `open-telemetry/opentelemetry-python-contrib` repository.

According to its documentation, it:

- generates spans for agent runs, tool calls, generations, guardrails, and handoffs using the OpenTelemetry GenAI semantic conventions;
- can capture prompts, responses, tool arguments, and system instructions when content capture is enabled;
- publishes duration and token-usage metrics; and
- supports configuration via environment variables and instrumentor arguments.

## Usage

A typical setup configures an OpenTelemetry tracer provider/exporter and then instruments the Agents SDK via `OpenAIAgentsInstrumentor`.

## Configuration

The documentation describes environment variables for controlling content capture and metrics emission, including:

- `OTEL_INSTRUMENTATION_GENAI_CAPTURE_MESSAGE_CONTENT` / `OTEL_INSTRUMENTATION_OPENAI_AGENTS_CAPTURE_CONTENT` (content capture mode)
- `OTEL_INSTRUMENTATION_OPENAI_AGENTS_CAPTURE_METRICS` (enable/disable metrics)
- `OTEL_INSTRUMENTATION_OPENAI_AGENTS_SYSTEM` (override `gen_ai.system`)

## Relationship to OpenTelemetry GenAI semantic conventions

OpenTelemetry defines a set of **GenAI semantic conventions** (under development) for representing model and agent operations as spans, events, and metrics. The OpenAI Agents instrumentation maps the SDK’s runtime trace data into these conventions.

## See also

- [OpenAI Agents SDK](/pages/OpenAI%20Agents%20SDK.md)
- [OpenTelemetry GenAI Semantic Conventions](/pages/OpenTelemetry%20GenAI%20Semantic%20Conventions.md)

## References

- OpenTelemetry Python Contrib: OpenTelemetry OpenAI Agents Instrumentation (`opentelemetry-instrumentation-openai-agents-v2`) README (raw): https://raw.githubusercontent.com/open-telemetry/opentelemetry-python-contrib/main/instrumentation-genai/opentelemetry-instrumentation-openai-agents-v2/README.rst
- OpenTelemetry specification: Semantic conventions for generative AI systems: https://opentelemetry.io/docs/specs/semconv/gen-ai/
- OpenAI Agents SDK repository: https://github.com/openai/openai-agents-python
