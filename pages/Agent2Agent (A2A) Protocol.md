# Agent2Agent (A2A) Protocol

**Agent2Agent (A2A)** is an open protocol intended to enable interoperability between independent AI agent systems ("agentic applications"). It defines a common interaction model so that agents built by different vendors or frameworks can discover one another’s capabilities, exchange messages, and coordinate on tasks over standard web transports—without requiring either side to expose internal state, tools, or implementation details.<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref><ref>https://a2a-protocol.org/latest/specification/</ref>

A2A has been described publicly as complementary to tool/context protocols such as the Model Context Protocol (MCP): MCP focuses on giving an agent access to tools and context, while A2A focuses on agent-to-agent communication across systems.<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref>

## Overview

A2A centers on a **client/remote-agent** model:

- A **client** initiates an interaction on behalf of a user or system.
- A **remote agent (server)** processes the request and returns a direct response or manages work as a **task** (including updates for long-running work).<ref>https://a2a-protocol.org/latest/specification/</ref>

The protocol is designed to support synchronous request/response, streaming updates, and asynchronous patterns for long-running tasks.<ref>https://a2a-protocol.org/latest/specification/</ref>

## Design goals and principles

Public materials and the project specification emphasize reuse of established web standards, an "async-first" orientation for long-running tasks, and modality/content-type awareness for exchanging diverse content types.<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref><ref>https://a2a-protocol.org/latest/specification/</ref>

Commonly cited design principles include:

- **Built on existing standards**, including HTTP(S), JSON-RPC 2.0, and Server-Sent Events (SSE) for streaming updates.<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref><ref>https://a2a-protocol.org/latest/specification/</ref>
- **Capability discovery** via published metadata ("Agent Cards") so clients can identify which remote agent can perform a given kind of work.<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref><ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>
- **Task orientation and asynchronicity**, including long-running tasks with state updates delivered by polling, streaming, or push notifications depending on deployment and binding.<ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref><ref>https://a2a-protocol.org/latest/specification/</ref>
- **Modality/content-type awareness**, supporting exchange of diverse content types using structured message parts ("Parts").<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref><ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>
- **Enterprise-oriented security posture**, with authentication requirements declared in the Agent Card and credentials typically passed via HTTP headers using standard web security practices.<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref><ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>

## Core concepts (high level)

The specification defines several core objects and concepts, including:<ref>https://a2a-protocol.org/latest/specification/</ref><ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>

- **Agent Card**: a JSON metadata document published by an A2A server describing an agent's identity, capabilities, service endpoint, skills, and authentication requirements.<ref>https://a2a-protocol.org/latest/specification/</ref><ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>
- **Message**: a single communication turn between a client and an agent, with a role (for example, "user" or "agent") and content carried in one or more **parts**.<ref>https://a2a-protocol.org/latest/specification/</ref><ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>
- **Part**: the fundamental content container used within messages and artifacts; a part holds exactly one content field (for example, text, a URL reference, inline bytes, or structured data) and may include metadata such as media type and filename.<ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>
- **Task**: a stateful unit of work with a unique ID and defined lifecycle, used to track processing (including long-running operations).<ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>
- **Artifact**: a tangible output produced during task processing (for example, a document or structured data), composed of one or more parts and tied to the task lifecycle.<ref>https://a2a-protocol.org/latest/topics/key-concepts/</ref>

## Status and governance

The A2A project publishes a versioned specification and release notes in its public repository, and a published specification site that tracks versions (including a "latest" view). The specification site also links to a released versioned specification (for example, v0.3.0) and earlier versions.<ref>https://a2a-protocol.org/latest/specification/</ref><ref>https://github.com/a2aproject/A2A</ref>

## History

Google announced A2A publicly in April 2025 as an open protocol for agent interoperability, describing a partner ecosystem contributing to the effort.<ref>https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/</ref>

## References

- A2A Protocol website — "Agent2Agent (A2A) Protocol Specification" ("latest"): https://a2a-protocol.org/latest/specification/
- Google Developers Blog — "Announcing the Agent2Agent Protocol (A2A)" (Apr 9, 2025): https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- a2aproject/A2A (GitHub repository): https://github.com/a2aproject/A2A

## Ecosystem and participation

Google’s announcement stated that the protocol launch involved “more than 50 technology partners.”\
Source: https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
