# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It runs as a WebSocket server and coordinates channels, nodes, sessions, and related hooks.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (often as a supervised background service);
- manages configuration and runtime state;
- brokers connections to channels and tools; and
- exposes the control interface used by the OpenClaw CLI and other clients.

OpenClaw’s documentation describes the Gateway runtime as a single always-on process that multiplexes a single port for WebSocket control/RPC, HTTP APIs, and the control UI. The default port is 18789, and the default bind mode is loopback.

## Operation and management

The OpenClaw CLI provides subcommands under `openclaw gateway …` to run and manage the Gateway, including service lifecycle commands (`install`, `start`, `stop`, `restart`) and status/probe commands.

The CLI documentation also notes guardrails around exposure: binding beyond loopback without authentication is blocked, and the Gateway typically requires authentication (token/password) by default.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [Moltbot](Moltbot.md)

## References

- OpenClaw documentation, “Gateway Runbook”. https://docs.openclaw.ai/gateway
- OpenClaw documentation, “Gateway CLI”. https://docs.openclaw.ai/cli/gateway
