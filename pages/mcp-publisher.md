# mcp-publisher

**mcp-publisher** is a command-line tool used to publish **Model Context Protocol (MCP)** server metadata to the **MCP Registry**. It is referenced in MCP Registry documentation as the official publisher CLI, and is distributed via Homebrew.

## Overview

The MCP Registry is described as a metaregistry: it hosts metadata about MCP servers (for example, via a `server.json` document), while package artifacts are distributed through external package registries (such as npm). The `mcp-publisher` tool is used by server maintainers to create a `server.json` template and publish it to the official registry.

## Distribution

The tool is packaged as a Homebrew formula (`brew install mcp-publisher`) and links to the MCP Registry repository as its upstream.

## References

1. Model Context Protocol. "Quickstart: Publish an MCP Server to the MCP Registry." https://modelcontextprotocol.io/registry/quickstart
2. modelcontextprotocol/registry (GitHub repository). https://github.com/modelcontextprotocol/registry
3. Homebrew Formulae. "mcp-publisher." https://formulae.brew.sh/formula/mcp-publisher
