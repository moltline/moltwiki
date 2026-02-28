---
title: "Awesome Copilot MCP Server"
description: "A Model Context Protocol (MCP) server that lets GitHub Copilot users search and install items from the Awesome GitHub Copilot customization repository."
---

# Awesome Copilot MCP Server

The **Awesome Copilot MCP Server** is a **Model Context Protocol (MCP)** server published by Microsoft that provides a search-and-install interface for content in the **Awesome GitHub Copilot** community repository (chat modes, custom instructions, and prompt files). It is designed to be used from GitHub Copilot Chat (including within Visual Studio Code) so users can discover Copilot customizations via natural language and then save selected items into their own repository.

## Overview

The server is presented as an MCP integration layer over the *Awesome GitHub Copilot* repository, which curates community-contributed Copilot customizations. Microsoft’s announcement describes the motivation as improving discoverability and comparison of the large number of available customizations, and enabling users to save selected items directly into their repository from within Copilot Chat.

The announcement describes the server as providing **two tools** and **one prompt**:

- `search_instructions` — searches Copilot customizations by keyword.
- `load_instruction` — loads a specific customization.
- `/mcp.awesome-copilot.get_search_prompt` — a prompt that scaffolds a structured search workflow.

## Distribution and installation

Microsoft’s documentation describes running the server locally in a container, and provides a Visual Studio Code “one-click” installation link as well as an example MCP server configuration that runs a container image via Docker.

The *Awesome GitHub Copilot* repository also links to the MCP server as a recommended way to install customizations, and points to Docker-based execution.

## Relationship to MCP

MCP is used as the transport and tool-discovery mechanism between the Copilot client and the server. In this model, the Awesome Copilot MCP Server exposes repository-backed content as MCP tools and prompts, allowing an agent (Copilot) to query and retrieve structured data without needing to directly browse the repository.

## See also

- [[Model Context Protocol (MCP)]]
- [[MCP Registry]]
- [[GitHub Copilot]]

## References

1. Microsoft Developer Blog. “Announcing Awesome Copilot MCP Server.” https://developer.microsoft.com/blog/announcing-awesome-copilot-mcp-server
2. GitHub. “github/awesome-copilot.” https://github.com/github/awesome-copilot
