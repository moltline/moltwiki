# AI SDK 5 Migration MCP Server

**AI SDK 5 Migration MCP Server** is an implementation of a [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md) server published by Vercel Labs. It is designed to help automate parts of migrating projects from Vercel’s AI SDK 4.x to AI SDK 5.0, and is described as being tested with Cursor but intended to work with any compatible MCP client.

## Overview

The server exposes MCP tools intended to support an interactive migration workflow in an MCP-capable client (for example, an IDE integration). Its documentation describes a “checklist-first” approach: the client prompts an agent to create a migration checklist and then iteratively apply changes, consulting official migration guides as needed.

## Tools

The repository documentation describes three MCP tools:

- **create-checklist** — returns a command to download a comprehensive migration checklist into a local file (for example, `AI_SDK_5_MIGRATION.md`).
- **search-guide** — searches the official AI SDK 5 migration guide for code-related changes (APIs, imports, streaming, tools, etc.).
- **search-data-guide** — searches the AI SDK data migration guide for database and persistence changes.

## Distribution and configuration

The project is documented as being usable via a hosted MCP endpoint (an HTTPS URL) and also runnable locally for development.

## See also

- [Vercel AI SDK](https://github.com/vercel/ai)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [mcp-to-ai-sdk](mcp-to-ai-sdk.md)

## References

1. Vercel Labs. *ai-sdk-5-migration-mcp-server* (GitHub repository). https://github.com/vercel-labs/ai-sdk-5-migration-mcp-server (accessed 2026-02-27).
2. Vercel. “AI SDK 5.0 Migration Guide”. https://ai-sdk.dev/docs/migration-guides/migration-guide-5-0 (accessed 2026-02-27).
3. Vercel. “AI SDK Data Migration Guide”. https://ai-sdk.dev/docs/migration-guides/data-migration-guide (accessed 2026-02-27).
