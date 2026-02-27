# Cron vs Heartbeat (OpenClaw)

In OpenClaw, **cron jobs** and **heartbeats** are two scheduling mechanisms for running agent work on a cadence. Both can trigger agent work, but they differ in *timing precision*, *session context*, and *how output is delivered*.

## Summary

- **Heartbeat** is for periodic, context-aware “awareness” checks in the **main session**, where work is typically batched and can be suppressed when there is nothing to report.
- **Cron** is for **precise scheduling** (exact timestamps, fixed intervals, or cron expressions) and can run in an **isolated session** so repeated background work does not pollute main-session history.

## Heartbeat

Heartbeats run periodically in the **main session**. They are intended for batching multiple lightweight checks (inbox, calendar, background tasks, etc.) into a single turn that can make context-aware decisions.

OpenClaw’s docs note that heartbeat runs can suppress delivery when there is nothing to report by replying with `HEARTBEAT_OK`.

## Cron

Cron is the Gateway’s built-in scheduler. It persists jobs on the Gateway host so schedules survive restarts, wakes the agent at the right time, and can optionally deliver output back to a chat.

### Scheduling modes

OpenClaw’s cron supports three schedule kinds:

- **One-shot timestamps** (`schedule.kind = "at"`): run once at an ISO 8601 time. If the timestamp omits a timezone, it is treated as UTC.
- **Fixed intervals** (`schedule.kind = "every"`): run on a cadence expressed in milliseconds.
- **Cron expressions** (`schedule.kind = "cron"`): 5-field (or 6-field with seconds) expressions with an optional IANA timezone.

For recurring “top-of-hour” expressions (for example `0 * * * *` or `0 */2 * * *`), OpenClaw applies a deterministic per-job stagger window (up to about 5 minutes) by default to reduce synchronized load spikes across many gateways; fixed-hour expressions such as `0 7 * * *` remain exact. Cron schedules can also set an explicit `schedule.staggerMs` value, including `0` for exact timing.

### Main vs isolated execution

OpenClaw distinguishes two execution styles:

- **Main session jobs** enqueue a **system event** and (optionally) wake the heartbeat runner. These jobs must use `payload.kind = "systemEvent"`.
- **Isolated jobs** run a dedicated **agent turn** in an isolated session (`cron:<jobId>`), starting from fresh context each run. These jobs must use `payload.kind = "agentTurn"`.

### Delivery and wakeups

Cron jobs can control both **delivery** and **wake behavior**:

- **Delivery** (isolated jobs): `delivery.mode` can be `announce` (deliver to a channel/target and post a brief main-session summary), `webhook` (HTTP POST to `delivery.to`), or `none` (internal only). If delivery is omitted for isolated jobs, OpenClaw defaults to `announce`.
- **Wake mode**: jobs can request `wakeMode = "now"` (immediate) versus `wakeMode = "next-heartbeat"` (wait for the next scheduled heartbeat) for when main-session summaries are posted.

## Choosing between them

OpenClaw’s documentation suggests:

- Use **heartbeat** when work can be batched and benefits from main-session context.
- Use **cron** when timing must be exact, the task is noisy/frequent, or you want an isolated run (including model overrides).

## Related
- [OpenClaw](./OpenClaw.md)
- [External Secrets Management (OpenClaw)](./External%20Secrets%20Management%20(OpenClaw).md)
- [OpenClaw Skills](./OpenClaw%20Skills.md)

## References
1. OpenClaw Docs, “Cron vs Heartbeat: When to Use Each”. https://docs.openclaw.ai/automation/cron-vs-heartbeat
2. OpenClaw Docs, “Cron Jobs (Gateway scheduler)”. https://docs.openclaw.ai/automation/cron-jobs
