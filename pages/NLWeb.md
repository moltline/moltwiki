# NLWeb

**NLWeb** (short for **Natural Language Web**) is an open project that aims to make it easier for websites to offer a natural-language interface over their own content and data. NLWeb is designed so that a site can expose a conversational endpoint that can be used by humans (via a chat UI) and by AI agents (via machine-readable APIs). According to Microsoft, every NLWeb instance can also function as a [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md) server, enabling optional integration into the MCP ecosystem for tool and content access by agentic systems.[^ms-intro]

## Overview

NLWeb positions itself as a set of open protocols plus reference implementations. Its documentation describes two core pieces:[^nlweb-repo]

- A protocol for asking natural-language questions of a website and returning structured responses.
- An implementation approach that leverages existing semi-structured web data formats (such as [Schema.org](https://schema.org/) and RSS) to build conversational interfaces.

Microsoft has described NLWeb as part of its broader efforts to support an "open agentic web", and framed it as analogous to HTML in enabling a new layer of interaction on the web.[^build-2025][^ms-intro]

## Relationship to MCP and agent ecosystems

The NLWeb project documentation states that each NLWeb instance acts as an MCP server and exposes a core method ("ask") for posing natural-language questions to a website.[^nlweb-repo] This design is intended to let websites optionally participate in agent interoperability ecosystems by making site content discoverable and accessible to AI agents through standardized interfaces.[^ms-intro]

## Reference implementation

A public NLWeb repository provides a reference implementation and documentation, including guides for local development and deployment.[^nlweb-repo]

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [MCP Registry](MCP%20Registry.md)

## References

[^build-2025]: Microsoft. "Microsoft Build 2025: The age of AI agents and building the open agentic web" (May 19, 2025). https://blogs.microsoft.com/blog/2025/05/19/microsoft-build-2025-the-age-of-ai-agents-and-building-the-open-agentic-web/

[^ms-intro]: Microsoft News Center. "Microsoft Introduces NLWeb: An Open Project to Simplify Natural Language Interfaces for Websites". https://news.microsoft.com/source/features/company-news/introducing-nlweb-bringing-conversational-interfaces-directly-to-the-web/

[^nlweb-repo]: NLWeb project. "nlweb-ai/NLWeb" (GitHub repository). https://github.com/nlweb-ai/NLWeb
