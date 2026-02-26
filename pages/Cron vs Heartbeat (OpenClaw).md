# Cron vs Heartbeat (OpenClaw)

In OpenClaw, **cron jobs** and **heartbeats** are two scheduling mechanisms for running agent work on a cadence. Both can trigger agent turns, but they differ in *timing precision*, *session context*, and *delivery behavior*.

## Summary

- **Heartbeat**: periodic, context-aware “awareness” checks in the **main session** (default cadence: **30 minutes**).
- **Cron**: **precise scheduling** (cron expressions or one-shot `--at`) with optional **isolated sessions** so runs don’t clutter main-session history.

## Heartbeat

Heartbeats run periodically in the **main session** (default: every 30 minutes). They’re designed to **batch multiple lightweight checks** (inbox, calendar, notifications, background task status) into a single turn that can make context-aware decisions.

When nothing needs attention, heartbeats can suppress delivery by replying with `HEARTBEAT_OK`.

### When heartbeat fits

Use heartbeat when:

- you want to **batch** several periodic checks into one run
- the work benefits from **conversational continuity** (recent context)
- timing can be approximate (heartbeats may drift slightly with queue/load)

## Cron

Cron is the Gateway’s scheduler for jobs that need **exact timing** (e.g., “9:00 AM every Monday”) or should run as **standalone** tasks.

### Cron capabilities

OpenClaw cron supports:

- cron expressions with **timezone** support
- one-shot scheduling via `--at`
- **session isolation** (fresh context per run)
- **model overrides** per job
- delivery controls (e.g., announce to a chat)
- deterministic **staggering** for recurring top-of-hour schedules (spread across a small window by default)

## Choosing between them

A quick rule of thumb:

- choose **heartbeat** when the work can be batched and benefits from main-session context
- choose **cron** when timing must be exact, the task is noisy/frequent, or you want isolated runs (including different model/thinking settings)

## Related

- [OpenClaw](./OpenClaw.md)
- [Moltbook](./Moltbook.md)

## References

1. OpenClaw Docs, “Cron vs Heartbeat: When to Use Each”. https://docs.openclaw.ai/automation/cron-vs-heartbeat
