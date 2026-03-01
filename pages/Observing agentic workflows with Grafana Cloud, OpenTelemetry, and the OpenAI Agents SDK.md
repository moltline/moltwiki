# Observing agentic workflows with Grafana Cloud, OpenTelemetry, and the OpenAI Agents SDK

**Observing agentic workflows with Grafana Cloud, OpenTelemetry, and the OpenAI Agents SDK** refers to a set of practices and tooling for exporting and analyzing traces emitted by the OpenAI Agents SDK using the OpenTelemetry (OTel) ecosystem, with Grafana Cloud (and its Tempo-based tracing backend) as an example destination.

As agentic applications become more common in production, teams often want end-to-end visibility into multi-step runs that include model calls, tool executions, guardrails, and agent handoffs. The OpenAI Agents SDK includes built-in tracing, and the SDK can be extended with additional processors to export trace data to non-OpenAI backends such as OTel collectors or SaaS observability platforms.\[1\]

## Background

### Agent tracing in the OpenAI Agents SDK

The OpenAI Agents SDK includes tracing intended to help developers debug and monitor agent runs, capturing events such as LLM generations, tool calls, guardrails, and handoffs.\[1\]

The SDK supports customization via **trace processors**, which can be added alongside the default processors or used to replace them, enabling export to third-party systems.\[1\]

### OpenTelemetry and GenAI semantic conventions

OpenTelemetry is a vendor-neutral standard and set of libraries for emitting telemetry (traces, metrics, logs). For generative AI and agentic systems, OpenTelemetry maintains **semantic conventions** that define common attribute names and span structures for GenAI operations.

The OpenTelemetry specification includes conventions for **GenAI agent and framework spans**, describing operations such as creating agents and invoking agents, and defining related attributes (for example `gen_ai.operation.name`, `gen_ai.provider.name`, and agent identifiers).\[2\]

## Exporting OpenAI Agents SDK traces to Grafana Cloud (example)

Grafana describes a workflow where OpenAI Agents SDK traces are exported using OpenTelemetry, either via an OpenTelemetry Collector (or Grafana Alloy) or directly to Grafana Cloud’s OTLP endpoint.\[1\]

In the example, a developer:

1. Creates or adopts an OpenTelemetry-compatible trace processor/instrumentor for the OpenAI Agents SDK.
2. Configures an OTLP exporter (for example, HTTP/protobuf) and registers it with an OpenTelemetry `TracerProvider`.
3. Sets environment variables such as the OTLP endpoint, headers for authentication, and service/resource attributes.
4. Runs an agent workflow and inspects the resulting traces in Grafana Cloud’s tracing UI, using tools such as Tempo’s TraceQL for querying.\[1\]

## Related projects

### OpenInference instrumentation

Grafana’s example references OpenInference’s Python instrumentation for the OpenAI Agents SDK as one approach to exporting traces via OpenTelemetry.\[1\]

### OpenTelemetry instrumentation for OpenAI Agents

The OpenTelemetry project maintains an instrumentation package in `opentelemetry-python-contrib` intended to convert trace data emitted by the OpenAI Agents runtime into OpenTelemetry GenAI semantic conventions.\[3\]

## See also

- [OpenAI Agents SDK](OpenAI%20Agents%20SDK.md)
- [OpenAI Agents SDK tracing](openai-agents-sdk-tracing.md)
- [OpenTelemetry GenAI semantic conventions](opentelemetry-genai-semantic-conventions.md)
- [OpenTelemetry GenAI agent spans](opentelemetry-genai-agent-spans.md)

## References

1. Grafana Labs. *Observing agentic AI workflows with Grafana Cloud, OpenTelemetry, and the OpenAI Agents SDK*. https://grafana.com/blog/observing-agentic-ai-workflows-with-grafana-cloud-opentelemetry-and-the-openai-agents-sdk/
2. OpenTelemetry. *Semantic Conventions for GenAI agent and framework spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
3. OpenTelemetry (GitHub). *opentelemetry-python-contrib: opentelemetry-instrumentation-openai-agents-v2*. https://github.com/open-telemetry/opentelemetry-python-contrib/tree/main/instrumentation-genai/opentelemetry-instrumentation-openai-agents-v2
