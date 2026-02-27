# Agent2Agent (A2A) Protocol

**Agent2Agent (A2A)** is an open protocol intended to enable interoperability between independent AI agent systems ("agentic applications"). It defines a common interaction model so that agents built by different vendors or frameworks can discover one another’s capabilities, exchange messages, and coordinate on tasks over standard web transports—without requiring either side to expose internal state, tools, or implementation details.\
\
A2A has been described publicly by Google and partners as complementary to tool/context protocols such as the Model Context Protocol (MCP): MCP focuses on giving an agent access to tools and context, while A2A focuses on agent-to-agent communication across systems.

## Overview

A2A centers on a **client/remote-agent** model:

- A **client** initiates an interaction on behalf of a user or system.
- A **remote agent (server)** processes the request and returns a direct response or manages work as a **task** (including updates for long-running work).

The protocol is designed to support synchronous request/response, streaming updates, and asynchronous patterns for long-running tasks.

## Design goals and principles

Public materials and the project specification emphasize:

- **Reuse of existing standards** such as HTTP, JSON-RPC 2.0, and Server-Sent Events (SSE).
- **Capability discovery** so clients can identify which remote agent can perform a given kind of work.
- **Task orientation and asynchronicity**, including long-running tasks with state updates.
- **Modality/content-type awareness**, supporting exchange of diverse content types (for example, text and files referenced in messages).
- **Enterprise-oriented security posture**, aligning with common authentication/authorization practices.

## Core concepts (high level)

The specification describes several core objects and concepts, including:

- **Agent Card**: a JSON metadata document published by an A2A server describing identity, endpoint information, capabilities/skills, and authentication requirements.
- **Message**: a communication turn (for example, user → agent or agent → user) composed of one or more **parts**.
- **Part**: the smallest unit of content within a message or artifact (for example, text, file references, or structured data).
- **Task**: a stateful unit of work with an identifier and lifecycle; a task may complete immediately or run asynchronously.
- **Artifact**: an output produced for a task, composed of parts.

## Status and governance

The A2A project publishes a versioned specification and release notes in its public repository.

## References

- Google Developers Blog — "Announcing the Agent2Agent Protocol (A2A)" (Apr 9, 2025): https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- Agent2Agent (A2A) Protocol — specification and releases (a2aproject/A2A): https://github.com/a2aproject/A2A
- A2A Protocol Specification (published site; versioned): https://a2a-protocol.org/
