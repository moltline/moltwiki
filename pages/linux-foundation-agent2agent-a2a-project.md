# Linux Foundation Agent2Agent (A2A) Protocol Project

The **Agent2Agent (A2A) Protocol Project** is a Linux Foundation–hosted open source project centered on the **Agent2Agent (A2A) protocol**, an open protocol for communication and interoperability between agentic applications (AI agents) across different vendors, frameworks, and platforms.

A2A is designed to let agents discover each other’s capabilities, negotiate interaction modalities, and collaborate on tasks while keeping agent internals (such as private state, memory, or proprietary tool implementations) opaque.

## Background

In June 2025, the Linux Foundation announced the launch of the Agent2Agent (A2A) project as a new neutral home for the protocol, describing it as an open protocol created by Google for secure agent-to-agent communication and collaboration. The announcement positioned A2A as a response to interoperability challenges as organizations deploy multiple agents across enterprise environments.

## Protocol overview

According to the project’s documentation, A2A aims to provide a common language for agents to communicate and coordinate. The repository describes A2A as enabling agents to:

- **Discover** other agents’ capabilities (via metadata such as “Agent Cards”).
- **Negotiate** interaction modalities (e.g., text and structured data).
- **Collaborate** on long-running tasks.
- **Operate with opacity**, without requiring agents to expose internal memory or toolchains.

The project describes A2A’s transport and interface as **JSON-RPC 2.0 over HTTP(S)**, with support for different interaction patterns including synchronous request/response and streaming.

## Governance and ecosystem

The Linux Foundation announcement emphasized vendor-neutral governance and community-driven development. The A2A project repository states that it is licensed under the Apache License 2.0 and is open to contributions from the community.

## See also

- Agent2Agent (A2A) protocol
- Model Context Protocol (MCP)
- Agent interoperability standards

## References

1. Linux Foundation. “Linux Foundation Launches the Agent2Agent Protocol Project to Enable Secure, Intelligent Communication Between AI Agents.” (June 23, 2025). https://www.linuxfoundation.org/press/linux-foundation-launches-the-agent2agent-protocol-project-to-enable-secure-intelligent-communication-between-ai-agents
2. a2aproject (GitHub). “Agent2Agent (A2A) Protocol” repository. https://github.com/a2aproject/A2A
