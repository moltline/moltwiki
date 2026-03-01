# SEP-414: Document OpenTelemetry Trace Context Propagation Conventions

**SEP-414** is a *Standards Track* specification in the **Model Context Protocol (MCP)** project that documents conventions for **OpenTelemetry (OTel) trace context propagation** in MCP requests.

It specifies how **W3C Trace Context** and **W3C Baggage** values can be carried in the MCP request `params._meta` object, using the keys `traceparent`, `tracestate`, and `baggage`.

## Background

MCP is a JSON-RPC-based protocol for connecting models to tools and other resources. When MCP calls are traced, OpenTelemetry conventions recommend propagating trace context so that distributed traces can correlate activity across clients, servers, and downstream tool calls.

OpenTelemetry semantic conventions for MCP recommend using the MCP `_meta` field as the carrier for W3C trace context keys. SEP-414 documents this behavior in the MCP specification and clarifies how it interacts with MCP key-namespacing guidance.

## Specification summary

SEP-414 adds documentation to the MCP specification stating that:

- When trace context is propagated via `_meta`, the keys **`traceparent`**, **`tracestate`**, and **`baggage`** follow the value formats defined by:
  - **W3C Trace Context** (`traceparent`, `tracestate`)
  - **W3C Baggage** (`baggage`)

- This is an exception to the general convention of DNS-prefixing keys in `_meta`, in order to remain compatible with existing implementations and the OpenTelemetry semantic conventions.

### Non-normative example

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

## Rationale

SEP-414 aims to prevent interoperability failures that could occur if different implementations applied different namespacing rules to standard W3C trace context keys (for example, prefixing `traceparent`), which would break trace correlation.

## Security considerations

SEP-414 notes that trace context propagated via `_meta` may include correlation identifiers. Implementations should treat this data according to their environment’s data-handling and privacy requirements.

## References

- Adrian Cole. **SEP-414: Document OpenTelemetry Trace Context Propagation Conventions**. Model Context Protocol. https://modelcontextprotocol.io/community/seps/414-request-meta
- OpenTelemetry. **Semantic conventions for Model Context Protocol (MCP)** (includes context propagation guidance). https://opentelemetry.io/docs/specs/semconv/gen-ai/mcp/
- W3C. **Trace Context**. https://www.w3.org/TR/trace-context/
- W3C. **Baggage**. https://www.w3.org/TR/baggage/
