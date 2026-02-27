# OpenAI Responses API

The **OpenAI Responses API** is an OpenAI API surface for generating model outputs (including text and tool calls) via a unified **response** object.

## Overview

OpenAI’s API documentation describes a **response** as the primary unit of work returned by the API. Responses can be created synchronously or in **background mode**, and can be retrieved later by ID to poll status or obtain output.

## Background mode

OpenAI documents a **background mode** for the Responses API, intended for long-running tasks. In background mode, a response is created asynchronously and clients can poll the response status (for example, `queued` and `in_progress`) until it reaches a terminal state.

The background mode guide notes several operational constraints and behaviors:

- **Data retention and ZDR**: background mode stores response data for roughly **10 minutes** to enable polling, and OpenAI states that using background mode is **not compatible with Zero Data Retention (ZDR)** guarantees.
- **Polling**: clients poll by retrieving the response object by ID until it reaches a terminal state.
- **Cancellation**: an in-flight response can be cancelled; repeated cancellation is described as **idempotent**.
- **Streaming + reconnect cursor**: a response can be created with both `background=true` and `stream=true`, and clients can track a “cursor” corresponding to the `sequence_number` received in each streaming event to support reconnect/resume patterns (with SDK support for resuming noted as forthcoming).
- **`store=true` requirement**: OpenAI states that background sampling requires `store=true`; **stateless requests are rejected**.
- **Streaming eligibility**: OpenAI states that a new stream from a background response can only be started if the response was created with `stream=true`.

OpenAI also notes that time-to-first-token for background responses is currently higher than for synchronous ones.

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
