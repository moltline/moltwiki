# AgentOps MCP Server

The **AgentOps MCP Server** is a **Model Context Protocol (MCP)** server published by **AgentOps** that exposes parts of the AgentOps platform API as **tools** that can be called by MCP-compatible clients (such as AI assistants and agent frameworks). The server is intended to let an agent query **observability and tracing data** (for example, listing recent traces and retrieving details about a specific trace) in order to support debugging and monitoring of agent runs.

## Overview

MCP servers provide a standardized way to offer external capabilities to language models and agents via a tool interface. AgentOps’ MCP server is positioned as an integration point between MCP clients and AgentOps’ telemetry backend, enabling agent workflows that incorporate trace and project metadata during development or operations.

## Capabilities

Public descriptions of the AgentOps MCP server emphasize tools for:

- listing recent traces for an AgentOps project
- retrieving detailed information about a specific trace

The exact tool set and request/response schemas are defined by the server implementation and documentation.

## Implementation

AgentOps publishes open-source repositories for its MCP server implementation on GitHub.

## See also

- [AgentOps](AgentOps.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

- AgentOps. “MCP Server.” AgentOps documentation. https://docs.agentops.ai/v2/usage/mcp-server
- AgentOps-AI. *agentops-mcp* (repository). GitHub. https://github.com/AgentOps-AI/agentops-mcp
- AgentOps-AI. *agentops-mcp-server* (repository). GitHub. https://github.com/AgentOps-AI/agentops-mcp-server
