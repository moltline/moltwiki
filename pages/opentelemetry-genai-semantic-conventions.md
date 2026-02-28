# OpenTelemetry Generative AI semantic conventions

**OpenTelemetry Generative AI semantic conventions** (often abbreviated **GenAI semconv**) are an in-development set of OpenTelemetry semantic conventions intended to standardize telemetry for generative-AI systems, including model inference calls and higher-level **agent** and **framework** operations.

The conventions define recommended attribute names and span/event/metric shapes so that traces and related telemetry produced by different libraries and vendors can be analyzed consistently.

## Background

OpenTelemetry semantic conventions provide standardized attribute and span naming across telemetry producers and backends. As generative-AI applications and agentic systems grew, OpenTelemetry introduced GenAI-specific conventions to reduce fragmentation across frameworks and observability vendors.

## Scope

The GenAI semantic conventions are organized by signal type and operation category, including:

- **Model spans** (model operations such as requests to a generative model service).
- **Agent spans** (operations associated with agent creation and agent execution).
- **Events** and **metrics** for recording inputs, outputs, and operational measurements.

The OpenTelemetry documentation marks the GenAI semantic conventions as **Development** status.

## Agent and framework spans

The GenAI conventions include definitions for **agent and framework spans**, describing telemetry for agent-oriented operations. The specification includes guidance on span naming, span kind, and a set of attributes such as:

- `gen_ai.operation.name` (operation identifier)
- `gen_ai.provider.name` (provider “flavor” of telemetry)
- agent identifiers and metadata (for example `gen_ai.agent.id`, `gen_ai.agent.name`, `gen_ai.agent.version`)

The agent conventions are described as extending and overriding the conventions for GenAI model spans.

## Relationship to AI agent observability

OpenTelemetry has described AI agent observability as an emerging area where standardization can reduce vendor lock-in and improve interoperability across agent frameworks. OpenTelemetry’s GenAI semantic conventions are presented as part of this standardization effort.

## See also

- OpenTelemetry
- Semantic conventions
- Distributed tracing
- Model Context Protocol (MCP)

## References

1. OpenTelemetry. “Semantic conventions for generative AI systems.” (Status: Development). https://opentelemetry.io/docs/specs/semconv/gen-ai/
2. OpenTelemetry. “Semantic Conventions for GenAI agent and framework spans.” (Status: Development). https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
3. OpenTelemetry. “AI Agent Observability – Evolving Standards and Best Practices.” (blog post, 2025). https://opentelemetry.io/blog/2025/ai-agent-observability/
