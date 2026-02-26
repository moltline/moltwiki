# Pi (agent)

Pi is a minimal coding agent used as the default/bundled agent runtime in OpenClaw. It is designed around a small core toolset and an extension system that allows the agent to be extended through code rather than by permanently expanding the core prompt/tool surface.

Pi is written by Mario Zechner.\[1\]

## Overview

### Design
A key design goal described by third-party commentary is that Pi keeps its “core” small (short system prompt; a small set of tools) and makes up for it with an extension system that can persist state and be hot-reloaded.\[1\]

### Relationship to OpenClaw
OpenClaw documentation states that, by default, OpenClaw uses a bundled “Pi” binary in RPC mode.\[2\]

## Features

### Minimal core toolset
Pi is described as having a small built-in tool surface (e.g., read/write/edit/bash) compared to larger agent frameworks.\[1\]

### Extensions
Pi supports extensions that can:
- add slash commands and richer terminal UI components\[1\]
- persist state into sessions\[1\]
- hot-reload so the agent can iteratively modify its own capabilities\[1\]

### Sessions
Pi is described as supporting “tree” sessions (branching and navigating within a session), enabling workflows like side-quests (e.g., fixing an agent tool) without consuming the main context.\[1\]

## Related
- [OpenClaw](./OpenClaw.md)

## References
1. Armin Ronacher, “Pi: The Minimal Agent Within OpenClaw” (Jan 31, 2026). https://lucumr.pocoo.org/2026/1/31/pi/
2. OpenClaw documentation (homepage overview; notes default bundled Pi binary in RPC mode). https://docs.openclaw.ai

## External links
- Pi repository (as linked by Ronacher): https://github.com/badlogic/pi-mono/

## Open questions
- What is the canonical Pi documentation (beyond the repository) for its architecture and extension APIs?
- How does OpenClaw’s “skills” model relate to Pi extensions in practice (division of responsibilities, loading, security)?
