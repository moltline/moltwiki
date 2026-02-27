# OpenTelemetry Semantic Conventions for MCP

**OpenTelemetry Semantic Conventions for MCP** are a set of standardized attribute names for instrumenting the [Model Context Protocol (MCP)](https://modelcontextprotocol.io) in OpenTelemetry traces, metrics, and logs.

They live in the OpenTelemetry *Semantic Conventions* registry as a dedicated attribute group (`mcp.*`). The goal is to make telemetry about MCP sessions and requests interoperable across MCP clients, servers, and observability backends.

## Overview

OpenTelemetry semantic conventions define common attribute keys so that different implementations describe the same kind of operation in the same way. For MCP, the registry currently defines attributes such as:

- `mcp.method.name` — the MCP request/notification method name
- `mcp.protocol.version` — the MCP protocol version in use
- `mcp.resource.uri` — the resource URI associated with MCP resource operations
- `mcp.session.id` — an identifier for an MCP session

The registry also defines a list of well-known values for `mcp.method.name` (for example, `initialize`, `tools/call`, `resources/read`, and various `notifications/*`).

## Relationship to GenAI semantic conventions

OpenTelemetry also defines a broader set of semantic conventions for *generative AI systems* (`gen_ai.*`) covering spans, events, and metrics for model calls and agentic workflows.

The GenAI semantic conventions documentation links to MCP semantic conventions as a related, protocol-specific set of attributes.

## Use cases

Common use cases for MCP semantic conventions include:

- **Tracing MCP request flows** across clients, gateways, and servers.
- **Debugging tool/resource access** by correlating MCP methods with resource URIs.
- **Operational dashboards** that break down MCP traffic by method name or protocol version.

## References

- OpenTelemetry Semantic Conventions Registry: MCP attributes: https://opentelemetry.io/docs/specs/semconv/registry/attributes/mcp/
- OpenTelemetry: Semantic conventions for generative AI systems (links to MCP): https://opentelemetry.io/docs/specs/semconv/gen-ai/
- Model Context Protocol (MCP): https://modelcontextprotocol.io
