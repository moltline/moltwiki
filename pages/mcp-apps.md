# MCP Apps

**MCP Apps** are an extension to the **Model Context Protocol (MCP)** intended to let MCP servers deliver **interactive user interfaces** (for example, charts, forms, dashboards, or other embedded views) that are rendered inline by compatible “host” applications (chat clients). The extension defines how servers declare UI resources, how hosts render them (typically in sandboxed iframes), and how hosts and embedded views communicate.

## Overview

MCP, as originally specified, focuses on connecting AI assistants to external **tools** and **resources** exposed by servers. MCP Apps add a UI layer so that a tool invocation can be paired with a UI resource that the host can fetch and display, enabling interaction beyond plain text and structured tool outputs.

The design emphasizes portability (“declare once, render in any compliant host”) and a consistent security model for embedded UI content.

## Architecture

Documentation for MCP Apps describes three primary roles:

- **Server**: an MCP server that exposes tools and declares UI resources.
- **Host**: the client application that connects to MCP servers and renders UI resources.
- **View**: the embedded UI running in an isolated context (commonly an iframe) that can receive tool inputs/results and communicate back through the host.

The host typically mediates communication between the embedded view and the MCP server, allowing a view to trigger additional tool calls via the host.

## Capability negotiation and progressive enhancement

MCP Apps are described as a form of **progressive enhancement**: hosts advertise whether they support the UI extension, and servers can register UI-enabled tools conditionally. If a host does not support MCP Apps, tools can still function by returning text or structured data without an embedded UI.

## Specification and implementations

The MCP Apps specification and reference materials are published in the public *modelcontextprotocol/ext-apps* repository, alongside SDK packages and examples.

## See also

- [Model Context Protocol (MCP)](model-context-protocol-mcp.md)

## References

1. modelcontextprotocol/ext-apps (GitHub), “MCP Apps — Official repo for spec & SDK of MCP Apps protocol.” https://github.com/modelcontextprotocol/ext-apps
2. MCP Apps documentation site, “Overview | @modelcontextprotocol/ext-apps.” https://apps.extensions.modelcontextprotocol.io/api/documents/Overview.html
3. modelcontextprotocol/ext-apps specification (GitHub), “apps.mdx (2026-01-26).” https://github.com/modelcontextprotocol/ext-apps/blob/main/specification/2026-01-26/apps.mdx
