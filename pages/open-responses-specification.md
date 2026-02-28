# Open Responses

**Open Responses** is an open-source specification and ecosystem for building multi-provider, interoperable large language model (LLM) interfaces, based on the OpenAI *Responses API* shape. It defines a shared schema for request/response objects, a streaming event model, and conventions for representing tool calls and multi-step “agentic loop” execution, with the stated goal of reducing fragmentation across provider APIs and enabling easier switching between model providers.

## Overview

Open Responses standardizes common primitives used by LLM APIs, including:

- **Items**: typed units that represent model input/output, tool invocations, and (optionally) reasoning-related states.
- **Streaming as semantic events**: server-sent events (SSE) where each event represents a meaningful state transition or delta (rather than raw JSON patches).
- **Agentic loop control flow**: a model may either yield control back to the developer for external tool execution, or run tools “internally” within provider infrastructure, depending on the deployment and tool model.

The specification uses RFC 2119 / RFC 8174 keywords (e.g., MUST/SHOULD) to define normative requirements.

## Specification concepts

### Items

In Open Responses, an **item** is an atomic unit of context that can appear as either input to a model or output from a model. Item types include (but are not limited to) message-like outputs and function/tool call representations. Items are discriminated by a `type` field.

The specification also describes item lifecycle **status** values such as `in_progress`, `incomplete`, and `completed`, and how these relate to the containing response state.

### Streaming events

For streaming responses, Open Responses specifies use of **Server-Sent Events** (`Content-Type: text/event-stream`). Streams are composed of typed events (for example, events indicating that an output item was added, text deltas, or completion). The spec describes requirements such as the terminal event being a literal `[DONE]` marker.

### Internal vs. external tools

Open Responses distinguishes between:

- **External tools**, executed by the developer’s application when the model requests a tool call.
- **Internal tools**, executed within a provider or router’s infrastructure as part of a provider-managed agentic loop.

This distinction is used to describe where orchestration logic resides and how multi-step workflows can be run either in a single provider-managed request or with developer-managed tool execution.

## Relationship to OpenAI Responses API

The Open Responses project positions itself as an ecosystem and specification “based on” the OpenAI Responses API, aiming to provide a shared schema that multiple providers and tools can implement for interoperability.

## Reception and ecosystem

Coverage of Open Responses has described it as an attempt to reduce API fragmentation in agentic workflows, and noted early ecosystem interest from model routing and local inference tooling communities.

## See also

- [OpenAI Agents SDK](openai-agents-sdk.md)
- [Model Context Protocol (MCP)](model-context-protocol-mcp.md)
- [Agent protocol](agent-protocol.md)

## References

- Open Responses — Specification: https://www.openresponses.org/specification
- InfoQ — “Open Responses Specification Enables Unified Agentic LLM Workflows” (2026-02): https://www.infoq.com/news/2026/02/openai-open-responses/
- IETF BCP 14 / RFC 2119 (Key words for use in RFCs): https://datatracker.ietf.org/doc/html/rfc2119
- IETF RFC 8174 (Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words): https://datatracker.ietf.org/doc/html/rfc8174
