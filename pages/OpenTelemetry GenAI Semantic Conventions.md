# OpenTelemetry GenAI Semantic Conventions

**OpenTelemetry GenAI semantic conventions** are a set of recommended attribute names, span names, events, and metrics for instrumenting *generative AI* and *agentic* systems with OpenTelemetry.

They aim to make telemetry from LLM calls, tool invocations, and multi-step agent workflows more consistent across libraries and vendors, so that traces/metrics/logs can be queried and analyzed in a comparable way.

## Overview

OpenTelemetry (OTel) is a vendor-neutral observability framework. In addition to general semantic conventions (for HTTP, databases, messaging, etc.), OpenTelemetry publishes **semantic conventions for generative AI systems**.

Per the OpenTelemetry spec, the **GenAI semantic conventions** are currently in **document status: Development** and are defined across multiple signal types:

- **Events**: inputs/outputs captured as events (opt-in). (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-events/)
- **Metrics**: instruments describing GenAI operations. (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/)
- **Model spans**: spans for model operations (e.g., chat / completion). (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/)
- **Agent spans**: spans for agent and framework operations. (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

The top-level GenAI semantic conventions page also lists **technology-specific** GenAI semantic conventions (e.g., OpenAI, AWS Bedrock, Anthropic, Azure AI Inference) and an MCP-specific section. (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/)

## What gets standardized

The conventions define:

- **Span operation names** (for example `gen_ai.operation.name`) for common GenAI actions.
- **Provider identification** (for example `gen_ai.provider.name`) to distinguish telemetry “flavors” and provider-specific attributes.
- **Model identifiers** (for example `gen_ai.request.model`) and related request/response metadata.
- **Agent-specific attributes** (for example `gen_ai.agent.name`, `gen_ai.agent.id`, `gen_ai.agent.version`) when applicable.
- Guidance on **span kind** (for example `CLIENT` for remote services vs `INTERNAL` for in-process frameworks).

The spec also calls out a small set of attributes that are important for sampling decisions and **SHOULD be provided at span creation time** (if provided at all), including `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.request.model`, and server address/port. (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

## Agent spans

The agent-span specification includes patterns for operations such as:

- **Create agent**: describes agent creation (often for remote agent services). `gen_ai.operation.name` SHOULD be `create_agent`, and span name SHOULD be `create_agent {gen_ai.agent.name}`. Span kind SHOULD be `CLIENT`. (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)
- **Invoke agent**: describes invoking an agent to perform work. `gen_ai.operation.name` SHOULD be `invoke_agent`, and span name SHOULD be `invoke_agent {gen_ai.agent.name}` when available. Span kind SHOULD be `CLIENT` for remote agent services and MAY be `INTERNAL` for in-process agent frameworks. (See: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

It also describes how GenAI agent conventions extend and override the more general GenAI span conventions.

## Relationship to agent frameworks and autonomous systems

Agentic applications (autonomous or semi-autonomous systems) often involve:

- Multiple model calls (planning, reasoning, summarizing)
- Tool use (search, databases, APIs)
- Multi-step execution with intermediate state

OpenTelemetry’s GenAI semantic conventions are intended to help represent these workflows in standard telemetry so that teams can:

- Debug failures and latency across steps
- Compare behavior across models/providers
- Apply sampling and policy controls using consistent attributes

## See also

- [OpenTelemetry semantic conventions for generative AI systems](https://opentelemetry.io/docs/specs/semconv/gen-ai/)
- [Semantic conventions for generative AI model spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/)
- [Semantic conventions for GenAI agent and framework spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)
- [Semantic conventions for generative AI metrics](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/)

## References

1. OpenTelemetry Documentation — *Semantic conventions for generative AI systems*. https://opentelemetry.io/docs/specs/semconv/gen-ai/
2. OpenTelemetry Documentation — *Semantic conventions for Generative AI events*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-events/
3. OpenTelemetry Documentation — *Semantic conventions for generative AI model spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
4. OpenTelemetry Documentation — *Semantic Conventions for GenAI agent and framework spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
5. OpenTelemetry Documentation — *Semantic conventions for generative AI metrics*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
