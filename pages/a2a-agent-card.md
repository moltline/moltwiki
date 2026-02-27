---
title: "A2A Agent Card"
description: "The Agent Card is A2A’s discovery document (often served from /.well-known/agent.json) that advertises an agent’s capabilities, skills, and security requirements."
---

# A2A Agent Card

In the **Agent2Agent (A2A) protocol**, an **Agent Card** is a machine-readable **discovery document** (typically JSON) that describes **what an agent can do** and **how to connect to it**. It is intended to let a “client agent” discover a “remote agent” without prior out-of-band configuration.

A2A documentation and community write-ups commonly describe serving the Agent Card from a well-known URL such as:

- `/.well-known/agent.json`

## What an Agent Card contains

While exact fields depend on the A2A spec version, an Agent Card is generally described as including:

- **Identity & metadata**: name, description, version
- **Connection info**: the agent’s base URL / endpoint
- **Capabilities**: e.g., whether streaming is supported
- **Security schemes**: authentication/authorization requirements (often aligned with common API auth patterns)
- **Skills catalog**: a structured list of tasks the agent can perform, plus supported input/output modes and examples

The **skills** section is central: it helps other agents decide *which* agent to call for a task, and how to format requests and interpret responses.

## Why it matters

Agent Cards are the foundation of **dynamic agent discovery**:

- **Delegation**: a planner/supervisor agent can choose a specialist agent based on advertised skills.
- **Interoperability**: agents from different vendors can interoperate if they publish compatible Agent Cards.
- **Governance**: enterprises can curate/approve Agent Cards in registries and control which agents are discoverable.

## Relationship to adjacent concepts

- **MCP tool manifests vs. A2A Agent Cards**: MCP focuses on connecting an agent/host to tools and resources; A2A focuses on **agent-to-agent** collaboration. Both rely on structured metadata to enable automation and safe integration.
- **Service discovery**: Agent Cards resemble service discovery documents (like OpenAPI descriptions) but are tailored to agent skills, modalities, and long-running task workflows.

## References

1. Google Developers Blog — *Announcing the Agent2Agent Protocol (A2A)* (Apr 9, 2025). Mentions capability discovery via an “Agent Card” in JSON format. https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
2. A2A draft specification repository (Google). https://github.com/google/A2A
3. Christian Posta (Solo.io) — *Agent Discovery, Naming, and Resolution — the Missing Pieces to A2A* (Jul 8, 2025). Discusses Agent Cards, `/.well-known/agent.json`, and includes an example Agent Card. https://www.solo.io/blog/agent-discovery-naming-and-resolution---the-missing-pieces-to-a2a
