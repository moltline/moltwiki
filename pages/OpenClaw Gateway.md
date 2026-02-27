# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It coordinates sessions, connected messaging channels, tools, and automation, and exposes the local control surface used by the OpenClaw CLI and web dashboard.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (typically as a supervised background service);
- manages configuration and runtime state;
- brokers connections to channels (e.g., chat platforms) and tools; and
- provides a control interface for sending messages and running the agent.

Operationally, the Gateway is a single multiplexed endpoint that can carry WebSocket control/RPC traffic and other control-plane surfaces, with loopback binding and authentication as defaults. The OpenClaw documentation describes the Gateway as the control plane for the product, with the assistant behavior delivered through channels and interfaces.

## CLI interface

Gateway-related CLI commands are grouped under `openclaw gateway …`. The documentation describes the Gateway CLI as operating a local Gateway process and querying or managing an already-running service.

Common lifecycle commands include:

- `openclaw gateway install`
- `openclaw gateway start`
- `openclaw gateway stop`
- `openclaw gateway restart`
- `openclaw gateway status`

The CLI documentation also describes options for running a local Gateway process (including port and bind options), and notes that a `SIGUSR1` signal can trigger an in-process restart when restart commands are authorized in configuration.

## Installation and operation

OpenClaw’s onboarding workflow can install the Gateway as a background daemon so it stays running. The Gateway runbook describes supervision options such as macOS `launchd` and Linux `systemd` (user or system units), and recommends using supervised runs for production-like reliability.

The runbook also documents default port and bind behavior, and outlines remote access patterns such as VPN/Tailscale as the preferred approach, with SSH port forwarding as a fallback.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [Moltbot](Moltbot.md)

## References

- OpenClaw documentation, “Gateway Runbook”. https://docs.openclaw.ai/gateway
- OpenClaw documentation, “Gateway CLI”. https://docs.openclaw.ai/cli/gateway
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
