# Agent2Agent (A2A) Protocol

The **Agent2Agent (A2A) Protocol** is an open protocol for interoperability between independent AI agent systems. It aims to let agents built by different vendors and frameworks discover each other’s capabilities and collaborate on tasks without sharing internal state.

**Type:** Agent interoperability protocol
**Status:** Release candidate (v1.0 spec); latest released version 0.3.0
**Specification:** https://a2a-protocol.org/latest/specification/
**Repository:** https://github.com/a2aproject/A2A

## Background
As “agentic” applications became more common, many systems converged on standards for **agent-to-tool** integration (for example, Model Context Protocol (MCP)). A2A targets a different layer: **agent-to-agent** communication—so one agent can delegate work to another, exchange context, and coordinate progress.

## What it is
A2A defines:

- A **canonical data model** (e.g., tasks, messages, parts, artifacts, agent metadata)
- A set of **core operations** (e.g., send a message, stream updates, fetch task state)
- **Protocol bindings** that map those operations onto concrete transports (e.g., JSON-RPC and other bindings)

The A2A specification describes the protocol as “async first” and “enterprise ready,” emphasizing long-running tasks, modality-agnostic content exchange, and standard web security practices.

## Key concepts
A2A’s specification centers on a few objects:

- **Agent Card**: a JSON metadata document published by an A2A server describing identity, capabilities, endpoint, and authentication requirements.
- **Task**: a stateful unit of work identified by an ID that progresses through a lifecycle.
- **Message**: a turn in the interaction (role: user/agent) composed of one or more **Parts**.
- **Part / Artifact**: content units for text, file references, or structured data; artifacts represent outputs composed of parts.

(These terms are defined in the specification.)\[1\]

## How it works (high level)
1. A client identifies a remote agent and retrieves its **Agent Card** (to learn capabilities and auth requirements).\[1\]
2. The client sends a **message** to initiate work.
3. The remote agent may respond directly or create a **task** for asynchronous processing.
4. For long-running work, updates can be delivered via **streaming** mechanisms and/or **push notifications** (webhooks).\[1\]

## Relationship to MCP
MCP focuses on connecting models/agents to **tools and resources**. A2A focuses on connecting **agents to other agents**, including capability discovery and task coordination. Some systems may use both: MCP for tool access inside an agent, and A2A for collaboration between agents.

## See also
- Model Context Protocol (MCP)

## References
1. A2A Protocol — “Agent2Agent (A2A) Protocol Specification (Release Candidate v1.0)”. https://a2a-protocol.org/latest/specification/
2. a2aproject/A2A (GitHub repository). https://github.com/a2aproject/A2A

## External links
- https://a2a-protocol.org/
