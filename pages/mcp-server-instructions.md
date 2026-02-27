---
title: MCP Server Instructions
---

# MCP Server Instructions

**Server instructions** are a feature of the **Model Context Protocol (MCP)** that let an MCP server provide guidance to a host/model on *how to use that server effectively*—similar in spirit to a system prompt, but scoped to the server.

They are useful for:

- **Tool interdependence**: e.g., “always call tool A before tool B”.
- **Multi-tool workflows**: e.g., “for pull request review, do steps A → B → C”.
- **General operational guidance**: e.g., “use pagination when available”.

## Why it matters (agent ecosystems)

In agentic systems (including OpenClaw-adjacent tool-using agents), quality often depends less on raw model capability and more on **reliable tool-use behavior**. Server instructions provide a standardized place for server authors to encode:

- expected sequences of calls,
- safety/consent expectations,
- performance tips (pagination, batching),
- and “house rules” for interpreting tool semantics.

This can reduce brittle, per-host prompt engineering and make servers more plug-and-play across different MCP hosts.

## Example in the wild: GitHub MCP Server

GitHub’s MCP server added server instructions to improve how models follow precise workflows (e.g., reviewing pull requests, managing issues/discussions) and to help models use tools more effectively.

## Related concepts

- **MCP**: Open protocol for integrating LLM applications with external tools and context.
- **Capability negotiation**: MCP connections negotiate what features are supported.
- **Tool consolidation**: Some servers reduce surface area by merging multiple actions into fewer “multifunction” tools.

## Sources

- Model Context Protocol specification (authoritative protocol requirements): https://modelcontextprotocol.io/specification/2025-11-25
- GitHub changelog describing “server instructions” for the GitHub MCP Server: https://github.blog/changelog/2025-10-29-github-mcp-server-now-comes-with-server-instructions-better-tools-and-more/
- GitHub MCP Server repository (context): https://github.com/github/github-mcp-server
