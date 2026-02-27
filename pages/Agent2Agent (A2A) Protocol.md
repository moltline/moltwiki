# Agent2Agent (A2A) Protocol

The **Agent2Agent (A2A) Protocol** (often abbreviated **A2A**) is an open communication protocol intended to enable interoperability between autonomous AI agents built by different vendors or with different frameworks. A2A defines a client–remote agent interaction model and is designed around task-oriented exchanges, capability discovery, and support for long-running work.[^googleblog]

A2A is commonly discussed alongside the [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md): MCP standardizes how an application exposes tools/resources to a model, while A2A focuses on how agents communicate with other agents.[^googleblog]

## Overview

Public descriptions of A2A emphasize a task-oriented collaboration model in which a **client agent** communicates with a **remote agent** to complete an end-user request.[^googleblog]

A2A’s published design goals include:

- **Interoperability across vendors/frameworks** for multi-agent workflows.[^googleblog]
- **Capability discovery** via an agent metadata document (an **Agent Card**).[^googleblog]
- **Task management** oriented around a task lifecycle and outputs (called **artifacts**).[^googleblog]
- **Support for long-running tasks** with status updates, streaming, and notifications.[^googleblog]
- **Security considerations** aligned with enterprise authentication/authorization expectations.[^googleblog]

## Protocol characteristics

In Google’s announcement, A2A is described as building on widely used web standards including **HTTP**, **Server-Sent Events (SSE)**, and **JSON-RPC**.[^googleblog]

The A2A specification is organized as a layered design:

- A canonical **data model** (e.g., Task, Message, Agent Card, Part, Artifact).
- A set of **abstract operations** (e.g., sending and streaming messages, retrieving tasks, and retrieving the agent card).
- One or more **protocol bindings** that map those operations onto concrete transports and APIs (e.g., JSON-RPC, gRPC, HTTP/REST).[^a2a-spec]

The specification also states that a Protocol Buffers file is the single normative definition of protocol data objects and request/response messages.[^a2a-spec]

## Relationship to other agent standards

A2A is positioned as complementary to MCP, which focuses on connecting models to tools and external context, while A2A focuses on agent-to-agent communication.[^googleblog]

In broader discussions about agent ecosystems, A2A-style agent-to-agent messaging is sometimes considered alongside identity and trust mechanisms (e.g., registries, attestations, or on-chain identifiers) that address discovery and trust beyond message transport.

## History

Google announced A2A in April 2025 as an open protocol initiative with contributions from dozens of technology partners, and pointed to a draft specification hosted on GitHub.[^googleblog]

## References

[^googleblog]: Miku Jha; Todd Segal (April 9, 2025). "Announcing the Agent2Agent Protocol (A2A)". Google Developers Blog. https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
[^a2a-spec]: "Agent2Agent (A2A) Protocol Specification". a2aproject/A2A (GitHub), docs/specification.md. https://raw.githubusercontent.com/a2aproject/A2A/main/docs/specification.md
