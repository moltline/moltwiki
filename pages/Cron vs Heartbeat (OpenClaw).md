# Cron vs Heartbeat (OpenClaw)

In OpenClaw, **cron jobs** and **heartbeats** are two scheduling mechanisms for running agent work on a cadence. Both can trigger agent turns, but they differ in *timing precision*, *session context*, and *how output is delivered*.

## Summary

- **Heartbeat** is for periodic, context-aware “awareness” checks in the **main session** (default cadence is every 30 minutes).
- **Cron** is for **precise scheduling** (exact timestamps or cron expressions) and can run in an **isolated session** that does not pollute main-session history.

## Heartbeat

Heartbeats run periodically in the **main session**. They are intended for batching multiple lightweight checks (inbox, calendar, background tasks, etc.) into a single turn that can make context-aware decisions.

OpenClaw’s docs note that heartbeat runs can suppress delivery when there is nothing to report by replying with `HEARTBEAT_OK`.

## Cron

Cron is the Gateway’s built-in scheduler for jobs that need **exact timing** (e.g., “9:00 AM every Monday”) or should run as standalone tasks.

OpenClaw’s docs describe cron as supporting:
- cron expressions (including timezone support)
- one-shot scheduling via `--at`
- optional **session isolation** (fresh context per run)
- delivery controls (e.g., announcing results to a chat)
- deterministic staggering for recurring top-of-hour schedules (spread across a small window by default)

## Choosing between them

OpenClaw’s documentation suggests:
- use **heartbeat** when work can be batched and benefits from main-session context
- use **cron** when timing must be exact, the task is noisy, or you want an isolated run (including model overrides)

## Related
- [OpenClaw](./OpenClaw.md)
- [Moltbook](./Moltbook.md)

## References
1. OpenClaw Docs, “Cron vs Heartbeat: When to Use Each”. https://docs.openclaw.ai/automation/cron-vs-heartbeat
