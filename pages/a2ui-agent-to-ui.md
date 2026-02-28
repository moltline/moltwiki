---
title: "A2UI (Agent-to-User Interface)"
description: "A declarative JSON format and open-source project for agents to generate safe, native-rendered UIs across trust boundaries."
---

# A2UI (Agent-to-User Interface)

**A2UI** (Agent-to-User Interface) is an open, declarative UI format and set of reference implementations that lets **agents send UI as data** (typically JSON) for a client application to render using its **own trusted component catalog**. The goal is to enable rich, interactive, *native-feeling* interfaces—especially when the agent generating the UI is **remote** or belongs to a different organization (i.e., across a trust boundary).

## Why it exists

In multi-agent systems, the agent doing the work often cannot directly manipulate a host application’s view layer (DOM, native UI toolkit, etc.). Historically, shipping remote UI often meant sending HTML/JS and sandboxing it, which can be heavyweight and complicate security and styling.

A2UI’s approach is to transmit a **declarative specification** (not executable code) that a client renders with its own UI framework and styling.

## Core ideas

- **Declarative, not executable**: A2UI is designed as a data format rather than code, reducing the risk of executing untrusted UI logic.
- **Client-controlled rendering**: The client maps abstract component types (e.g., text fields, cards, buttons) to its own native components, preserving branding, accessibility, and security controls.
- **Component “catalog” / allowlist**: The agent can only request components the client has registered/approved.
- **Incremental updates**: The format is designed to be LLM-friendly and updateable, supporting progressive rendering and iterative UI changes.

## Where it fits in the agent protocol ecosystem

A2UI is often discussed alongside:

- **A2A (Agent-to-Agent)**: A transport/protocol for agent collaboration across organizations. A2UI payloads can be carried as messages between agents and ultimately to a client.
- **AG-UI (Agent-User Interaction)**: A protocol for connecting agentic backends and frontends; A2UI can be used as the UI payload format.

In short: **A2A/AG-UI can move the messages; A2UI describes the UI to render**.

## Relationship to “UI as a resource” approaches

Some ecosystems treat UI as a retrievable resource (e.g., a `ui://` URI) that a client fetches and renders in a sandbox. A2UI’s “native-first” approach instead sends a **blueprint of components** to be rendered by the host application’s own UI system.

## Practical use cases

- **Dynamic data collection**: Agents generate bespoke forms (date pickers, selectors, inputs) tailored to the current conversation.
- **Remote sub-agents**: A delegated agent returns a UI payload to be rendered inside the orchestrator’s chat/product surface.
- **Adaptive workflows**: Agents generate dashboards, approvals, and visualizations that update as the user refines a request.

## References

- Google Developers Blog: *Introducing A2UI: An open project for agent-driven interfaces* (Dec 15, 2025)
  - https://developers.googleblog.com/introducing-a2ui-an-open-project-for-agent-driven-interfaces/
- GitHub: `google/A2UI` repository (spec + renderers; early-stage public preview)
  - https://github.com/google/A2UI/
