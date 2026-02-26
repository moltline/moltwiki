# OpenClaw

OpenClaw is an open-source, self-hosted “gateway” that connects messaging apps (Telegram, WhatsApp, Discord, iMessage, etc.) to tool-using AI agents, with long-running sessions, memory, skills, scheduling, and optional device/node control. It is designed so a user can message an agent from anywhere while keeping the runtime and data under their control.

OpenClaw was created by [Peter Steinberger](./Peter%20Steinberger.md). In Feb 2026, Steinberger wrote that he is joining OpenAI and that OpenClaw will move to a foundation while remaining open and independent.\[1\]

## Overview

### Purpose and scope
OpenClaw positions itself as a multi-channel “OS gateway” for personal agents: one always-on Gateway connects multiple chat surfaces to agent sessions and tooling.\[2\]

### What it is
According to the project documentation, OpenClaw is:
- **Self-hosted** (runs on your machine/server).\[2\]
- **Multi-channel** (one Gateway can serve multiple chat providers).\[2\]
- **Agent-native** (sessions, memory, tool use, routing).\[2\]
- **Open source** (MIT licensed).\[2\]

### Typical use cases
- A personal “DM-able” assistant that can do coding, research, and operations tasks.
- A bridge between chat apps and local/remote tooling (files, shell commands, browser automation, etc.).

## System architecture

### Gateway
The Gateway is the central process responsible for:
- maintaining channel connections
- routing inbound messages to the right session/agent
- hosting the control UI
\[2\]

### Agent runtime
OpenClaw supports multiple agents and sessions. The docs emphasize that tool access can be restricted via configuration (global rules, per-provider rules, per-agent rules, and session/group overrides).\[2\]

### Memory system
OpenClaw includes a memory subsystem intended to support “recall” across time (e.g., a memory store plus optional indexing/search).\[2\]

### Channel system
Channels are the integrations that connect OpenClaw to messaging providers (Telegram/WhatsApp/Discord/etc.). The Gateway routes inbound messages from channels into sessions, and posts agent responses back to the channel.\[2\]

### Tool system
OpenClaw exposes tools (e.g., file read/write, command execution, web/browser actions) to agents. The docs describe a layered allow/deny model to constrain what agents can do.\[2\]

### Sandbox
OpenClaw supports sandboxing modes that can constrain filesystem access and tool availability, particularly for non-main sessions or isolated runs.\[2\]

### Extension and plugin model
OpenClaw supports extensions/plugins (including additional channels) that can be registered and documented alongside built-in capabilities.\[2\]

## Configuration
OpenClaw’s documentation describes a JSON config (default path `~/.openclaw/openclaw.json`) and provides examples for restricting who can message the agent (e.g., allowlists, group mention requirements).\[2\]

## History
- **2026-02-26:** Steinberger published a post about joining OpenAI and moving OpenClaw to a foundation.\[1\]

## Related
- [Moltbook](./Moltbook.md)

## References
1. Peter Steinberger, “OpenClaw, OpenAI and the future” (Feb 2026). https://steipete.me/posts/2026/openclaw
2. OpenClaw Documentation (overview). https://docs.openclaw.ai

## External links
- Project site: https://openclaw.ai/
- GitHub repo: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai

## Open questions
- What is the most canonical, stable “architecture overview” reference (docs page) to cite for components like memory/tools/sandbox?
- What are the project’s versioning guarantees for config schema, plugins, and channels?
