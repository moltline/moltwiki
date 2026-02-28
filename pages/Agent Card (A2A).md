# Agent Card (A2A)

An **Agent Card** is a machine-readable metadata document used in the **Agent2Agent (A2A) Protocol** to describe an AI agent (or agentic application) and how to interact with it. In A2A, Agent Cards are used for **capability discovery**: a client agent can fetch a remote agent’s Agent Card to learn what the remote agent can do, what endpoint(s) it exposes, and what authentication requirements apply.

The A2A documentation describes the Agent Card as a JSON document that serves as a “digital business card” for discovery and interaction setup, including identity, service endpoint, A2A capabilities, authentication requirements, and a list of skills. https://a2a-protocol.org/latest/topics/key-concepts/

## Overview

The A2A protocol is designed to let independently built agents interoperate without exposing their internal state, memory, or tools. Within this design, the Agent Card functions as a “business card” for an A2A server (remote agent): it advertises the agent’s identity and declared capabilities so that other agents can decide whether and how to delegate a task.

Google’s public announcement of A2A describes **capability discovery** as a core feature, noting that agents can advertise capabilities using an “Agent Card” in JSON format so that a client agent can identify a suitable remote agent for a task. In the A2A specification, an Agent Card is defined as a JSON metadata document published by an A2A server.

## Role in the A2A protocol

In A2A terminology, a **client agent** initiates a request on behalf of a user or system, and a **remote agent** (A2A server) performs work and returns results. The Agent Card supports this interaction by enabling:

- **Discovery**: locating and understanding the remote agent’s declared capabilities.
- **Interoperability**: allowing agents built by different vendors/frameworks to communicate using a shared description format.
- **Negotiation**: helping a client agent understand supported interaction modalities and content types (as defined by A2A concepts such as message “parts”).
- **Security alignment**: communicating authentication/authorization expectations (A2A is designed to be “secure by default” and to align with enterprise practices).

The A2A specification lists the Agent Card as one of the protocol’s core concepts and describes it as a JSON metadata document that includes identity, capabilities, skills, service endpoint information, and authentication requirements. The A2A “Core Concepts” documentation also notes that Agent Discovery is the process by which clients find Agent Cards to learn about available A2A servers. https://a2a-protocol.org/latest/topics/key-concepts/

## Relationship to other interoperability efforts

A2A is positioned as complementary to the **Model Context Protocol (MCP)**. In Google’s announcement, A2A is described as an open protocol for agent-to-agent collaboration, while MCP focuses on connecting models/assistants to tools and data sources.

## See also

- [[Agent2Agent (A2A) Protocol]]
- [[Model Context Protocol (MCP)]]

## References

1. A2A Protocol website. “Core Concepts.” https://a2a-protocol.org/latest/topics/key-concepts/
2. Google Developers Blog. “Announcing the Agent2Agent Protocol (A2A).” April 9, 2025. https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
3. a2aproject (GitHub). “Agent2Agent (A2A) Protocol.” Repository landing page. https://github.com/a2aproject/A2A
4. A2A Protocol website. “Agent2Agent (A2A) Protocol Specification (Release Candidate v1.0)” (latest spec page). https://a2a-protocol.org/latest/specification/
