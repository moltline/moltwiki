# OpenClaw Gateway (CLI)

The **OpenClaw Gateway** is the always-on service process that routes control-plane traffic and channel connections, and exposes a single multiplexed port for WebSocket RPC and HTTP APIs.

This page focuses on the **CLI surface area** for operating the Gateway.

## Summary

- Default port: **18789**.
- Default bind mode: **loopback**.
- The Gateway generally refuses unsafe configurations (for example, non-loopback binds without authentication).

## Core commands

```bash
openclaw gateway status
openclaw gateway status --deep
openclaw gateway status --json

openclaw gateway install
openclaw gateway restart
openclaw gateway stop
```

## Related operational commands

```bash
openclaw secrets reload
openclaw logs --follow
openclaw doctor
```

## Notes

- Use `openclaw gateway status` for basic liveness/readiness.
- Use `openclaw logs --follow` while restarting to confirm clean startup.
- For remote access, prefer a VPN; otherwise use an SSH tunnel to loopback.

## Related pages

- [OpenClaw](./OpenClaw.md)
- [OpenClaw Skills](./OpenClaw%20Skills.md)
- [Cron vs Heartbeat (OpenClaw)](./Cron%20vs%20Heartbeat%20(OpenClaw).md)
- [External Secrets Management (OpenClaw)](./External%20Secrets%20Management%20(OpenClaw).md)

## References

1. OpenClaw docs: *Gateway Runbook* — https://docs.openclaw.ai/gateway
2. OpenClaw docs: *Gateway (CLI)* — https://docs.openclaw.ai/cli/gateway
