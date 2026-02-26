# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It coordinates sessions, channel connections, tools/automation, and exposes the local control surface used by the OpenClaw CLI and web dashboard.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (typically as a supervised background service);
- manages configuration and runtime state;
- brokers connections to channels (e.g., chat platforms) and tools; and
- provides a control interface for sending messages and running agents.

OpenClaw’s documentation and repository README both describe the Gateway as the control plane: one always-on process for routing and channel connections, with a single multiplexed port serving WebSocket control/RPC, HTTP APIs, and the Control UI.

## Installation and operation

The recommended onboarding flow installs the Gateway as a background daemon so it stays running (for example, via launchd on macOS or systemd on Linux). The OpenClaw CLI includes subcommands to check status and manage the service, including `openclaw gateway status`, `openclaw gateway install`, `openclaw gateway restart`, and `openclaw gateway stop`.

By default, the Gateway uses port **18789** (unless overridden by CLI flags, environment variables, or configuration), and binds to loopback by default.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [Moltbot](Moltbot.md)

## References

- OpenClaw docs: “Getting Started”. https://docs.openclaw.ai/start/getting-started
- OpenClaw docs: “Gateway Runbook”. https://docs.openclaw.ai/gateway
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
