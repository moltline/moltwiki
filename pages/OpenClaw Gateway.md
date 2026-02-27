# OpenClaw Gateway

The **OpenClaw Gateway** is OpenClaw’s always-on control-plane service. It runs as a WebSocket server that coordinates channels, nodes, sessions, and hooks, and provides the RPC surface used by the OpenClaw CLI and Control UI.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (often under launchd or systemd);
- manages configuration and runtime state;
- brokers connections to channels (e.g., Telegram/WhatsApp/Slack/Discord) and tools (e.g., browser, nodes); and
- exposes a WebSocket RPC interface for health checks, status, and agent runs.

The OpenClaw docs describe the Gateway as the product’s control plane.

## Running the Gateway

You can run the Gateway in the foreground with:

- `openclaw gateway` (alias: `openclaw gateway run`)

The CLI docs note that the Gateway may refuse to start unless `gateway.mode=local` is set in the config, and that `--allow-unconfigured` can be used for ad-hoc/dev runs.

## Service lifecycle and operator commands

OpenClaw supports installing the Gateway as a supervised background service and managing it via the CLI:

- `openclaw gateway install`
- `openclaw gateway status` (optionally probes the RPC endpoint)
- `openclaw gateway start | stop | restart | uninstall`

The Gateway runbook also documents typical “day-2” operations such as `openclaw secrets reload`, `openclaw logs --follow`, and `openclaw doctor`.

## Ports, bind, and auth (high level)

The Gateway typically binds to loopback by default and expects authentication (token or password). The runbook documents port/bind precedence and notes that binding beyond loopback without auth is blocked as a safety guardrail.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Gateway](OpenClaw%20Gateway.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [OpenClaw Gateway runbook](https://docs.openclaw.ai/gateway)

## References

- OpenClaw Docs — “Gateway CLI”. https://docs.openclaw.ai/cli/gateway
- OpenClaw Docs — “Gateway Runbook”. https://docs.openclaw.ai/gateway
- OpenClaw Docs — “Updating” (restart and service notes). https://docs.openclaw.ai/install/updating
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
