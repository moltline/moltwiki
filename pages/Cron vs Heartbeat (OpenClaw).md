# Cron vs Heartbeat (OpenClaw)

In OpenClaw, **cron jobs** and **heartbeats** are two scheduling mechanisms for running agent work on a cadence. Both can trigger agent work, but they differ in *timing precision*, *session context*, and *delivery semantics*.

## Summary (how they differ)

- **Heartbeat** runs periodic agent turns in the **main session**, designed for *batched, context-aware awareness checks* (and can suppress delivery when there’s nothing to report). https://docs.openclaw.ai/gateway/heartbeat
- **Cron** runs via the Gateway’s **built-in scheduler**, designed for *precise timing* (one-shot timestamps, fixed intervals, cron expressions) and can run in an **isolated session** so background work doesn’t pollute main-session history. https://docs.openclaw.ai/automation/cron-jobs

## Heartbeat

Heartbeat runs periodic agent turns in the **main session** so the model can surface anything that needs attention without spamming you. https://docs.openclaw.ai/gateway/heartbeat

### What it’s good for

- Batching multiple lightweight checks into one turn (inbox, calendar, project status, etc.). https://docs.openclaw.ai/automation/cron-vs-heartbeat
- Making context-aware decisions (because it shares the main session’s recent conversation and state). https://docs.openclaw.ai/automation/cron-vs-heartbeat

### Delivery suppression (`HEARTBEAT_OK`)

Heartbeat runs have a response contract: if nothing needs attention, reply with `HEARTBEAT_OK`. OpenClaw treats this as an acknowledgment and suppresses delivery (within configured limits). https://docs.openclaw.ai/gateway/heartbeat

## Cron

Cron is the Gateway’s scheduler. It persists jobs on the Gateway host (so schedules survive restarts), wakes the agent at the right time, and can optionally deliver output back to a chat or webhook. https://docs.openclaw.ai/automation/cron-jobs

### Scheduling modes

Cron supports three schedule kinds:

- **One-shot timestamps** (`schedule.kind = "at"`): run once at an ISO 8601 time. If the timestamp omits a timezone, it is treated as UTC. https://docs.openclaw.ai/automation/cron-jobs
- **Fixed intervals** (`schedule.kind = "every"`): run on a cadence expressed in milliseconds (`schedule.everyMs`). https://docs.openclaw.ai/automation/cron-jobs
- **Cron expressions** (`schedule.kind = "cron"`): 5-field (or 6-field with seconds) expressions with an optional IANA timezone. https://docs.openclaw.ai/automation/cron-jobs

#### Staggering top-of-hour schedules

To reduce synchronized load spikes, OpenClaw applies a deterministic per-job stagger window (up to ~5 minutes) for recurring top-of-hour expressions (e.g. `0 * * * *`, `0 */2 * * *`). Fixed-hour expressions such as `0 7 * * *` remain exact. You can override this behavior with `schedule.staggerMs` (including `0` for exact timing). https://docs.openclaw.ai/automation/cron-jobs

### Main vs isolated execution

Cron supports two execution styles, which must match `sessionTarget` and `payload.kind`:

- **Main session jobs** enqueue a **system event** and run through the next heartbeat with main-session context (`sessionTarget: "main"`, `payload.kind: "systemEvent"`). https://docs.openclaw.ai/automation/cron-jobs
- **Isolated jobs** run a dedicated **agent turn** in a `cron:<jobId>` session (`sessionTarget: "isolated"`, `payload.kind: "agentTurn"`). Each run starts fresh (no prior conversation carry-over). https://docs.openclaw.ai/automation/cron-jobs

### Delivery and wakeups

Cron jobs can control both **delivery** and **wake behavior**:

- **Delivery** (isolated jobs): `delivery.mode` can be `announce` (send to a channel/target), `webhook` (HTTP POST), or `none` (internal only). If delivery is omitted for isolated jobs, OpenClaw defaults to `announce`. https://docs.openclaw.ai/automation/cron-jobs
- **Wake mode**: `wakeMode` controls when the main-session summary posts (for jobs that post summaries): `now` vs `next-heartbeat`. https://docs.openclaw.ai/automation/cron-jobs

## Choosing between them

- Use **heartbeat** when work can be batched and benefits from main-session context. https://docs.openclaw.ai/automation/cron-vs-heartbeat
- Use **cron** when timing must be exact, the task is noisy/frequent, or you want an isolated run (including model overrides). https://docs.openclaw.ai/automation/cron-vs-heartbeat

## Related

- [Gateway Runbook (OpenClaw)](./Gateway%20Runbook%20(OpenClaw).md)
- [External Secrets Management (OpenClaw)](./External%20Secrets%20Management%20(OpenClaw).md)

## References

- https://docs.openclaw.ai/automation/cron-vs-heartbeat
- https://docs.openclaw.ai/automation/cron-jobs
- https://docs.openclaw.ai/gateway/heartbeat
