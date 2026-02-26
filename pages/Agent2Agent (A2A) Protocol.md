# Agent2Agent (A2A) Protocol

The **Agent2Agent (A2A) Protocol** (**A2A**) is an open communication protocol for interoperability between independent AI agent systems. It is intended to let agents built by different vendors or frameworks discover each other’s capabilities, exchange messages, and coordinate work—without requiring agents to expose internal state such as private memory, proprietary reasoning, or tool implementations.

## Overview

A2A is designed around a **client agent** initiating a **task** with a **remote agent** (server). The protocol defines a task lifecycle and a structured message model so that agents can collaborate on both short and long-running work.

Google Cloud announced A2A in April 2025 as an open protocol to support multi-agent interoperability in enterprise settings, and positioned it as complementary to Anthropic’s [[Model Context Protocol (MCP)]], which standardizes how hosts connect to tools and context.

## Design goals and characteristics

A2A’s published goals and design principles include:

- **Interoperability across agent implementations** (different frameworks, languages, and vendors).
- **Capability discovery** via metadata documents ("Agent Cards") that describe an agent’s skills and connection details.
- **Task-oriented collaboration**, including support for **long-running tasks** with state updates.
- **Use of existing web standards**, including **HTTP** and **JSON-RPC 2.0**; the specification also describes streaming updates (e.g., via Server-Sent Events).
- **Security considerations**, aiming to support enterprise authentication and authorization patterns.

## Specification

The A2A project publishes an open specification and reference materials in a public repository. The documentation site presents a versioned specification and describes a layered approach:

- A canonical **data model** (e.g., tasks, messages, parts, artifacts)
- Abstract **operations** (e.g., sending messages, getting tasks)
- Concrete **protocol bindings** (e.g., JSON-RPC)

## Ecosystem

The A2A repository links to multiple SDKs and example implementations intended to help developers expose agents as A2A servers and build A2A clients.

## See also

- [[Model Context Protocol (MCP)]]

## References

- Google Cloud. “Announcing the Agent2Agent Protocol (A2A).” (Apr 9, 2025). https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- a2aproject. “Agent2Agent (A2A) Protocol” (GitHub repository). https://github.com/a2aproject/A2A
- A2A Protocol Documentation Site. “Agent2Agent (A2A) Protocol Specification.” https://a2a-protocol.org/latest/specification/
- JSON-RPC Working Group. “JSON-RPC 2.0 Specification.” https://www.jsonrpc.org/specification
