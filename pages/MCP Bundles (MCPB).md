---
title: MCP Bundles (MCPB)
description: A packaging format for distributing local Model Context Protocol (MCP) servers as one-click installable bundles.
---

**MCP Bundles (MCPB)** are a packaging format for distributing **local** [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md) servers as a single, installable artifact (a `.mcpb` file). MCPB bundles are ZIP archives that contain the server plus a `manifest.json` describing the server and its capabilities.[^mcpb-readme]

The MCPB project is maintained in the open by the **Model Context Protocol** organization on GitHub, and includes:

- a bundle specification (the `manifest.json` schema)
- a CLI for creating bundles
- reference code used by Claude Desktop to load/verify bundles[^mcpb-readme]

## Why MCPB exists

MCP servers can be run locally via stdio transports, but installing them traditionally involves manual dependency management and host-specific configuration. MCPB aims to make local MCP servers easier to distribute and install—“spiritually similar” to browser or editor extension bundles—so end users can install a local MCP server with a single click in supporting desktop apps.[^mcpb-readme]

## What’s inside a `.mcpb`

At a minimum, an MCPB bundle contains a `manifest.json` and any files needed to run the MCP server (code, dependencies, assets). The repository describes typical layouts for Node.js, Python, and binary servers.[^mcpb-readme]

## Tooling (CLI)

The MCPB repository includes a CLI to help create bundles, including initializing a `manifest.json` and packing a directory into a `.mcpb` artifact.[^mcpb-readme]

## Relationship to “DXT” (Desktop Extensions)

The MCPB repository notes that the project was renamed from **DXT (Desktop Extensions)** to **MCPB (MCP Bundles)**, including a rename of the CLI and file extension (for example, `.dxt` → `.mcpb`).[^mcpb-readme]

## Claude Desktop and local MCP servers

Anthropic’s Claude Desktop documentation describes “desktop extensions” as a streamlined way to install and manage local MCP servers, including support for installing custom extensions by selecting a `.mcpb` file in the app’s Extensions settings.[^claude-help-mcpb]

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [mcp-publisher](mcp-publisher.md) (publishing MCP server metadata to the MCP Registry)

## References

[^mcpb-readme]: Model Context Protocol org (GitHub). **modelcontextprotocol/mcpb** — “Desktop Extensions: One-click local MCP server installation in desktop apps” (README). https://github.com/modelcontextprotocol/mcpb

[^claude-help-mcpb]: Anthropic (Claude Help Center). **Getting Started with Local MCP Servers on Claude Desktop** (mentions installing a custom extension by selecting a `.mcpb` file and links to MCPB developer documentation). https://support.claude.com/en/articles/10949351-getting-started-with-local-mcp-servers-on-claude-desktop
