---
title: "MCP roots (Model Context Protocol)"
summary: "In the Model Context Protocol (MCP), roots are client-provided filesystem boundaries that define where an MCP server is allowed to operate."
read_when:
  - Understanding MCP client capabilities and filesystem access boundaries
---

# MCP roots (Model Context Protocol)

In the **Model Context Protocol (MCP)**, **roots** are filesystem locations that an MCP *client* exposes to an MCP *server* as the allowed boundary for file operations. A root is represented as a `file://` URI (with an optional human-readable name). Servers can request the list of roots, and clients may notify servers when the list changes.

## Purpose

Roots are intended to:

- Define the **scope of filesystem access** granted by a client to a server.
- Provide a standardized way for servers to discover which directories (or repositories) they can operate in.
- Support workflows where users select or manage accessible workspaces in a client UI.

## Protocol overview

### Capability declaration

Clients that support roots declare a `roots` capability during MCP initialization. The capability can indicate whether the client will emit notifications when the root list changes.

### Listing roots

Servers retrieve roots by sending a `roots/list` request. The response contains an array of root objects, each with a `uri` (a `file://` URI in the current specification) and an optional `name`.

### Root list change notifications

If supported, clients notify servers of changes via `notifications/roots/list_changed`.

## Data model

A root definition includes:

- **`uri`**: a unique identifier for the root; currently required to be a `file://` URI.
- **`name`** (optional): a display name for user-facing interfaces.

## Security considerations

The MCP roots specification emphasizes that clients should only expose roots with appropriate permissions, validate root URIs, and enforce access controls. Servers are expected to respect root boundaries and handle cases where roots become unavailable.

## References

- Model Context Protocol — *Roots* (draft specification): https://modelcontextprotocol.io/specification/draft/client/roots
- Model Context Protocol — *Specification* landing page: https://modelcontextprotocol.io/specification/
