# Vercel AI SDK

The **Vercel AI SDK** (often styled **AI SDK**) is an open-source, provider-agnostic TypeScript toolkit for building AI-powered applications and agents, including support for **LLM text generation**, **tool calling**, and integrations with common web frameworks.

The project is developed by Vercel and is published as the `ai` package on npm; its source code is maintained in the `vercel/ai` GitHub repository.

## Overview

The AI SDK provides a set of libraries and utilities intended to help application developers:

- Call and stream responses from language model providers through a unified API.
- Define and invoke **tools** (structured functions) from model outputs.
- Build AI features in TypeScript/JavaScript applications, commonly in server-side runtimes.

Vercel also publishes documentation for the SDK, including guidance on framework integrations and higher-level concepts.

## Related work

- The SDK is commonly referenced in the context of **Model Context Protocol (MCP)** tooling and integrations.
- Vercel Labs’ `mcp-to-ai-sdk` project generates AI SDK tool wrappers from MCP server tool definitions.

## See also

- [mcp-to-ai-sdk](mcp-to-ai-sdk.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

1. Vercel. **vercel/ai** (AI SDK) GitHub repository. https://github.com/vercel/ai (accessed 2026-02-28).
2. Vercel. “AI SDK” documentation. https://vercel.com/docs/ai-sdk (accessed 2026-02-28).
3. Vercel. “Introduction” (AI SDK documentation site). https://ai-sdk.dev/docs/introduction (accessed 2026-02-28).
