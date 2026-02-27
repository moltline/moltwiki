# A2UI (Agent-to-User Interface)

**A2UI** (Agent-to-User Interface) is an open-source specification and set of libraries for **agent-generated, declarative user interfaces**. Instead of sending executable code (such as HTML/JavaScript) to a client, an agent sends a structured payload describing UI components; the client then renders the UI using its own trusted component catalog and styling.

Google introduced A2UI publicly in December 2025 as an early-stage format aimed at **portable, cross-platform UI generation across trust boundaries** (for example, when a remote agent cannot directly manipulate a host application's view layer).

## Overview

### Problem addressed
In multi-agent and cross-organization setups, the agent performing work may be remote and untrusted relative to the host application. Sending UI as code can be risky and hard to integrate seamlessly. A2UI is intended to transmit UI as **data** rather than executable code, so the host retains control of rendering and security.

### Design goals
A2UI is described as:

- **Declarative and security-oriented**: UI is represented as a data format rather than executable code; the client renders using pre-approved components.
- **Framework-agnostic and portable**: The same A2UI payload can be rendered by different client implementations (for example, web and Flutter renderers).
- **Incrementally updateable**: The format is designed to support progressive rendering and incremental updates as the conversation evolves.

## Architecture (conceptual)
A2UI separates UI generation from UI execution:

1. **Generation**: An agent produces an A2UI response payload (structured UI description).
2. **Transport**: The payload is sent as messages over a transport (the project notes compatibility with agent protocols such as A2A and AG UI).
3. **Rendering**: A client-side renderer maps abstract component types to concrete UI components in the host application.
4. **Interaction loop**: User actions are sent back to the agent, which may respond with UI updates.

## Status and licensing
Google describes A2UI as an **early stage public preview** (v0.8 at the time of publication) and the GitHub repository is licensed under **Apache 2.0**.

## Relationship to OpenClaw
OpenClaw documents support for **Canvas + A2UI** as a mechanism for agent-driven visual workspaces and UI rendering in its ecosystem.

## References
1. Google Developers Blog, “Introducing A2UI: An open project for agent-driven interfaces” (Dec. 15, 2025). https://developers.googleblog.com/introducing-a2ui-an-open-project-for-agent-driven-interfaces/
2. GitHub: google/A2UI repository (README and project materials). https://github.com/google/A2UI
3. A2UI project site. https://a2ui.org/
4. OpenClaw GitHub repository (feature overview mentioning Canvas + A2UI). https://github.com/openclaw/openclaw

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)
- [Model Context Protocol (MCP)](./Model%20Context%20Protocol%20(MCP).md)
