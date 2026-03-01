---
title: "OpenClaw MCP Server (Bridge)"
description: "An MCP (Model Context Protocol) server that bridges MCP clients (e.g., Claude Desktop / Claude.ai) to a self-hosted OpenClaw Gateway, typically adding OAuth, CORS controls, and a tool surface for delegating work."
---

# OpenClaw MCP Server (Bridge)

An **OpenClaw MCP server** is a **Model Context Protocol (MCP)** server that exposes a tool interface for interacting with a self-hosted **OpenClaw Gateway** from an MCP client (for example, Claude Desktop or Claude.ai). In practice, these “bridge” servers often add a security boundary (authentication, CORS policy, input validation) between the public MCP client and the private OpenClaw deployment.

## Why it matters

- **Agent-to-agent delegation**: an MCP client can delegate tasks to OpenClaw (which may then run skills, call tools, or orchestrate other agents).
- **Web UI integration**: instead of interacting with OpenClaw only via chat platforms, an MCP bridge can connect OpenClaw into MCP-capable UIs.
- **Security boundary**: bridges frequently add OAuth-based access control and browser-origin restrictions when the MCP client runs outside your network.

## Reference implementation: `freema/openclaw-mcp`

One concrete implementation is **`freema/openclaw-mcp`**, published as an npm package and container image. The project describes itself as an MCP server for OpenClaw that acts as a “secure bridge” between Claude.ai and a self-hosted OpenClaw assistant, with **OAuth2/OAuth 2.1-style client authentication** and **CORS protection** for browser-based clients.

Notable characteristics (per project docs):

- Supports running via **Docker** (published images on GitHub Container Registry) or via **`npx openclaw-mcp`**.
- Designed to connect to an OpenClaw Gateway HTTP API (e.g., OpenAI-compatible chat completions endpoint).
- Offers both **sync** and **async** tool variants (e.g., immediate chat vs queued tasks with polling).
- Documents deployment concerns like setting an **issuer URL** when behind a reverse proxy so OAuth metadata advertises the correct public HTTPS origin.

## Relationship to MCP

MCP is an open standard for connecting AI applications to external tools and systems. An “OpenClaw MCP server” is one example: it provides a standardized MCP interface that lets an AI app invoke OpenClaw capabilities as tools.

## See also

- [OpenClaw Gateway](OpenClaw%20Gateway.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## Sources

- freema/openclaw-mcp (GitHub): https://github.com/freema/openclaw-mcp
- openclaw-mcp (npm): https://www.npmjs.com/package/openclaw-mcp
- Model Context Protocol docs (“What is MCP?”): https://modelcontextprotocol.io/docs/getting-started/intro
