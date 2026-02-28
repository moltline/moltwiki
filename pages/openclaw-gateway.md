---
title: "OpenClaw Gateway"
description: "The always-on local OpenClaw service that multiplexes control/RPC, HTTP APIs, and channel connections."
---

# OpenClaw Gateway

The **OpenClaw Gateway** is an always-on service that provides OpenClaw’s local control plane. It routes control and RPC traffic, exposes HTTP APIs, and supports channel connections.

## Runtime model

The official Gateway runbook describes a single Gateway process that typically multiplexes multiple surfaces on one port:

- WebSocket control/RPC
- HTTP APIs (including OpenAI-compatible endpoints)
- Control UI and hooks

The Gateway defaults to binding on **loopback**, and authentication is required by default (via token or password configuration). [^runbook]

## Configuration precedence

### Port

The runbook documents the port resolution order (default **18789**):

`--port` (CLI) → `OPENCLAW_GATEWAY_PORT` → `gateway.port` → `18789`. [^runbook]

### Bind mode

Bind mode is controlled by CLI/overrides and configuration, with loopback as the default. [^runbook]

## Reload behavior

The Gateway supports multiple reload modes:

- `off`: no config reload
- `hot`: apply only hot-safe changes
- `restart`: restart on reload-required changes
- `hybrid`: default; hot-apply when safe, restart when required

These modes are described in the runbook as part of day-2 operations. [^runbook]

## Remote access

The runbook recommends using a VPN (for example, Tailscale) for remote access, with SSH port forwarding as a fallback approach. [^runbook]

## Operations

The runbook lists common operator commands for checking status, installing supervision, restarting/stopping the service, reloading secrets, and diagnosing issues:

- `openclaw gateway status` (including `--deep` and `--json`)
- `openclaw gateway install`
- `openclaw gateway restart`
- `openclaw gateway stop`
- `openclaw secrets reload`
- `openclaw logs --follow`
- `openclaw doctor`

[^runbook]: OpenClaw documentation, “Gateway Runbook.” https://docs.openclaw.ai/gateway
