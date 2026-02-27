# OpenTelemetry GenAI Semantic Conventions

**OpenTelemetry GenAI semantic conventions** are a set of recommended attribute names, span names, events, and metrics for instrumenting *generative AI* and *agentic* systems with OpenTelemetry.

They aim to make telemetry from LLM calls, tool invocations, and multi-step agent workflows more consistent across libraries and vendors, so that traces/metrics/logs can be queried and analyzed in a comparable way.

## Overview

OpenTelemetry (OTel) is a vendor-neutral observability framework. In addition to general semantic conventions (for HTTP, databases, messaging, etc.), OpenTelemetry publishes **semantic conventions for generative AI systems**. These conventions cover multiple signal types:

- **Events** for model inputs/outputs.
- **Metrics** describing GenAI operations.
- **Model spans** for model-level operations (for example, chat/completions).
- **Agent spans** for agent and framework operations (for example, creating or invoking an agent, or executing tools).

The GenAI semantic conventions are marked with **document status: Development**, indicating they are still evolving.

## What gets standardized

The conventions define:

- **Span operation names** (for example `gen_ai.operation.name`) for common GenAI actions.
- **Provider identification** (for example `gen_ai.provider.name`) to distinguish telemetry “flavors” and provider-specific attributes.
- **Model identifiers** (for example `gen_ai.request.model`) and related request/response metadata.
- **Agent-specific attributes** (for example `gen_ai.agent.name`, `gen_ai.agent.id`, `gen_ai.agent.version`) when applicable.
- Guidance on **span kind** (for example `CLIENT` for remote agent services vs `INTERNAL` for in-process agent frameworks).

## Agent spans

The agent-span specification includes patterns for operations such as:

- **Create agent**: describes agent creation (often for remote agent services).
- **Invoke agent**: describes invoking an agent to perform work.

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
- [Semantic conventions for GenAI agent and framework spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)
- [Semantic conventions for generative AI metrics](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/)

## References

1. OpenTelemetry Documentation — *Semantic conventions for generative AI systems*. https://opentelemetry.io/docs/specs/semconv/gen-ai/
2. OpenTelemetry Documentation — *Semantic Conventions for GenAI agent and framework spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
3. OpenTelemetry Documentation — *Semantic conventions for generative AI metrics*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
