---
title: "Agent Registration and Discovery Protocol (ARDP)"
description: "An IETF Internet-Draft proposing a lightweight control-plane protocol for registering and discovering autonomous software agents with stable identities and capability-based resolution."
---

# Agent Registration and Discovery Protocol (ARDP)

**Agent Registration and Discovery Protocol (ARDP)** is an IETF Internet-Draft (Informational) that proposes a lightweight **control-plane** protocol for **registering**, **discovering**, and **resolving endpoints** for autonomous software agents operating in distributed and federated environments.

ARDP’s stated focus is to provide:

- **Stable agent identities** with **dynamic reachability** (agents can move while their identifier stays stable)
- **Capability advertisement** (including the ability to select among interaction protocols such as **MCP**, **A2A**, **HTTP**, and **gRPC**)
- Minimal **presence/health** signaling
- **Security-first** discovery controls and federation-friendly operation

The draft explicitly does **not** define agent-to-agent task execution or tool invocation; instead, it positions itself as complementary to interaction protocols (e.g., MCP and A2A).

## Why it matters

As agent ecosystems grow, a recurring gap is **how to find and reach an agent** reliably when its runtime endpoint changes, while also controlling discovery for privacy and security. ARDP frames this as a control-plane problem and proposes a protocol surface for:

- **Registering** an agent with an authority (with TTL/refresh semantics)
- **Resolving** an agent identifier to current endpoints
- **Querying** by capabilities, with privacy defaults/redaction
- Supporting **federation** across administrative domains

## Core concepts (from the draft)

- **Agent Identity**: defines an agent identifier syntax (“AID”) and canonical form.
- **Registration model**: operations such as **REGISTER** and **DEREGISTER**, plus TTL/refresh.
- **Discovery and resolution**: operations such as **RESOLVE** and **QUERY**.
- **Capabilities**: a capability schema and bindings intended to enable protocol selection.
- **Security considerations**: includes “proof of control” mechanisms (e.g., signed payloads) and authorization scopes for discovery.

## Relationship to other protocols

ARDP is described as **transport-agnostic** and complementary to agent interaction protocols. In particular, it calls out protocol selection among:

- **Model Context Protocol (MCP)**
- **Agent2Agent (A2A)**
- **HTTP**
- **gRPC**

## Status

ARDP is currently published as an **Internet-Draft** (“work in progress”) and may change or be replaced.

## References

- R. Pioli, *Agent Registration and Discovery Protocol (ARDP)*, Internet-Draft (Informational), February 2026. IETF Datatracker: https://datatracker.ietf.org/doc/draft-pioli-agent-discovery/01/
