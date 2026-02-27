# OpenTelemetry GenAI Semantic Conventions

**OpenTelemetry GenAI semantic conventions** are a set of recommended attribute names, span names, events, and metrics for instrumenting *generative AI* and *agentic* systems with OpenTelemetry.

They aim to make telemetry from LLM calls, tool invocations, and multi-step agent workflows more consistent across libraries and vendors, so that traces/metrics/logs can be queried and analyzed in a comparable way.

## Status and scope

OpenTelemetry’s **semantic conventions for Generative AI systems** are published with document status **Development** (i.e., they are still evolving). They define conventions for multiple signal types:

- **Events** (GenAI inputs/outputs)
- **Metrics** (GenAI operation metrics)
- **Model spans** (e.g., chat/completions)
- **Agent spans** (agent/framework operations such as creating/invoking an agent or executing tools)

Source: https://opentelemetry.io/docs/specs/semconv/gen-ai/

## What gets standardized

The conventions define:

- **Span operation names** via `gen_ai.operation.name` (with a registry of well-known values).
- **Provider identification** via `gen_ai.provider.name` (acts as a discriminator for provider “telemetry flavor” and which provider-specific attributes should appear).
- **Model identifiers** via `gen_ai.request.model` / `gen_ai.response.model` and related request/response metadata.
- **Agent identifiers** via `gen_ai.agent.name`, `gen_ai.agent.id`, `gen_ai.agent.version`, etc., when applicable.
- Guidance on **span kind** (often `CLIENT` for remote services; `INTERNAL` may be used for in-process frameworks).

## Sampling-critical attributes (set at span start)

The GenAI agent span conventions explicitly call out a small set of attributes that can matter for sampling and therefore **SHOULD be provided at span creation time (if provided at all)**:

- `gen_ai.operation.name`
- `gen_ai.provider.name`
- `gen_ai.request.model`
- `server.address`
- `server.port`

Source: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/

## Agent spans (examples)

The agent-span specification includes patterns for operations such as:

- **Create agent**: `gen_ai.operation.name` SHOULD be `create_agent`; span name SHOULD be `create_agent {gen_ai.agent.name}`; span kind SHOULD be `CLIENT`.
- **Invoke agent**: `gen_ai.operation.name` SHOULD be `invoke_agent`; span name SHOULD be `invoke_agent {gen_ai.agent.name}` when available; span kind SHOULD be `CLIENT` for remote services and MAY be `INTERNAL` for in-process frameworks.

Source: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/

## Relationship to agent frameworks and autonomous systems

Agentic applications often involve multiple model calls (planning/summarizing), tool use (search, databases, APIs), and multi-step execution with intermediate state. GenAI semantic conventions help represent these workflows in standard telemetry so teams can:

- Debug failures and latency across steps
- Compare behavior across models/providers
- Apply sampling and policy controls using consistent attributes

## See also

- https://opentelemetry.io/docs/specs/semconv/gen-ai/
- https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
- https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
- https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
- https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/

## References

1. OpenTelemetry Documentation — *Semantic conventions for generative AI systems*. https://opentelemetry.io/docs/specs/semconv/gen-ai/
2. OpenTelemetry Documentation — *Semantic conventions for GenAI agent and framework spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
3. OpenTelemetry Documentation — *Semantic conventions for generative AI model spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
4. OpenTelemetry Documentation — *GenAI attribute registry*. https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/
