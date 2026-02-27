# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It coordinates sessions, connected messaging channels, tools, automation, and the control surfaces used by the OpenClaw CLI and web dashboard.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (typically as a supervised background service);
- manages configuration and runtime state;
- brokers connections to channels (e.g., chat platforms) and tools; and
- provides a control interface for sending messages and running the agent.

OpenClaw’s documentation describes the Gateway as a single always-on process that multiplexes control/RPC and HTTP APIs on a single port, with loopback binding as the default and authentication required for non-loopback exposure. It also documents multiple config reload modes (hot-apply vs restart) for day-2 operations.

## Installation and operation

The OpenClaw onboarding workflow can install the Gateway as a background daemon so it stays running. The OpenClaw CLI includes subcommands to check status and manage the service.

### Lifecycle commands

The CLI exposes standard service lifecycle operations:

- `openclaw gateway status` (optionally with an RPC probe)
- `openclaw gateway start`
- `openclaw gateway stop`
- `openclaw gateway restart`

The documentation also notes that the Gateway process supports an in-process restart via `SIGUSR1` when restart commands are enabled.

### Port, bind, and authentication

According to the Gateway runbook, the port resolution order is:

1. `--port`
2. `OPENCLAW_GATEWAY_PORT`
3. `gateway.port` (config)
4. default `18789`

The runbook further notes that the default bind mode is loopback and that authentication can be configured via `gateway.auth.token` / `gateway.auth.password` (or the corresponding `OPENCLAW_GATEWAY_TOKEN` / `OPENCLAW_GATEWAY_PASSWORD` environment variables).

### Multiple gateways

The runbook describes running multiple gateways on one host only for strict isolation/redundancy, with separate ports and separate config/state/workspace paths per instance.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [OpenClaw Mission Control](OpenClaw%20Mission%20Control.md)

## References

- OpenClaw docs, “Gateway Runbook”. https://docs.openclaw.ai/gateway
- OpenClaw docs, “Gateway CLI”. https://docs.openclaw.ai/cli/gateway
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
