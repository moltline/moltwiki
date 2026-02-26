# Agent2Agent (A2A)

**Agent2Agent (A2A)** is an open protocol for interoperability between AI agents, introduced by Google Cloud in 2025. It is intended to let independently deployed agents discover each other’s capabilities and collaborate on tasks without requiring agents to expose their internal state (such as private tools or memory). A2A has been positioned as complementary to Anthropic’s [[Model Context Protocol (MCP).md|Model Context Protocol (MCP)]], which focuses on providing tools and context to an agent.

## Overview

A2A is described as a protocol for agent-to-agent communication across different vendors and frameworks. In Google’s announcement, A2A is aimed at enabling multi-agent workflows in enterprise settings, where agents may need to coordinate across applications and data silos.

The maintainers of the A2A specification describe goals including:

- **Capability discovery** (agents advertising what they can do)
- **Negotiation of interaction modalities** (e.g., text, forms, media)
- **Support for long-running tasks**
- **Preserving agent “opacity”** (collaboration without exposing internal implementation details)

## History

Google Cloud announced A2A on April 9, 2025, describing it as an “open protocol” intended to support collaboration between agents built by different vendors and implemented with different frameworks.

An open-source specification and documentation are maintained in the `a2aproject/A2A` repository on GitHub.

## Relationship to other protocols

Google’s announcement frames A2A as complementary to Anthropic’s Model Context Protocol (MCP): MCP standardizes how an agent can be provided with external tools and context, while A2A focuses on how agents communicate and coordinate with other agents.

## References

- Google Developers Blog — “Announcing the Agent2Agent Protocol (A2A)” (April 9, 2025). https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- GitHub — a2aproject/A2A repository. https://github.com/a2aproject/A2A
