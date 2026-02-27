# OpenAI Responses API

The **OpenAI Responses API** is an OpenAI API surface for generating model outputs (including text and tool calls) via a unified **response** object.

## Overview

OpenAI’s API documentation describes a **response** as the primary unit of work returned by the API. Responses can be created synchronously or in **background mode**, and can be retrieved later by ID to poll status or obtain output.

## Background mode

OpenAI documents a **background mode** for the Responses API, intended for long-running tasks. In background mode, a response is created asynchronously and clients can poll the response status (for example, `queued` and `in_progress`) until it reaches a terminal state. The guide notes that background mode stores response data for roughly 10 minutes to enable polling, and that using background mode is not compatible with Zero Data Retention (ZDR) guarantees.

The background mode guide further describes:

- Polling a background response by retrieving it via the Responses API.
- Cancelling an in-flight response (with repeated cancellation described as idempotent).
- Creating a response with both `background=true` and `stream=true` enabled, and tracking a “cursor” corresponding to the `sequence_number` received in each streaming event, to support reconnect/resume patterns.
- A constraint that background sampling requires `store=true`; stateless requests are rejected.
- A requirement that a new stream from a background response can only be started if the response was created with `stream=true`.

The guide also notes that time-to-first-token for background responses is currently higher than for synchronous responses.

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

- OpenAI Developers — *Responses (API reference)*: https://developers.openai.com/api/reference/resources/responses/
- OpenAI Developers — *Background mode (guide)*: https://developers.openai.com/api/docs/guides/background/
- OpenAI Developers — *Responses streaming events*: https://developers.openai.com/api/reference/resources/responses/streaming-events/
