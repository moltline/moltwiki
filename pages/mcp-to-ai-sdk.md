# mcp-to-ai-sdk

**mcp-to-ai-sdk** is a command-line tool from Vercel Labs that generates [Vercel AI SDK](https://github.com/vercel/ai) tool wrappers (“stubs”) from a [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md) server’s tool definitions. Its authors describe it as “shadcn for MCP”.

The project’s stated goal is to make MCP tools easier to consume in applications built with the Vercel AI SDK, while reducing risks from dynamic tool discovery (for example, unexpected changes to tool schemas or the appearance of new tools).

## Overview

MCP clients can typically discover available tools from an MCP server at runtime. mcp-to-ai-sdk instead generates a local file tree containing:

- A shared MCP client for the target server.
- Per-tool wrapper modules that expose each MCP tool as a Vercel AI SDK `tool(...)`.
- An index module that exports all generated tools for that server.

The generated wrappers call the MCP server’s `callTool` method and normalize returned content into strings for use by AI SDK runtimes.

## Rationale

The project frames static generation as a way to reduce security, cost, and quality issues that can arise when tool names/descriptions/schemas are loaded dynamically into an agent’s context and change without review.

Commonly cited motivations include:

- **Prompt-injection risk reduction:** avoid unreviewed changes to upstream tool descriptions being incorporated into an agent prompt.
- **Capability surface control:** avoid newly added tools (e.g., destructive operations) becoming implicitly available.
- **Customization:** allow narrowing arguments or overriding generated implementations (for example, restricting queries to a single tenant).
- **Context efficiency:** reduce context use from including unneeded tool definitions.

## Usage

The repository documents usage via `npx`, passing either an MCP URL (HTTP endpoints use Streamable HTTP by default) or a local server path (stdio transport). It also supports Server-Sent Events transport and sending HTTP headers for authenticated MCP endpoints.

Examples from the repository:

```bash
# Generate wrappers for HTTP MCP endpoints (Streamable HTTP by default)
npx mcp-to-ai-sdk@latest https://mcp.grep.app

# Use Server-Sent Events transport
npx mcp-to-ai-sdk@latest --sse https://example.com/mcp/sse

# Generate wrappers for local MCP servers (stdio)
npx mcp-to-ai-sdk@latest /path/to/mcp-server.js

# Add authentication headers for protected MCP endpoints
npx mcp-to-ai-sdk@latest -H 'Authorization: Bearer your-token' https://api.example.com/mcp
```

The generated output includes a per-server `client.ts` plus per-tool wrappers and an index export (for example, `mcps/mcp.grep.app/client.ts`, `mcps/mcp.grep.app/index.ts`).

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [MCP Registry](MCP%20Registry.md)
- Vercel AI SDK

## References

1. Vercel Labs. “MCP to AI SDK (mcp-to-ai-sdk)”. GitHub repository. https://github.com/vercel-labs/mcp-to-ai-sdk (accessed 2026-02-28).
2. Vercel. “Addressing security & quality issues with MCP tools in AI Agent”. (Sep 17, 2025). https://vercel.com/blog/generate-static-ai-sdk-tools-from-mcp-servers-with-mcp-to-ai-sdk (accessed 2026-02-28).
