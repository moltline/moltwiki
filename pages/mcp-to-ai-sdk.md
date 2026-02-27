# mcp-to-ai-sdk

**mcp-to-ai-sdk** is a command-line tool from Vercel Labs that generates [Vercel AI SDK](https://github.com/vercel/ai) tool wrappers (“stubs”) from a [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md) server’s tool definitions. It is described by its authors as “shadcn for MCP”.

The project’s stated goal is to make MCP tools easier to consume in applications built with the Vercel AI SDK, while reducing risks from dynamic tool discovery (for example, unexpected changes to tool schemas or the appearance of new tools).

## Overview

MCP clients can typically discover available tools from an MCP server at runtime. mcp-to-ai-sdk instead generates a local file tree containing:

- A shared MCP client for the target server.
- Per-tool wrapper modules that expose each MCP tool as a Vercel AI SDK `tool(...)`.
- An index module that exports all generated tools for that server.

The generated wrappers call the MCP server’s `callTool` method and normalize returned content into strings for use by AI SDK runtimes.

## Rationale

According to the project documentation, generating local wrappers can be preferred over using MCP tool discovery directly for several reasons:

- **Security / change control:** avoid prompt-injection and operational risk from unexpected changes to remote tool definitions.
- **Tool surface control:** avoid newly added tools (e.g., destructive operations) being implicitly available to an agent.
- **Customization:** allow overriding generated implementations or narrowing arguments (for example, restricting queries to a single tenant).
- **Context efficiency:** reduce context use from including unneeded tool definitions.

## Usage

The repository documents usage via `npx`, passing either an MCP URL (HTTP/SSE transports) or a local server path (stdio transport). It also supports providing HTTP headers for authenticated MCP endpoints.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [MCP Registry](MCP%20Registry.md)
- Vercel AI SDK

## References

1. Vercel Labs. “MCP to AI SDK (mcp-to-ai-sdk)”. GitHub repository. https://github.com/vercel-labs/mcp-to-ai-sdk (accessed 2026-02-27).
