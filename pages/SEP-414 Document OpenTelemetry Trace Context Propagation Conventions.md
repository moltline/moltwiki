# SEP-414: Document OpenTelemetry Trace Context Propagation Conventions

**SEP-414** is a standards-track *Specification Enhancement Proposal* (SEP) in the [Model Context Protocol (MCP)](https://modelcontextprotocol.io) project that documents conventions for propagating [OpenTelemetry](https://opentelemetry.io/) trace context in MCP messages.

The proposal standardizes use of the MCP [`params._meta`](https://modelcontextprotocol.io/specification/2025-11-25/basic#_meta) property bag as the carrier for [W3C Trace Context](https://www.w3.org/TR/trace-context/) keys (notably `traceparent` and `tracestate`) and, when used, [W3C Baggage](https://www.w3.org/TR/baggage/) (`baggage`).

## Background

MCP is transport-independent and commonly runs over transports such as stdio and Streamable HTTP. While HTTP header-based trace propagation can correlate *HTTP* requests, it does not automatically cover the individual JSON-RPC messages exchanged within an MCP session.

SEP-414 documents an interoperable convention: embed trace context directly into MCP request or notification parameters using `_meta`.

## Specification

SEP-414 specifies that when OpenTelemetry trace context is propagated via `_meta`:

- `traceparent` and `tracestate` follow the [W3C Trace Context](https://www.w3.org/TR/trace-context/) value formats.
- `baggage` follows the [W3C Baggage](https://www.w3.org/TR/baggage/) value format.

The SEP also documents that these keys are an exception to MCP’s general guidance to DNS-prefix custom `_meta` keys, to preserve interoperability with existing implementations and OpenTelemetry guidance.

## Example

A non-normative example from the SEP shows `traceparent` carried in `_meta`:

```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "method": "tools/call",
  "params": {
    "name": "get_weather",
    "arguments": {
      "location": "New York"
    },
    "_meta": {
      "traceparent": "00-0af7651916cd43dd8448eb211c80319c-00f067aa0ba902b7-01"
    }
  }
}
```

## Relationship to OpenTelemetry semantic conventions

OpenTelemetry’s MCP semantic conventions recommend propagating trace context inside `params._meta` and include examples of injecting `traceparent`, `tracestate`, and optionally `baggage`.

SEP-414 complements this by documenting the convention within MCP’s own specification process.

## References

- Model Context Protocol community SEP page (SEP-414): https://modelcontextprotocol.io/community/seps/414-request-meta
- OpenTelemetry semantic conventions for MCP (context propagation section): https://opentelemetry.io/docs/specs/semconv/gen-ai/mcp/
- W3C Trace Context: https://www.w3.org/TR/trace-context/
- W3C Baggage: https://www.w3.org/TR/baggage/
