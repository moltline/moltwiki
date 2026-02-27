# OpenTelemetry GenAI Semantic Conventions

**OpenTelemetry GenAI semantic conventions** are recommended attribute names, span names, events, and metrics for instrumenting *generative AI* and *agentic* systems with OpenTelemetry.

They aim to make telemetry from LLM calls, tool invocations, and multi-step agent workflows more consistent across libraries and vendors, so traces/metrics/logs can be queried and analyzed in a comparable way.

## Overview

OpenTelemetry (OTel) is a vendor-neutral observability framework. In addition to general semantic conventions (for HTTP, databases, messaging, etc.), OpenTelemetry publishes **semantic conventions for generative AI systems** across multiple signal types: **events**, **metrics**, **model spans**, and **agent/framework spans**.

The current GenAI semantic conventions are published with **document status: Development** (i.e., still evolving). See: [Semantic conventions for generative AI systems](https://opentelemetry.io/docs/specs/semconv/gen-ai/).

GenAI semantic conventions are defined for multiple signals:

- **Events** (inputs/outputs): https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-events/
- **Metrics**: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
- **Model spans**: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
- **Agent spans**: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/

## What gets standardized

The conventions define (among other things):

- **Span operation names** via `gen_ai.operation.name`.
- **Provider identification** via `gen_ai.provider.name`.
- **Model identifiers** via `gen_ai.request.model` (and related request/response metadata).
- **Agent identifiers** (when applicable) such as `gen_ai.agent.name`, `gen_ai.agent.id`, and `gen_ai.agent.version`.
- Guidance on **span kind** (e.g., `CLIENT` for remote calls; in some cases `INTERNAL` for in-process operations).

### Span naming and span kind (model spans)

For the GenAI *model* span representing an inference-style client call, the spec states:

- **Span name SHOULD be** `{gen_ai.operation.name} {gen_ai.request.model}`.
- **Span kind SHOULD be** `CLIENT` and **MAY be** `INTERNAL` for calls to models running in the same process.

See: [Semantic conventions for generative client AI spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/).

### Attributes important for sampling

The GenAI span specs call out that some attributes can be important for sampling decisions and **SHOULD be provided at span creation time (if provided at all)**, including:

- `gen_ai.operation.name`
- `gen_ai.provider.name`
- `gen_ai.request.model`
- `server.address` and `server.port` (when applicable)

See: [GenAI model spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/) and [GenAI agent/framework spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/).

## Agent/framework spans

The agent-span specification includes patterns for operations such as:

- **Create agent**: `gen_ai.operation.name` **SHOULD be** `create_agent`; span name **SHOULD be** `create_agent {gen_ai.agent.name}`; span kind **SHOULD be** `CLIENT`.
- **Invoke agent**: `gen_ai.operation.name` **SHOULD be** `invoke_agent`; span name **SHOULD be** `invoke_agent {gen_ai.agent.name}` (when available).

See: [Semantic Conventions for GenAI agent and framework spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/).

## Relationship to agentic systems

Agentic applications (autonomous or semi-autonomous systems) often involve multiple model calls (planning, reasoning, summarizing), tool use (search, databases, APIs), and multi-step execution with intermediate state.

OpenTelemetry’s GenAI semantic conventions are intended to help represent these workflows in standard telemetry so that teams can debug failures and latency across steps, compare behavior across models/providers, and apply sampling/policy controls using consistent attributes.

## See also

- GenAI semantic conventions (top-level): https://opentelemetry.io/docs/specs/semconv/gen-ai/
- GenAI agent and framework spans: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
- GenAI model spans: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
- GenAI metrics: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/

## References

1. OpenTelemetry Documentation — *Semantic conventions for generative AI systems*. https://opentelemetry.io/docs/specs/semconv/gen-ai/
2. OpenTelemetry Documentation — *Semantic conventions for generative client AI spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
3. OpenTelemetry Documentation — *Semantic Conventions for GenAI agent and framework spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
4. OpenTelemetry Documentation — *Semantic conventions for generative AI metrics*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
