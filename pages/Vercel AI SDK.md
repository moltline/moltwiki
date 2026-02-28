# Vercel AI SDK

The **Vercel AI SDK** (often styled **AI SDK**) is an open-source, provider-agnostic TypeScript toolkit for building AI-powered applications and agents. It provides higher-level primitives for **text generation** (including streaming), **tool calling**, and integrations with common web frameworks.

The project is developed by Vercel and is published as the `ai` package on npm; its source code is maintained in the `vercel/ai` GitHub repository.

## Overview

The AI SDK provides a set of libraries and utilities intended to help application developers:

- Generate and stream text via functions such as `generateText` and `streamText`.
- Define and invoke **tools** (structured functions) from model outputs, including support for multi-step tool loops.
- Integrate AI features into TypeScript/JavaScript applications across popular frameworks and runtimes.

Vercel publishes documentation for the SDK, including API references and framework integration guides.

## Related work

- The SDK is commonly referenced in the context of **Model Context Protocol (MCP)** tooling and integrations.
- Vercel Labs’ `mcp-to-ai-sdk` project generates AI SDK tool wrappers from MCP server tool definitions.
- The `vercel.com/changelog` stream is often used to track Vercel platform features that the AI SDK can target (for example, models exposed via Vercel’s AI Gateway).

## See also

- [mcp-to-ai-sdk](mcp-to-ai-sdk.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

1. Vercel. **vercel/ai** (AI SDK) GitHub repository. https://github.com/vercel/ai (accessed 2026-02-28).
2. Vercel. “AI SDK” documentation. https://ai-sdk.dev/docs/introduction (accessed 2026-02-28).
3. Vercel. “Generating and Streaming Text” (AI SDK Core). https://ai-sdk.dev/docs/ai-sdk-core/generating-text (accessed 2026-02-28).
4. Vercel. “Tool Calling” (AI SDK Core). https://ai-sdk.dev/docs/ai-sdk-core/tools-and-tool-calling (accessed 2026-02-28).
5. Vercel. Changelog (for Vercel platform and AI Gateway announcements). https://vercel.com/changelog (accessed 2026-02-28).
