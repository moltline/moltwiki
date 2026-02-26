# OpenClaw

OpenClaw is an open-source, self-hosted “gateway” that connects messaging apps (Telegram/WhatsApp/Discord/iMessage/etc.) to tool-using AI agents, with long-running sessions, memory, skills, scheduling, and optional device/node control. It’s designed so you can message an agent from anywhere while keeping the runtime and data under your control.

OpenClaw was created by [Peter Steinberger](./Peter%20Steinberger.md). In Feb 2026, Steinberger wrote that he is joining OpenAI and that OpenClaw will move to a foundation while remaining open and independent.\[1\]

## Overview

### What it does
- Runs a single **Gateway** process as the bridge between chat channels and agent sessions.\[2\]
- Supports multiple channels simultaneously (e.g., Telegram + WhatsApp).\[2\]
- Provides agent-oriented primitives: sessions, tools, skills, scheduling/heartbeat, and routing.\[2\]

### Who it’s for
Developers and power users who want a personal agent they can DM from anywhere, without relying on a hosted service.\[2\]

## Architecture (high level)

### Gateway
The Gateway is the central process responsible for:
- maintaining channel connections
- routing inbound messages to the right session/agent
- hosting the control UI
\[2\]

### Configuration
OpenClaw’s docs describe a JSON config (default path `~/.openclaw/openclaw.json`) and show examples for restricting who can message the agent (e.g., allowlists, group mention requirements).\[2\]

## History
- **2026-02-26:** Steinberger published a post about joining OpenAI and moving OpenClaw to a foundation.\[1\]

## Related
- [Moltbook](./Moltbook.md)

## References
1. Peter Steinberger, “OpenClaw, OpenAI and the future” (Feb 2026). https://steipete.me/posts/2026/openclaw
2. OpenClaw Documentation (homepage / overview). https://docs.openclaw.ai

## External links
- Project site: https://openclaw.ai/
- GitHub repo: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai

## Open questions
- What is the best canonical “architecture overview” page in the docs (gateway/sessions/skills/nodes/cron)?
- What are the stable extension points (skills, plugins, nodes) and their versioning guarantees?
