# MCP of MCPs

**MCP of MCPs** is a community-developed tool described as a *meta-server* for the [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md). It aims to aggregate multiple MCP servers behind a single endpoint and provide lightweight discovery and selective loading of tool metadata.

## Overview

As MCP clients connect to increasing numbers of tools, loading full tool schemas and passing large intermediate results through a model context window can increase latency and token usage. MCP of MCPs positions itself as an aggregation layer intended to reduce this overhead by:

- Providing a consolidated view of tools across configured MCP servers.
- Supporting discovery of tools via semantic search.
- Supporting selective loading of tool definitions (schemas) rather than loading all tools up front.
- Providing an execution mechanism intended to move data between tools without serializing intermediate data into model tokens.

## Features

The project documentation describes several tools exposed by the meta-server, including:

- **semantic_search_tools**: searches available tools by intent.
- **get_mcps_servers_overview**: returns a lightweight list of tool names across servers.
- **get_tools_overview**: loads full definitions for a selected subset of tools.
- **run_functions_code**: runs code intended to orchestrate calls across tools.

## Relationship to MCP efficiency work

Anthropic has described a related efficiency pattern for MCP clients: presenting MCP tools as code APIs and executing code outside the model context to avoid loading all tool definitions and to avoid repeatedly serializing large intermediate tool outputs into tokens.

## References

- GitHub: eliavamar, “mcp-of-mcps” (repository) — https://github.com/eliavamar/mcp-of-mcps
- MCP Servers (Awesome MCP Servers directory): “mcp-of-mcps” — https://mcpservers.org/servers/eliavamar/mcp-of-mcps
- Anthropic Engineering: “Code execution with MCP: building more efficient AI agents” — https://www.anthropic.com/engineering/code-execution-with-mcp
