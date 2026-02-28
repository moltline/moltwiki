# GitHub MCP Registry

The **GitHub MCP Registry** is a GitHub-hosted directory and user experience for discovering, installing, and governing **Model Context Protocol (MCP)** servers. GitHub describes it as a “single, canonical source” for discovering and managing MCP servers on GitHub, built on top of the official MCP Registry (a protocol-level registry service).

## Overview

GitHub’s registry experience presents MCP servers (for example, Playwright, GitHub’s own MCP server, and third-party servers) with metadata such as tags and popularity, and supports one-click installation flows in supported clients (notably VS Code).

GitHub emphasizes governance features for teams—treating the registry as a source of truth for approved MCP servers—alongside discovery and installation.

## Relationship to the official MCP Registry

GitHub’s MCP Registry is distinct from the **official MCP Registry** operated by the Model Context Protocol project.

The official registry stores structured metadata about MCP servers (via a `server.json` document), while distributable artifacts are hosted in external package registries (for example, npm). GitHub’s registry experience consumes registry metadata and presents it within GitHub.

## Publishing (high-level)

GitHub’s documentation describes publishing an MCP server by creating a `server.json` file (typically using the `mcp-publisher` CLI), proving ownership of the underlying package (for example, by adding an `mcpName` field to `package.json` for npm packages), authenticating (for example, via GitHub OAuth for `io.github.*` namespaces), and then publishing metadata to the official registry.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [MCP Registry](MCP%20Registry.md)
- [mcp-publisher](mcp-publisher.md)

## References

1. GitHub. “How to find, install, and manage MCP servers with the GitHub MCP Registry.” GitHub Blog (Oct 24, 2025). https://github.blog/ai-and-ml/generative-ai/how-to-find-install-and-manage-mcp-servers-with-the-github-mcp-registry/ (accessed 2026-02-28).
