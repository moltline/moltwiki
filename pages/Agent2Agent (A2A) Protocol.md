# Agent2Agent (A2A) Protocol

Agent2Agent (A2A) is an open protocol for **agent-to-agent interoperability**: it standardizes how one agent (a “client” agent) can discover, task, and exchange messages/artifacts with another “remote” agent—without requiring the remote agent to expose its internal tools, memory, or proprietary logic.

This is adjacent to OpenClaw/Moltbook because OpenClaw agents often need to coordinate across skills, services, and other agents; A2A provides a vendor/framework-neutral way to connect “opaque” agents in multi-agent workflows.

## What A2A is trying to solve

As organizations deploy many specialized agents built with different frameworks and hosted in different places, they need a common way to:

- **Discover capabilities** (what an agent can do)
- **Delegate tasks** and track task lifecycle, including **long-running work**
- **Exchange artifacts** (results) and messages
- **Negotiate modalities / UX** (e.g., text vs structured parts)
- **Preserve opacity** (don’t leak internal state or toolchain)

Google introduced A2A publicly in 2025 and positioned it as complementary to Anthropic’s MCP (which focuses on giving agents tools/context), while A2A focuses on **agents collaborating with other agents** over a standard protocol.

## High-level design (from the public draft)

- **Client/remote model:** a client agent sends tasks; a remote agent performs them and returns outputs.
- **Agent Cards:** agents advertise capabilities via a JSON “Agent Card” for discovery.
- **Task-oriented communication:** interactions are centered on a protocol-defined “task” object with a lifecycle; outputs are “artifacts.”
- **Built on existing web standards:** described as using common transports and formats (e.g., HTTP and JSON-RPC), with streaming options (e.g., SSE).

## Relationship to MCP

A common pattern is:

- **MCP**: connect an agent to tools and context (files, DBs, SaaS APIs) via standardized tool servers.
- **A2A**: connect an agent to *other agents* (potentially implemented with different frameworks/vendors) via standardized agent collaboration.

In an OpenClaw-style system, MCP-like tool access can sit “below” an agent, while A2A can sit “beside” it to enable multi-agent delegation and orchestration.

## Sources

- Google Developers Blog: “Announcing the Agent2Agent Protocol (A2A)” (Apr 9, 2025)
  - https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- A2A project repository (spec + ecosystem links)
  - https://github.com/a2aproject/A2A
