# OpenInference

**OpenInference** is an open semantic-conventions specification for **AI application observability** built on top of [OpenTelemetry](https://opentelemetry.io/). It standardizes how operations such as large language model (LLM) calls, agent steps, tool invocations, and retrieval (RAG) operations are represented in distributed traces so that telemetry from different AI frameworks can be analyzed consistently.[^oi-spec]

## Overview

OpenTelemetry provides a vendor-neutral API/SDK and a wire format (OTLP) for capturing and exporting traces, metrics, and logs, but its core attribute model is intentionally generic. OpenInference defines an AI-focused attribute schema and span taxonomy intended to make traces from LLM and agentic systems easier to interpret and compare across tools and backends.[^oi-spec]

The OpenInference project also maintains instrumentation libraries and plugins that emit OpenTelemetry traces using OpenInference conventions for a range of AI SDKs and frameworks.[^oi-repo]

## Data model

### Traces and spans

In OpenTelemetry, a **trace** is a tree of **spans** linked by parent–child relationships. OpenInference uses this structure to represent an end-to-end AI request (for example, a single agent turn) and its internal operations (model calls, tool executions, retrieval queries, and post-processing steps).[^oi-spec]

### Span kinds

OpenInference defines a span classification attribute, `openinference.span.kind`, that labels what role a span plays in an AI pipeline. The specification describes span kinds including:

- **LLM** (a call to a language model API)
- **AGENT** (a reasoning step in an autonomous agent)
- **TOOL** (execution of a function or external API invoked by a model)
- **RETRIEVER** (a query to a vector store, search engine, or knowledge base)
- **EMBEDDING** (embedding generation)
- **RERANKER**, **GUARDRAIL**, **EVALUATOR**, **PROMPT**, and **CHAIN** (other common AI pipeline steps)[^oi-spec]

### Semantic conventions

OpenInference specifies attribute naming and representation conventions for AI-specific data such as model identifiers, structured inputs/outputs (e.g., message arrays), and token accounting, with the goal of making telemetry portable across OpenTelemetry-compatible backends.[^oi-spec]

## Instrumentation

The OpenInference repository includes language- and framework-specific instrumentation packages (notably for Python) intended to record traces using OpenInference conventions while remaining compatible with standard OpenTelemetry tooling.[^oi-repo]

## Related concepts

- [OpenTelemetry GenAI Semantic Conventions](OpenTelemetry%20GenAI%20Semantic%20Conventions.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

[^oi-spec]: [OpenInference Specification](https://arize-ai.github.io/openinference/spec/)
[^oi-repo]: [Arize-ai/openinference (GitHub)](https://github.com/Arize-ai/openinference)
