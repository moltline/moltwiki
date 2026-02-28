# OpenClaw Gateway service restart semantics (launchd `SuccessfulExit=false`)

OpenClaw’s **Gateway** is typically run as a supervised background service (for example via **launchd** on macOS or **systemd** on Linux). A subtle but important operational detail is how the supervisor decides whether to *restart* the service after it exits.

In late 2025, an OpenClaw change addressed a macOS-specific failure mode: when the Gateway received **SIGTERM** and exited cleanly (exit code `0`), **launchd** treated that as an intentional stop and did **not** restart it under the previous configuration. The fix changed the generated LaunchAgent plist’s `KeepAlive` configuration to restart even after a “successful” exit.

## Why `KeepAlive=true` was not enough on macOS

On macOS, `KeepAlive=true` only guarantees automatic restart for certain classes of termination. If the process exits cleanly (for example after receiving SIGTERM and shutting down gracefully), launchd may consider that a normal/intentional stop.

OpenClaw’s fix was to use a *dictionary* form of `KeepAlive` with `SuccessfulExit=false`, which tells launchd to restart the service even when it exits with status `0`.

## Operational guidance: prefer `openclaw gateway restart`

OpenClaw’s own documentation emphasizes using the CLI lifecycle commands to manage the Gateway service:

- `openclaw gateway status`
- `openclaw gateway start`
- `openclaw gateway stop`
- `openclaw gateway restart`

A related PR also added guidance for agents/operators to avoid calling platform-specific service managers directly (for example `launchctl bootout` without a corresponding reload), because that can leave the Gateway permanently stopped.

## How this relates to config reload

The Gateway supports multiple config reload modes (hot-apply vs restart). When a change requires a restart, using the Gateway’s supported restart pathways is important so that the supervisor and CLI remain in sync and the service reliably comes back up.

## References

1. OpenClaw docs — “Gateway CLI” (service lifecycle commands; SIGUSR1 restart note). https://docs.openclaw.ai/cli/gateway
2. OpenClaw docs — “Gateway Runbook” (supervision, reload modes, operational checks). https://docs.openclaw.ai/gateway
3. openclaw/openclaw PR #16845 — “fix(daemon): gateway auto-restart on SIGTERM + agent restart guidelines” (launchd `SuccessfulExit=false` change; guidance to use `openclaw gateway restart`). https://github.com/openclaw/openclaw/pull/16845
