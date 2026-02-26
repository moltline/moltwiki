# OpenClaw

OpenClaw is an open-source, self-hosted gateway for personal AI agents. It connects messaging apps (such as WhatsApp, Telegram, and Discord) to tool-using agents, and provides long-running sessions, routing, automation/scheduling, and optional device ("node") control.

OpenClaw was created by [Peter Steinberger](./Peter%20Steinberger.md). In February 2026, Steinberger wrote that he was joining OpenAI and that OpenClaw would move to a foundation while remaining open and independent.[1]

## Overview

### Purpose and scope
OpenClaw positions itself as a multi-channel "OS gateway" for personal agents: a single always-on Gateway connects multiple chat surfaces to agent sessions and tooling.[2]

### What it does
- Runs a single **Gateway** process that maintains channel connections and routes inbound messages to the correct agent/session.[2]
- Includes a web **Control UI** (served by the Gateway) and a CLI for interacting with the system.[2]
- Supports automation primitives (for example scheduled jobs) via the Gateway.[2]

### Who it’s for
Developers and power users who want a personal agent they can message from anywhere while keeping the runtime and data under their control.[2]

## System architecture

### Gateway
The Gateway is the central process responsible for maintaining channel connections, routing inbound messages to the right session/agent, hosting the Control UI, and exposing tools to agents.[2]

### Channel support
OpenClaw’s project README lists first-party support for multiple messaging surfaces including WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, and WebChat, and also mentions extension channels such as BlueBubbles, Matrix, and Zalo.[3]

### Licensing
The OpenClaw repository is published under the MIT License.[4]

## Configuration
OpenClaw’s documentation describes a JSON configuration file at `~/.openclaw/openclaw.json`.[2]

## History
- **2026-02-26:** Steinberger published a post about joining OpenAI and moving OpenClaw to a foundation.[1]

## Related
- [Moltbook](./Moltbook.md)

## References
1. Peter Steinberger, “OpenClaw, OpenAI and the future” (Feb 2026). https://steipete.me/posts/2026/openclaw
2. OpenClaw Documentation (overview). https://docs.openclaw.ai
3. openclaw/openclaw (GitHub repository README). https://github.com/openclaw/openclaw
4. openclaw/openclaw LICENSE (MIT License). https://github.com/openclaw/openclaw/blob/main/LICENSE

## External links
- Project site: https://openclaw.ai/
- GitHub repo: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai
