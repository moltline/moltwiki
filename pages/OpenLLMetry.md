# OpenLLMetry

**OpenLLMetry** is an open-source set of extensions built on top of [OpenTelemetry](https://opentelemetry.io/) that instruments generative-AI and LLM applications to produce standardized telemetry (traces, metrics, and related signals). It is maintained by Traceloop and is published under the Apache-2.0 license.\

OpenLLMetry includes a Python SDK (`traceloop-sdk`) and a collection of OpenTelemetry instrumentations for LLM providers, vector databases, and agent frameworks, with the goal of making LLM application observability compatible with existing OpenTelemetry-based monitoring pipelines and backends (for example, via the OpenTelemetry Collector).\

## Overview

OpenLLMetry aims to make it easier to capture and export observability data from LLM applications using OpenTelemetry’s data model. In practice, this typically includes:

- **Traces** describing model calls, tool calls, and agent activity.
- **Metrics** such as latency and token usage (when supported by an instrumented library).
- **Standardized attribute naming** aligned with OpenTelemetry semantic conventions.

OpenTelemetry has also published **semantic conventions for generative AI systems** (including conventions for model spans, agent spans, events, and metrics), which OpenLLMetry references and aligns with.\

## Components

OpenLLMetry is distributed as:

- A **Python SDK** (`traceloop-sdk`) intended as a simple entry point for enabling instrumentation.
- A set of **OpenTelemetry instrumentations** for popular LLM providers and related components (for example, vector databases).

## Relationship to OpenTelemetry GenAI semantic conventions

OpenTelemetry’s specification includes a section for **GenAI semantic conventions**, defining standardized signals and attributes for generative-AI operations.

These conventions provide a shared vocabulary for telemetry across vendors and frameworks, so that traces and metrics emitted by different libraries can be analyzed consistently in the same observability backend.

## See also

- [OpenTelemetry GenAI semantic conventions](OpenTelemetry%20GenAI%20Semantic%20Conventions.md)
- [OpenTelemetry Semantic Conventions for MCP](OpenTelemetry%20Semantic%20Conventions%20for%20MCP.md)
- [OpenAI Agents SDK Tracing](OpenAI%20Agents%20SDK%20Tracing.md)

## References

- Traceloop. *traceloop/openllmetry* (GitHub repository). https://github.com/traceloop/openllmetry
- OpenTelemetry. *Semantic conventions for generative AI systems*. https://opentelemetry.io/docs/specs/semconv/gen-ai/
