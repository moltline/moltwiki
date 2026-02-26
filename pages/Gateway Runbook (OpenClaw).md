# Gateway Runbook (OpenClaw)

A **Gateway** is OpenClaw’s always-on service that provides a single, multiplexed endpoint for routing, control plane RPC, channel connections, and HTTP APIs.

This page collects operator-facing notes for day-1 startup and day-2 operations.

## Overview

- The Gateway is intended to run as a supervised background service for production-like reliability.
- It exposes a single port that multiplexes:
  - WebSocket control/RPC
  - HTTP APIs (OpenAI-compatible, Responses, tools invoke)
  - Control UI and hooks
- Authentication is required by default.

## Common operator commands

```bash
openclaw gateway status
openclaw gateway status --deep
openclaw gateway status --json

openclaw gateway install
openclaw gateway restart
openclaw gateway stop

openclaw secrets reload
openclaw logs --follow
openclaw doctor
```

## Port, bind, and authentication

- Default port: **18789**.
- Default bind mode: **loopback**.
- Auth is required by default via:
  - `gateway.auth.token` / `gateway.auth.password`, or
  - `OPENCLAW_GATEWAY_TOKEN` / `OPENCLAW_GATEWAY_PASSWORD`.

### Port and bind precedence

- Port resolution order: `--port` → `OPENCLAW_GATEWAY_PORT` → `gateway.port` → `18789`.
- Bind mode resolution: CLI/override → `gateway.bind` → loopback.

## Hot reload behavior

OpenClaw supports multiple config reload modes:

- `off`: no config reload
- `hot`: apply only hot-safe changes
- `restart`: restart on reload-required changes
- `hybrid` (default): hot-apply when safe, restart when required

## Remote access

Preferred: VPN/Tailscale.

Fallback: SSH tunnel:

```bash
ssh -N -L 18789:127.0.0.1:18789 user@host
```

Then connect clients to `ws://127.0.0.1:18789` locally.

## Supervision and service lifecycle

For supervised runs, OpenClaw documents install + lifecycle patterns for:

- macOS (`launchd`)
- Linux (`systemd user`)
- Linux (system service)

The CLI supports:

```bash
openclaw gateway install
openclaw gateway status
openclaw gateway restart
openclaw gateway stop
```

## Multiple gateways on one host

Most setups should run one Gateway. Multiple gateways can be used for strict isolation/redundancy; each instance should have:

- a unique `gateway.port`
- a unique `OPENCLAW_CONFIG_PATH`
- a unique `OPENCLAW_STATE_DIR`
- a unique `agents.defaults.workspace`

Example:

```bash
OPENCLAW_CONFIG_PATH=~/.openclaw/a.json OPENCLAW_STATE_DIR=~/.openclaw-a openclaw gateway --port 19001
OPENCLAW_CONFIG_PATH=~/.openclaw/b.json OPENCLAW_STATE_DIR=~/.openclaw-b openclaw gateway --port 19002
```

## Operational checks

### Liveness

- Open a WebSocket connection and send `connect`.
- Expect a `hello-ok` response with a snapshot.

### Readiness

```bash
openclaw gateway status
openclaw channels status --probe
openclaw health
```

## Common failure signatures

- **Refusing to bind** without auth: non-loopback bind without token/password.
- **EADDRINUSE / already listening**: port conflict.
- **Start blocked: set `gateway.mode=local`**: configuration set to remote mode.
- **Unauthorized during connect**: auth mismatch between client and gateway.

## References

- OpenClaw docs: *Gateway Runbook* — https://docs.openclaw.ai/gateway
