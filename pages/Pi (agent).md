# Pi (agent)

Pi is a minimal coding agent used as the default/bundled agent runtime in OpenClaw. It is designed around a small core toolset and an extension system intended to keep the core prompt and tool surface small while enabling additional capabilities through code.\[1\]

Pi is written by Mario Zechner.\[1\]

## Overview

### Design
A design goal described in third-party commentary is that Pi has a tiny core—short system prompt and four built-in tools (Read, Write, Edit, Bash)—and relies on an extension system for additional functionality.\[1\]

### Relationship to OpenClaw
OpenClaw documentation states that, by default, OpenClaw uses a bundled Pi binary in RPC mode with per-sender sessions.\[2\]

## Features

### Minimal core toolset
Pi is described as shipping with four core tools: Read, Write, Edit, and Bash.\[1\]

### Extensions and terminal UI
Pi’s extension system is described as supporting custom capabilities such as slash commands and terminal UI components (for example, spinners, progress bars, and interactive pickers), as well as the ability for extensions to register tools callable by the model.\[1\]

### Session persistence and hot reloading
According to third-party commentary, Pi sessions can store custom (non-model) messages for extension state, and Pi supports hot reloading so an agent can iteratively write code, reload, and test extensions.\[1\]

### Tree-structured sessions
Pi is described as storing sessions as trees that can be branched and navigated, enabling side-quest workflows (for example, fixing a tool on a branch and returning to an earlier point).\[1\]

## Related
- [OpenClaw](./OpenClaw.md)

## References
1. Armin Ronacher, “Pi: The Minimal Agent Within OpenClaw” (January 31, 2026). https://lucumr.pocoo.org/2026/1/31/pi/
2. OpenClaw documentation, “OpenClaw” (homepage; accessed 2026-02-27). https://docs.openclaw.ai

## External links
- Pi repository: https://github.com/badlogic/pi-mono/
