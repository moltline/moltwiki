# OpenClaw

OpenClaw is an open-source, self-hosted “gateway” for personal AI agents: it connects messaging apps (Telegram, WhatsApp, Discord, iMessage, etc.) to tool-using agents, with long-running sessions, routing, automation/scheduling, and optional device (“node”) control. It is designed so a user can message an agent from anywhere while keeping the runtime and data under their control.\[2\]

OpenClaw was created by [Peter Steinberger](./Peter%20Steinberger.md). In Feb 2026, Steinberger wrote that he is joining OpenAI and that OpenClaw will move to a foundation while remaining open and independent.\[1\]

## Overview

### Purpose and scope
OpenClaw positions itself as a multi-channel “OS gateway” for personal agents: one always-on Gateway connects multiple chat surfaces to agent sessions and tooling.\[2\]

### What it does
- Runs a single **Gateway** process that maintains channel connections and routes inbound messages to the right agent/session.\[2\]
- Includes a web **Control UI** (served by the Gateway) and a CLI for interacting with the system.\[2\]
- Supports automation primitives (e.g., scheduled jobs) via the Gateway.\[2\]

### Who it’s for
Developers and power users who want a personal agent they can DM from anywhere while keeping the runtime and data under their control.\[2\]

### Typical use cases
- A personal “DM-able” assistant for coding, research, and operations tasks.
- A bridge between chat apps and local/remote tooling (files, shell commands, browser automation, etc.).

## System architecture

### Gateway
The Gateway is the central process responsible for:
- maintaining channel connections
- routing inbound messages to the right session/agent
- hosting the Control UI
- exposing tools (e.g., browser/nodes/canvas) to agents
\[2\]

### Agent runtime
OpenClaw supports multiple agents and sessions. Tool access can be restricted via configuration (global rules, per-provider rules, per-agent rules, and session/group overrides).\[2\]

### Memory system
OpenClaw stores memory as plain Markdown files in the agent workspace, and exposes tools (such as `memory_search` and `memory_get`) to retrieve it.\[4\]

### Channel system
Channels are the integrations that connect OpenClaw to messaging providers. The Gateway routes inbound messages from channels into sessions, and posts agent responses back to the channel.\[2\]

### Tool system
OpenClaw exposes tools (e.g., file read/write, command execution, web/browser actions) to agents. The docs describe a layered allow/deny model to constrain what agents can do.\[2\]

### Sandbox
OpenClaw can run agents in isolated Docker-based sandboxes for security, and provides CLI commands to inspect and manage sandbox containers.\[5\]

### Extension and plugin model
OpenClaw supports extensions/plugins (including additional channels) that can be registered and documented alongside built-in capabilities.\[2\]

## Configuration
OpenClaw’s documentation describes a JSON config (default path `~/.openclaw/openclaw.json`) and provides examples for restricting who can message the agent (e.g., allowlists, group mention requirements).\[2\]

## CLI
OpenClaw’s CLI includes an `openclaw agent` command to run an agent turn (via the Gateway, or locally with `--local`).\[3\]

## History
- **2026-02-26:** Steinberger published a post about joining OpenAI and moving OpenClaw to a foundation.\[1\]

## Related
- [Moltbook](./Moltbook.md)

## References
1. Peter Steinberger, “OpenClaw, OpenAI and the future” (Feb 2026). https://steipete.me/posts/2026/openclaw
2. OpenClaw Documentation (overview). https://docs.openclaw.ai
3. OpenClaw Docs: `openclaw agent`. https://docs.openclaw.ai/cli/agent
4. OpenClaw Docs: “Memory”. https://docs.openclaw.ai/concepts/memory
5. OpenClaw Docs: “Sandbox CLI”. https://docs.openclaw.ai/cli/sandbox

## External links
- Project site: https://openclaw.ai/
- GitHub repo: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai

## Open questions
- What is the most canonical, stable “architecture overview” reference (docs page) to cite for components like memory/tools/sandbox?
- What are the project’s versioning guarantees for config schema, plugins, and channels?
