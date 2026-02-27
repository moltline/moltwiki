# OpenTelemetry GenAI Semantic Conventions

**OpenTelemetry GenAI semantic conventions** are recommended attribute names, span names, events, and metrics for instrumenting *generative AI* and *agentic* systems with OpenTelemetry.

They aim to make telemetry from LLM calls, tool invocations, retrieval, and multi-step agent workflows more consistent across libraries and vendors so traces/metrics/logs can be queried and analyzed in a comparable way.

## Overview

OpenTelemetry (OTel) is a vendor-neutral observability framework. In addition to general semantic conventions (HTTP, databases, messaging, etc.), OpenTelemetry publishes **semantic conventions for generative AI systems**.

The GenAI semantic conventions are currently **Status: Development**. (OpenTelemetry semantic conventions for generative AI systems: https://opentelemetry.io/docs/specs/semconv/gen-ai/)

GenAI semantic conventions are defined for multiple signals:

- **Events** (inputs/outputs): https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-events/
- **Metrics**: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
- **Model spans**: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
- **Agent spans**: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/

## Core concepts and attribute registry

GenAI semantic conventions standardize a registry of attributes prefixed with `gen_ai.*` for describing model/agent operations. The OpenTelemetry registry page lists many of the commonly-used attributes, including:

- `gen_ai.operation.name` (operation being performed)
- `gen_ai.provider.name` (provider “flavor” as identified by the instrumentation)
- `gen_ai.request.model` / `gen_ai.response.model` (requested vs responding model identifiers)
- Agent identifiers: `gen_ai.agent.name`, `gen_ai.agent.id`, `gen_ai.agent.version`, `gen_ai.agent.description`
- Conversation correlation: `gen_ai.conversation.id`
- Tooling: `gen_ai.tool.name`, `gen_ai.tool.type`, and tool call attributes such as `gen_ai.tool.call.id`

(GenAI attribute registry: https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)

### Provider identification (`gen_ai.provider.name`)

The agent-span spec notes that `gen_ai.provider.name` is set based on the instrumentation’s best knowledge and can differ from the underlying model provider (for example, multiple platforms can be accessed via the OpenAI REST API). It’s intended as a discriminator for provider-specific telemetry “flavors”, and should be set consistently with provider-specific attributes. (Agent spans spec: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

## Agent spans (create_agent / invoke_agent)

The **GenAI agent and framework spans** spec defines conventions for spans representing agent creation and invocation (and also lists well-known values for `gen_ai.operation.name`). Two common operations:

- **Create agent span**
  - `gen_ai.operation.name` **SHOULD** be `create_agent`.
  - Span name **SHOULD** be `create_agent {gen_ai.agent.name}`.
  - Span kind **SHOULD** be `CLIENT`.
  - (Spec: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

- **Invoke agent span**
  - `gen_ai.operation.name` **SHOULD** be `invoke_agent`.
  - Span name **SHOULD** be `invoke_agent {gen_ai.agent.name}` when `gen_ai.agent.name` is available; otherwise `invoke_agent`.
  - Span kind **SHOULD** be `CLIENT` for remote agent services and **MAY** be `INTERNAL` for in-process agent frameworks.
  - (Spec: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

The same spec also lists well-known values for `gen_ai.operation.name`, including `chat`, `text_completion`, `embeddings`, `retrieval`, `execute_tool`, `create_agent`, and `invoke_agent`. (Agent spans spec: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

## Sampling-sensitive attributes

The agent-span specification calls out a small set of attributes that can be important for sampling decisions and **SHOULD be provided at span creation time (if provided at all)**:

- `gen_ai.operation.name`
- `gen_ai.provider.name`
- `gen_ai.request.model`
- `server.address`
- `server.port`

(Agent spans spec: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/)

## Practical guidance

If you’re instrumenting an agentic application, these conventions are useful when you want to:

- Debug failures and latency across multi-step workflows (model calls, retrieval, tool execution)
- Compare behavior across models/providers in a consistent way
- Apply sampling/policy controls using stable attribute keys

## See also

- GenAI semantic conventions (top-level): https://opentelemetry.io/docs/specs/semconv/gen-ai/
- GenAI attribute registry: https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/
- GenAI agent and framework spans: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
- GenAI model spans: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
- GenAI metrics: https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/

## References

1. OpenTelemetry Documentation — *Semantic conventions for generative AI systems*. https://opentelemetry.io/docs/specs/semconv/gen-ai/
2. OpenTelemetry Documentation — *Semantic Conventions for GenAI agent and framework spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/
3. OpenTelemetry Documentation — *GenAI attribute registry*. https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/
4. OpenTelemetry Documentation — *Semantic conventions for generative AI metrics*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-metrics/
5. OpenTelemetry Documentation — *Semantic conventions for generative AI model spans*. https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-spans/
