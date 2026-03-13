# OpenAI Responses API

The **OpenAI Responses API** is an OpenAI API surface for generating model outputs (including text and tool calls) via a unified **Response** object, positioned in OpenAI’s documentation as a successor-style interface to earlier chat/completions-style APIs. OpenAI’s API changelog lists the Responses API as released in **March 2025**.<ref>https://developers.openai.com/api/docs/changelog/</ref>

## Overview

OpenAI’s documentation describes a **response** as the primary unit of work returned by the API. A response can include multiple **output items** (for example, messages and tool calls), and text output may include **annotations** (such as URL citations).<ref>https://developers.openai.com/api/reference/resources/responses/</ref>

Responses can be created synchronously or in **background mode**, and can be retrieved later by ID to poll status or obtain output.<ref>https://developers.openai.com/api/docs/guides/background/</ref>

OpenAI also documents **Structured Outputs** in the Responses API, where developers can constrain model output to a supplied **JSON Schema**. The guide describes Structured Outputs as ensuring responses adhere to the schema (for example, not omitting required keys or producing invalid enum values), and shows enabling it by supplying `text: { format: { type: "json_schema", strict: true, schema: ... } }` in a Responses API request.<ref>https://developers.openai.com/api/docs/guides/structured-outputs/</ref>

## Background mode

OpenAI documents **background mode** for long-running tasks. In background mode, a response is created asynchronously and clients can poll the response status (for example, `queued` and `in_progress`) until it reaches a terminal state.<ref>https://developers.openai.com/api/docs/guides/background/</ref>

OpenAI also documents cancellation of an in-flight response; cancelling twice is described as idempotent (subsequent calls return the final Response object).<ref>https://developers.openai.com/api/docs/guides/background/</ref>

OpenAI notes that background mode has a higher time-to-first-token than synchronous responses, and that latency improvements were planned.<ref>https://developers.openai.com/api/docs/guides/background/</ref>

### Streaming and resumability

OpenAI documents creating a response with both `background=true` and `stream=true`, and tracking a cursor corresponding to the `sequence_number` included in each streaming event. The cursor can be used to resume streaming from a later point if the client reconnects (for example, by starting after a particular sequence number).<ref>https://developers.openai.com/api/docs/guides/background/</ref><ref>https://developers.openai.com/api/reference/resources/responses/methods/retrieve/</ref>

In the API reference for retrieving a response, OpenAI describes a `starting_after` query parameter as “the sequence number of the event after which to start streaming.”<ref>https://developers.openai.com/api/reference/resources/responses/methods/retrieve/</ref>

### Storage and data retention

OpenAI’s data controls documentation distinguishes between (a) **abuse monitoring logs** and (b) **application state** stored by some features. By default, abuse monitoring logs are retained for up to 30 days (unless legally required otherwise).<ref>https://developers.openai.com/api/docs/guides/your-data/</ref>

For `/v1/responses`, OpenAI states that the Responses API has a **30-day application state retention period by default**, or when the `store` parameter is set to `true` (with response data stored for at least 30 days).<ref>https://developers.openai.com/api/docs/guides/your-data/</ref>

OpenAI also states that **background mode stores response data for roughly 10 minutes to enable polling**, and therefore is **not compatible with Zero Data Retention (ZDR)**, even though requests from ZDR projects may still be accepted for legacy reasons; OpenAI notes that projects using Modified Abuse Monitoring (MAM) can rely on background mode.<ref>https://developers.openai.com/api/docs/guides/background/</ref><ref>https://developers.openai.com/api/docs/guides/your-data/</ref>

Finally, OpenAI documents that **background sampling requires `store=true`** and that stateless requests are rejected in this mode.<ref>https://developers.openai.com/api/docs/guides/background/</ref>

## Tool calling and structured outputs

OpenAI’s documentation positions the Responses API as a surface that can return tool calls as part of a response, enabling multi-step flows where an application executes tools and then sends tool outputs back to the model. OpenAI notes that when using reasoning models, any reasoning items returned alongside tool calls must also be passed back with tool call outputs in subsequent turns.<ref>https://developers.openai.com/api/docs/guides/function-calling/</ref>

## Relationship to agent frameworks

In agentic systems, a response-centric API can be used as a building block for:

- **Orchestration loops** that alternate between model output and tool execution.
- **Durable job execution** (via background mode) where work outlives a client connection.
- **Event streaming** and resumable streams for long-running agent tasks.

## See also

- [OpenAI Agents SDK](OpenAI%20Agents%20SDK.md)
- [OpenClaw Gateway](OpenClaw%20Gateway.md)
- [MCP Apps](MCP%20Apps.md)

## References

<references />
