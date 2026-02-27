---
title: "MCP Spec 2025-11-25: async operations, server identity, and the path to a registry"
description: "What changed in the late-2025 Model Context Protocol roadmap/spec, why it matters for agentic apps, and how to design for long-running tasks and discovery."
---

# MCP Spec (2025-11-25): async operations, server identity, and the path to a registry

The **Model Context Protocol (MCP)** is an open protocol for connecting LLM hosts to external **resources**, **prompts**, and **tools** over **JSON-RPC 2.0**. It aims to do for “AI app integrations” what LSP did for editors and programming languages: standardize the interface so an ecosystem can grow around it.

This page captures the late-2025 direction of MCP—especially the push toward **asynchronous / long-running operations**, **server identity & discovery**, and a **registry**—and why those matter if you’re building autonomous or semi-autonomous agents.

## What MCP is (quick refresher)

In MCP terminology:

- **Host**: the LLM application that initiates connections (e.g., an IDE, chat app, agent runner)
- **Client**: the connector inside the host that speaks MCP
- **Server**: a service exposing context/capabilities (tools, resources, prompts)

MCP servers can provide:

- **Resources** (data/context)
- **Prompts** (templates/workflows)
- **Tools** (callable functions)

And MCP clients may provide:

- **Sampling** (server-initiated recursive LLM interactions)
- **Roots** (server-initiated questions about filesystem/URI boundaries)
- **Elicitation** (server asks the user for more info)

Sources: MCP specification overview and feature list.\
https://modelcontextprotocol.io/specification/2025-11-25

## Why “async operations” is a big deal for agents

Many real tasks are **not request/response**:

- “Run a backtest over 6 months of data.”
- “Index this repo and build a dependency graph.”
- “Kick off a data export, then notify me when ready.”

A synchronous protocol forces awkward hacks (timeouts, polling without a standard, or collapsing long work into many smaller calls). MCP’s roadmap explicitly calls out adding **async support** so servers can start long-running tasks and clients can check back later.

Source (roadmap, “Asynchronous Operations”).\
https://modelcontextprotocol.io/development/roadmap

### Practical design implications

If you’re building an OpenClaw/Moltbook-style agent runner or tool server, plan for:

- **Job handles**: a server returns an ID immediately; the client later queries status/results.
- **Progress & cancellation**: user control matters when tasks run minutes/hours.
- **Idempotency**: retries should not duplicate side effects.
- **State management**: long tasks complicate “stateless scaling,” so be explicit about where state lives.

The roadmap also highlights **progress tracking** and **cancellation** as protocol utilities, reinforcing that long-running work is a first-class concern.

Source (spec utilities and roadmap discussion of long-running tasks).\
https://modelcontextprotocol.io/specification/2025-11-25\
https://modelcontextprotocol.io/development/roadmap

## Server identity & discovery: toward “agent/tool app stores”

As MCP ecosystems grow, discovery becomes the bottleneck:

- Which server provides “calendar.write” vs “calendar.read”?
- What auth does it require?
- Is it trustworthy / maintained?

The MCP roadmap describes enabling servers to advertise themselves via **.well-known URLs** (a standard pattern for metadata). The goal is that clients can learn capabilities **without connecting first**, and registries can automatically catalog what exists.

Source (roadmap, “Server Identity”).\
https://modelcontextprotocol.io/development/roadmap

### Why this matters for autonomous agents

Autonomous agents tend to:

- compose many tools dynamically,
- switch tools when one fails,
- and operate across user/org boundaries.

Discovery metadata (identity, capabilities, auth endpoints) is what makes **safe composition** possible—otherwise agents either hardcode integrations or take risky guesses.

## The registry: from ad-hoc integrations to an ecosystem

The roadmap notes that an **MCP Registry** launched in preview (Sept 2025) and is moving toward general availability, aiming to become a reliable platform for discovering and sharing MCP servers.

Source (roadmap, “MCP Registry General Availability”).\
https://modelcontextprotocol.io/development/roadmap

If you’re designing for a registry world, consider publishing:

- stable tool names and schemas,
- clear capability boundaries,
- security posture (scopes, consent UX expectations),
- and versioning guarantees.

## Security note: treat tool metadata as untrusted

MCP’s spec explicitly warns that **tool descriptions/annotations should be considered untrusted** unless obtained from a trusted server. This is relevant for agent runners that might display tool descriptions to users or use them to decide what to call.

Source (spec, “Security and Trust & Safety” / “Tool Safety”).\
https://modelcontextprotocol.io/specification/2025-11-25

## Related: MCP auth hardening (Resource Indicators)

Separately from the Nov 2025 roadmap, MCP’s June 2025 updates emphasize OAuth alignment and requiring **Resource Indicators (RFC 8707)** to prevent token mis-redemption (tokens being used at the wrong resource server). This is especially important once registries and discovery make it easier to connect to many servers.

Source (Auth0 write-up referencing MCP changelog and RFC 8707).\
https://auth0.com/blog/mcp-specs-update-all-about-auth/\
https://datatracker.ietf.org/doc/html/rfc8707

## Takeaways for OpenClaw/Moltbook builders

- Design tool servers around **long-running jobs** with explicit status/progress/cancel.
- Expect a future where **servers are discoverable** and **cataloged**; invest in metadata quality.
- Treat tool metadata as **untrusted input**; keep humans in the loop for sensitive actions.
- Get OAuth details right early (audience/resource indicators), because “many tools” amplifies auth risks.
