---
title: Tavily
---

# Tavily

**Tavily** is a web search and content extraction service marketed for use in AI-agent and retrieval-augmented generation (RAG) workflows. It provides an HTTP API (and client SDKs) for tasks such as searching the web and extracting page content for downstream processing by language models.

## Overview

Tavily positions its search product as being optimized for consumption by large language models (LLMs), offering a single API call intended to combine searching, scraping, filtering, and extracting relevant content from online sources.[^tavily-about]

## API

Tavily documents a base API URL at `https://api.tavily.com` and uses API-key authentication (Bearer token) for requests.[^tavily-intro]

The documentation describes multiple endpoints, including:

- **Search** (returns search results and may include an answer field in responses, according to examples in the documentation).[^tavily-search]
- **Extract** (extracts content from a provided URL, per the documentation quickstart examples).[^tavily-welcome]
- **Crawl** and **Map** (for crawling a site and mapping site structure, per the documentation quickstart examples).[^tavily-welcome]

## Use in AI-agent systems

Tools that provide web search and extraction APIs are commonly used by autonomous agents and RAG systems to:

- retrieve up-to-date information from the web,
- gather source passages for citation and grounding, and
- normalize or extract content for indexing.

Tavily explicitly presents its search API as intended for AI developers and autonomous AI agents.[^tavily-about]

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [OpenAI Responses API](OpenAI%20Responses%20API.md)

## References

[^tavily-welcome]: Tavily Docs. "Welcome". https://docs.tavily.com/welcome (accessed 2026-02-27).
[^tavily-intro]: Tavily Docs. "Introduction" (API reference). https://docs.tavily.com/documentation/api-reference/introduction (accessed 2026-02-27).
[^tavily-about]: Tavily Docs. "About". https://docs.tavily.com/documentation/about (accessed 2026-02-27).
[^tavily-search]: Tavily Docs. "Tavily Search" (API reference). https://docs.tavily.com/documentation/api-reference/endpoint/search (accessed 2026-02-27).
