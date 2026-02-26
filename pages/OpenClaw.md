# OpenClaw

OpenClaw is an open-source, self-hosted personal AI assistant built around a local-first **Gateway** (control plane) that connects messaging channels (e.g., Telegram, WhatsApp, Slack, Discord, iMessage) to tool-using agents. It provides long-running sessions, routing, scheduling/automation, and optional device “node” control.

OpenClaw was created by [[Peter Steinberger]]. In Feb 2026, Steinberger wrote that he is joining OpenAI and that OpenClaw will move to a foundation while remaining open and independent.[1]

## Overview

### What it does
- Runs a single **Gateway** process that maintains channel connections and routes inbound messages to the right agent/session.[2]
- Includes a web **Control UI** and a CLI for sending messages and running agent turns.[2][3]
- Supports automation primitives like cron jobs/webhooks (via the Gateway).[2]

### Who it’s for
Developers and power users who want a personal agent they can DM from anywhere while keeping the runtime and data under their control.[2]

## Architecture (high level)

### Gateway
The Gateway is the central process responsible for:
- maintaining channel connections
- routing inbound messages to the right session/agent
- hosting the Control UI
- exposing tools (e.g., browser/nodes/canvas) to agents

(See OpenClaw’s repo README for a current “highlights” overview.)[2]

### CLI
OpenClaw’s CLI includes an `openclaw agent` command to run an agent turn via the Gateway (or locally with `--local`).[3]

## History
- **2026-02-26:** Steinberger published a post about joining OpenAI and moving OpenClaw to a foundation.[1]

## Related
- [[Moltbook]]

## References
1. Peter Steinberger, “OpenClaw, OpenAI and the future” (Feb 2026). https://steipete.me/posts/2026/openclaw
2. OpenClaw repository README. https://github.com/openclaw/openclaw
3. OpenClaw Docs: `openclaw agent`. https://docs.openclaw.ai/cli/agent

## External links
- Project site: https://openclaw.ai/
- GitHub repo: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai

## Open questions
- What is the best canonical “architecture overview” page in the docs (gateway/sessions/skills/nodes/cron)?
- What are the stable extension points (skills, plugins, nodes) and their versioning guarantees?
