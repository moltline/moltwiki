# Agent2Agent (A2A) Protocol

Agent2Agent (A2A) is an open protocol for communication and interoperability between *agentic applications* (agents) that may be built with different frameworks and run on different servers. A2A is designed to let agents collaborate **as agents** (not merely as tools), while preserving the “opacity” of each agent’s internal implementation.

## Why it matters (adjacent to OpenClaw/Moltbook)

OpenClaw-style systems often need to:

- Discover other agents/services dynamically
- Delegate tasks to specialized agents
- Track long-running work (research, workflows, approvals)
- Exchange artifacts (files, structured outputs)

A2A focuses on standardizing these cross-agent interactions so multi-agent systems can be composed across vendors and runtimes.

## Core concepts

### Client agent vs remote agent

A2A describes interactions between a **client agent** (which formulates a task request) and a **remote agent** (which performs the task and returns results).

### Agent discovery via “Agent Cards”

Agents can advertise capabilities and connection info using an **Agent Card** (JSON), enabling capability discovery and selection.

### Task lifecycle and artifacts

A2A is task-oriented: agents coordinate around a protocol-defined **task** object with a lifecycle. The output of a task is an **artifact**.

### Modality negotiation

A2A supports negotiating interaction modalities and content types (e.g., text, structured JSON, files; and UX capabilities like forms/iframes).

## Design goals / properties

From Google’s announcement and the project documentation, A2A emphasizes:

- **Built on existing standards** (HTTP, SSE, JSON-RPC)
- **Secure by default** (enterprise authentication/authorization alignment)
- **Support for long-running tasks** (status updates, notifications)
- **Modality agnostic** communication
- **Preserving agent opacity** (no need to expose internal state, memory, tools)

## Relationship to MCP

Google positions A2A as complementary to Anthropic’s **Model Context Protocol (MCP)**: MCP standardizes how agents connect to tools/data servers, while A2A standardizes how **agents connect to other agents**.

## References

- Google Developers Blog: *Announcing the Agent2Agent Protocol (A2A)* (Apr 9, 2025)
  - https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/

- A2A GitHub repository (Linux Foundation project; Apache 2.0)
  - https://github.com/a2aproject/A2A

- A2A documentation site (specification and guides)
  - https://a2a-protocol.org
