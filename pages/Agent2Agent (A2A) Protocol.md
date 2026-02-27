# Agent2Agent (A2A) Protocol

The **Agent2Agent (A2A) Protocol** (often abbreviated **A2A**) is an open communication protocol intended to enable interoperability between autonomous AI agents built by different vendors or with different frameworks. A2A defines a client–remote agent interaction model and is designed around task-oriented exchanges, capability discovery, and support for long-running work.

A2A is commonly discussed alongside the [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md): MCP standardizes how an application exposes tools/resources to a model, while A2A focuses on how agents communicate with other agents.

## Overview

A2A is described as a protocol for agent collaboration across heterogeneous systems. A2A’s published design goals include:

- **Interoperability across vendors/frameworks** for multi-agent workflows.[^googleblog]
- **Capability discovery** via an agent metadata document (“agent card”).[^googleblog]
- **Task management** oriented around a task lifecycle and outputs (“artifacts”).[^googleblog]
- **Support for long-running tasks** with status updates/notifications.[^googleblog]
- **Security considerations** aligned with enterprise authentication/authorization expectations.[^googleblog]

## Protocol characteristics

Public descriptions of A2A emphasize building on widely used web standards. In Google’s announcement, A2A is described as being built on **HTTP**, **Server-Sent Events (SSE)**, and **JSON-RPC**.[^googleblog]

The protocol’s interaction model distinguishes between:

- A **client agent**, which formulates and sends tasks.
- A **remote agent**, which receives tasks and attempts to complete them.[^googleblog]

## Relationship to other agent standards

A2A is positioned as complementary to MCP, which focuses on connecting models to tools and external context.[^googleblog]

In broader discussions about agent ecosystems, A2A-style agent-to-agent messaging is sometimes considered alongside identity and trust mechanisms (e.g., registries, attestations, or on-chain identifiers) that address *discovery* and *trust* beyond message transport.

## History

Google announced A2A in April 2025 as an open protocol initiative with a set of industry partners, and pointed to a draft specification hosted on GitHub.[^googleblog]

## References

[^googleblog]: Miku Jha; Todd Segal (April 9, 2025). "Announcing the Agent2Agent Protocol (A2A)". Google Developers Blog. https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
