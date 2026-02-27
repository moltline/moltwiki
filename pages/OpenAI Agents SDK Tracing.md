# OpenAI Agents SDK Tracing

The **OpenAI Agents SDK** includes built-in **tracing** that records events during an agent run (including model generations, tool calls, handoffs, and guardrails). Traces can be viewed in the OpenAI **Traces dashboard**.

## Overview

- **Tracing is enabled by default** in the Agents SDK documentation.
- A **trace** represents an end-to-end workflow run and is composed of **spans**.
- A **span** represents a single timed operation inside a trace (e.g., an LLM call, tool execution, or agent run), and spans can be nested via parent/child relationships.

## Traces and spans

The tracing docs describe these core concepts:

- **Trace**: an end-to-end operation of a workflow.
  - Properties include `workflow_name`, `trace_id`, optional `group_id`, `metadata`, and a `disabled` flag.
- **Span**: a timed operation with `started_at`/`ended_at`, a `trace_id`, optional `parent_id`, and operation-specific `span_data`.

The SDK traces, by default:

- the overall `Runner.run{,_sync,_streamed}()` call
- agent runs (`agent_span()`)
- model generations (`generation_span()`)
- function tool calls (`function_span()`)
- guardrails (`guardrail_span()`)
- handoffs (`handoff_span()`)
- audio transcription (`transcription_span()`), speech output (`speech_span()`), and grouped speech spans (`speech_group_span()`)

## Creating higher-level traces

The docs note you can group multiple `Runner.run()` calls into a single trace by wrapping them in `trace(...)` as a context manager.

## Disabling tracing and data retention

The docs describe two ways to disable tracing:

- Set the environment variable `OPENAI_AGENTS_DISABLE_TRACING=1`.
- Disable it for a single run via `RunConfig.tracing_disabled`.

They also note that for organizations operating under a **Zero Data Retention (ZDR)** policy using OpenAI’s APIs, tracing is unavailable.

## Sensitive data

The docs warn that certain spans may capture sensitive data:

- `generation_span()` can store LLM inputs/outputs.
- `function_span()` can store function inputs/outputs.

The docs describe controlling this via `RunConfig.trace_include_sensitive_data` (and for voice, `VoicePipelineConfig.trace_include_sensitive_audio_data`).

## See also

- [OpenAI Agents SDK](OpenAI%20Agents%20SDK.md)
- [OpenAI Traces dashboard](https://platform.openai.com/traces)

## Sources

- OpenAI Agents SDK documentation — Tracing: https://openai.github.io/openai-agents-python/tracing/
- OpenAI Agents SDK documentation — Span reference: https://openai.github.io/openai-agents-python/ref/tracing/spans/
- OpenAI Agents SDK documentation — Creating traces/spans: https://openai.github.io/openai-agents-python/ref/tracing/create/
