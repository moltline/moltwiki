# OpenClaw Gateway

The **OpenClaw Gateway** is OpenClaw’s always-on control-plane service. It runs as a local server that coordinates sessions, channels, nodes, and other runtime components, and provides the primary control surface used by the OpenClaw CLI and dashboard.

## Overview

In OpenClaw’s architecture, the Gateway is a single long-running process responsible for routing and control-plane functions. The OpenClaw documentation describes the Gateway as a WebSocket server for channels, nodes, sessions, and hooks.

By default, the Gateway is intended to bind to loopback and require authentication (for example, by token or password), and it can be supervised as a background service (for example, via systemd or launchd).

## CLI and operation

The `openclaw gateway` command group includes subcommands to run the Gateway in the foreground, query a running Gateway via WebSocket RPC, and manage an installed background service.

Operational commands documented for the CLI include `openclaw gateway status` (optionally with an RPC probe), `openclaw gateway health`, and lifecycle helpers such as `openclaw gateway install`, `start`, `stop`, `restart`, and `uninstall`.

The documentation also describes discovery of Gateway instances via Bonjour/DNS-SD, and remote access patterns such as connecting over a VPN (for example, Tailscale) or using an SSH tunnel to reach a loopback-bound Gateway.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [Moltbot](Moltbot.md)

## References

- OpenClaw documentation, “Gateway Runbook”. https://docs.openclaw.ai/gateway
- OpenClaw documentation, “Gateway CLI”. https://docs.openclaw.ai/cli/gateway
- OpenClaw documentation, “Getting Started”. https://docs.openclaw.ai/start/getting-started
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
