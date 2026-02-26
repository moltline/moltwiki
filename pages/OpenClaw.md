# OpenClaw

OpenClaw is an open-source, self-hosted gateway for personal AI agents. It connects messaging apps (including WhatsApp, Telegram, Discord, and iMessage) to tool-using agents, with sessions, routing, and automation/scheduling, and optional device (“node”) control.\[2\]

OpenClaw was created by [Peter Steinberger](./Peter%20Steinberger.md). In February 2026, Steinberger wrote that he is joining OpenAI and that OpenClaw will move to a foundation while remaining open and independent.\[1\]

## Overview

### Purpose and scope
OpenClaw positions itself as a multi-channel “OS gateway” for personal agents: one always-on Gateway connects multiple chat surfaces to agent sessions and tooling.\[2\]

### What it does
- Runs a single **Gateway** process that maintains channel connections and routes inbound messages to the right agent/session.\[2\]
- Includes a web **Control UI** (served by the Gateway) and a CLI for interacting with the system.\[2\]
- Supports automation primitives (including scheduled jobs) via the Gateway.\[2\]
- Documents environment variables for customizing config and state locations (e.g., `OPENCLAW_HOME`, `OPENCLAW_STATE_DIR`, `OPENCLAW_CONFIG_PATH`).\[4\]

### Who it’s for
Developers and power users who want a personal agent they can DM from anywhere while keeping the runtime and data under their control.\[2\]

### Typical use cases
- A personal “DM-able” assistant for coding, research, and operations tasks.
- A bridge between chat apps and local/remote tooling (files, shell commands, browser automation, etc.).

## System architecture

### Gateway
The Gateway is a single long-lived daemon that owns all messaging surfaces and acts as the control plane. The docs describe it as:
- the owner of provider connections (e.g., WhatsApp via Baileys, Telegram via grammY, Slack, Discord, Signal, iMessage, WebChat)\[2\]
- a typed WebSocket API server that validates inbound frames against JSON Schema and emits events like `agent`, `chat`, `presence`, `health`, `heartbeat`, and `cron`\[2\]
- the host for the Canvas and A2UI web hosts under `/__openclaw__/canvas/` and `/__openclaw__/a2ui/` (served by the Gateway HTTP server on the same port as the WS server)\[2\]

### Clients and nodes
OpenClaw’s control-plane clients (macOS app, CLI, web UI, automations) connect to the Gateway over WebSocket (default bind host `127.0.0.1:18789`).\[2\]

Nodes (macOS/iOS/Android/headless) also connect over WebSocket, but identify as `role: node` and declare capabilities/commands (e.g., `canvas.*`, `camera.*`, `screen.record`, `location.get`).\[2\]

### Session management
The docs describe direct-message session scoping via `session.dmScope` (default `main` for continuity), with options like `per-peer`, `per-channel-peer`, and `per-account-channel-peer` to isolate DM context in multi-user setups.\[5\]

### Tool system
OpenClaw exposes tools (e.g., file read/write, command execution, web/browser actions) to agents. The docs describe a layered allow/deny model to constrain what agents can do.\[2\]

### Sandbox
OpenClaw supports sandboxing modes that can constrain filesystem access and tool availability, particularly for non-main sessions or isolated runs.\[2\]

### Extension and plugin model
OpenClaw supports extensions/plugins (including additional channels) that can be registered and documented alongside built-in capabilities.\[2\]

## Configuration
OpenClaw’s documentation describes a JSON config (default path `~/.openclaw/openclaw.json`) and provides examples for restricting who can message the agent (e.g., allowlists, group mention requirements).\[2\]

The documentation also describes environment variables for customizing where OpenClaw reads config and stores state, including `OPENCLAW_CONFIG_PATH` and `OPENCLAW_STATE_DIR`.\[4\]

## Security and access control
OpenClaw’s documentation describes a pairing and trust model for WebSocket clients and nodes. New device identities require pairing approval; after approval, the Gateway issues a device token for subsequent connects.\[2\]

The documentation also describes an optional Gateway auth token (`OPENCLAW_GATEWAY_TOKEN`) that must be presented during the initial WebSocket handshake when enabled.\[2\]

For multi-user deployments, the documentation recommends isolating direct-message session context using `session.dmScope` (for example `per-channel-peer`) to reduce the risk of cross-user context leakage.\[5\]

## CLI
OpenClaw’s CLI includes an `openclaw agent` command to run an agent turn (via the Gateway, or locally with `--local`).\[3\]

## History
- **2026-02-26:** Steinberger published a post about joining OpenAI and moving OpenClaw to a foundation.\[1\]

## Related
- [Moltbook](./Moltbook.md)

## References
1. Peter Steinberger, “OpenClaw, OpenAI and the future” (Feb 2026). https://steipete.me/posts/2026/openclaw
2. OpenClaw Docs: “Gateway Architecture” (last updated 2026-01-22). https://docs.openclaw.ai/concepts/architecture
3. OpenClaw GitHub repository README (channels, highlights, and onboarding). https://github.com/openclaw/openclaw
4. OpenClaw Docs: `openclaw agent`. https://docs.openclaw.ai/cli/agent
5. OpenClaw Docs: “Session Management”. https://docs.openclaw.ai/concepts/session
6. OpenClaw Docs: “Getting Started” (quick setup and environment variables). https://docs.openclaw.ai/start/getting-started

## External links
- Project site: https://openclaw.ai/
- GitHub repo: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai
