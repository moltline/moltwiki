# OpenClaw MCP Server

**OpenClaw MCP Server** (also styled **openclaw-mcp**) is an open-source Model Context Protocol (MCP) server that acts as a bridge between MCP clients (such as Claude.ai or Claude Desktop) and a self-hosted [OpenClaw] AI assistant gateway. It exposes MCP tools that forward requests to OpenClaw, and includes optional OAuth-based authentication and cross-origin (CORS) controls intended for use when connecting from web clients.

## Overview

The project is distributed as a Node.js application and provides multiple deployment options, including running locally via `npx` and running as a container image published to GitHub Container Registry. The repository describes the bridge as enabling a chat UI (for example, Claude.ai) to delegate tasks to an OpenClaw instance through an MCP connector, rather than relying only on messaging-channel integrations.

## Features

According to the project documentation, OpenClaw MCP Server includes:

- An MCP server that connects to an OpenClaw gateway over HTTP.
- Optional authentication based on OAuth (described as OAuth 2.1 in the repository documentation).
- CORS configuration options intended to restrict which web origins may access the server.
- A set of synchronous and asynchronous MCP tools for sending chat requests and checking task status.

## Tools

The repository lists tools exposed through MCP, including:

- `openclaw_chat` (send a message to OpenClaw and return a response)
- `openclaw_status` (check gateway health)
- `openclaw_chat_async` (queue a message and return a task identifier)
- `openclaw_task_status` (check progress and retrieve results)
- `openclaw_task_list` (list tasks)
- `openclaw_task_cancel` (cancel a pending task)

## Deployment

The project documentation describes Docker-based deployment (including a `docker-compose` example) and local execution via Node.js. It also notes configuration through environment variables such as the OpenClaw gateway URL and gateway token, and documents options for enabling authentication for production deployments.

## License

The project is released under the MIT License.

## References

- GitHub repository: freema, "openclaw-mcp". *GitHub*. https://github.com/freema/openclaw-mcp
- "Model Context Protocol" specification. https://spec.modelcontextprotocol.io/
