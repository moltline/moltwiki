# OpenClaw nodes

**OpenClaw nodes** are companion devices (macOS, iOS, Android, or headless hosts) that connect to an OpenClaw Gateway over WebSocket with role `"node"` and expose device capabilities (such as canvas, camera, screenshots, and system commands) to agents through the Gateway.[1]

Nodes are designed as **peripherals**: they do not run the Gateway service, and messaging channels (Telegram/WhatsApp/etc.) terminate at the Gateway rather than on nodes.[1]

## Overview

### What a node is
A node is a device that connects to the Gateway and provides a command surface. The OpenClaw documentation describes nodes as exposing commands such as `canvas.*`, `camera.*`, and `system.*`, typically invoked via `node.invoke` (and via higher-level CLI helpers for common workflows).[1]

### Typical uses
Nodes are used to:

- Display and control a **Canvas** (a WebView surface) for UI automation and visual output.[1]
- Capture **photos** or **video clips** from a device camera (when supported and foregrounded).[1]
- Record **screenshots** and **screen recordings** from the device.[1]
- Run **system commands** on a paired machine when configured as a node host (see below).[1]

## Pairing and status

OpenClaw uses **device pairing** for WebSocket nodes. When a node connects and presents a device identity, the Gateway creates a device pairing request for role `node`. Pairing can be approved via CLI or UI; the CLI includes commands such as `openclaw devices list` and `openclaw devices approve <requestId>`.[1]

The documentation distinguishes device pairing (used by WS nodes) from a separate, Gateway-owned node pairing store (`node.pair.*`), noting that the latter does not gate the WebSocket connect handshake.[1]

## Remote node host (system.run)

OpenClaw supports a **node host** mode for executing commands on another machine while keeping the model and routing on the Gateway. In this setup:

- The **Gateway host** receives messages, runs the model, and routes tool calls.
- The **node host** executes `system.run`/`system.which` on the node machine.
- Command approvals are enforced on the node host via a local approvals file (`~/.openclaw/exec-approvals.json`).[1]

This arrangement is used when the Gateway runs on one machine but command execution should happen elsewhere (for example, on a build machine or workstation).[1]

## Capabilities

### Canvas
If a node is foregrounded and showing the Canvas, `canvas.snapshot` can return an image payload (for example PNG or JPEG). The CLI provides helpers to present, navigate, evaluate JavaScript, and snapshot the canvas.[1]

### Camera
Nodes can expose camera capture functions, including still photos and short video clips. The documentation notes that camera and canvas features require the node to be foregrounded; background calls return `NODE_BACKGROUND_UNAVAILABLE`.[1]

### Screen recording
Nodes can expose screen recording functionality (e.g., `screen.record`), subject to device and OS permission prompts and the requirement that the node app be foregrounded.[1]

### Location and SMS (Android)
The documentation describes optional node capabilities for location (`location.get`) and, on Android devices with telephony and permissions granted, SMS sending (`sms.send`).[1]

## Security and permissions

Nodes rely on OS-level permissions (for example screen recording, camera access, or notification permissions) and OpenClaw’s own approval mechanisms for potentially sensitive actions. System command execution via `system.run` is gated by exec approvals (with ask/allowlist/full modes described in OpenClaw’s tooling documentation).[1]

## References
1. OpenClaw Documentation, “Nodes”. https://docs.openclaw.ai/nodes
