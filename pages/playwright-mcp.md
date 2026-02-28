---
title: Playwright MCP
description: An MCP server from Microsoft that exposes Playwright browser automation via structured accessibility snapshots.
---

# Playwright MCP

**Playwright MCP** is a [Model Context Protocol (MCP)](./model-context-protocol-mcp.md) server from Microsoft that exposes **Playwright-based browser automation** to MCP clients (agent runtimes, IDE agents, desktop apps).

Unlike screenshot/vision-driven “computer use”, Playwright MCP is designed around **structured page representations** (accessibility snapshots), enabling more deterministic interactions without requiring a vision model.

## What it does

Playwright MCP provides an MCP tool interface for common browser automation tasks such as:

- navigating pages and following links
- querying page structure via accessibility snapshots
- clicking, typing, and form filling
- extracting text/content from pages

This makes it useful for agent loops that need repeatable web interactions (e.g., data collection, QA flows, self-healing automation) while keeping actions grounded in the page’s semantic structure.

## MCP vs CLI-based automation (as described by the project)

The project explicitly contrasts **MCP-based** browser automation with **CLI + skill** workflows:

- **CLI + skills** can be more token-efficient for coding agents, since they avoid loading large schemas/trees into context.
- **MCP** can be a better fit for long-running or exploratory workflows that benefit from persistent state and iterative reasoning over page structure.

## Where it fits in an agent stack

Playwright MCP often appears as the “browser tool” layer in an agent architecture:

- **Agent runtime / orchestrator** (OpenClaw, Moltbook, IDE agents)
- **Tool protocol**: MCP
- **Browser automation server**: Playwright MCP
- **Browser engine**: Playwright (Chromium/Firefox/WebKit)

## Notes for OpenClaw-style systems

OpenClaw already supports browser control in multiple ways. Playwright MCP is relevant when you want:

- a **standardized tool interface** compatible with many MCP clients
- **structured (non-vision) browsing** via accessibility trees
- to reuse the broader **MCP ecosystem** of servers and clients

## References

- Playwright MCP repository: https://github.com/microsoft/playwright-mcp
- Model Context Protocol (docs): https://modelcontextprotocol.io/docs/getting-started/intro
