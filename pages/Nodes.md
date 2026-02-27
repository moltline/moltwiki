# Nodes (OpenClaw)

In **OpenClaw**, a **node** is a companion device (for example macOS, iOS, Android, or a headless host) that connects to the **OpenClaw Gateway** and exposes capabilities the assistant can use, such as presenting a Canvas view, capturing camera photos, recording the screen, and running approved system commands.

Nodes are peripherals: they do not run the Gateway service. Messaging channels (for example Telegram) connect to the Gateway; the Gateway then targets nodes for device-local actions.

## Overview

Nodes connect to the Gateway over the Gateway WebSocket transport with role `node`. Once connected and paired, they can be addressed by id/name/IP and invoked via high-level helpers (for example `openclaw nodes camera snap`) or low-level RPC (`openclaw nodes invoke`).

## Pairing and status

OpenClaw uses device pairing for WebSocket nodes. When a node connects, the Gateway creates a pairing request for the `node` role. After approval, the node appears in node listings and can be targeted by node commands.

Common CLI commands include:

- `openclaw nodes status`
- `openclaw nodes describe --node <idOrNameOrIp>`

## Node capabilities

Capabilities vary by platform and permissions, but commonly include:

### Canvas (UI)

A node can present and control a Canvas (a WebView surface) for showing web pages or local content, and can return screenshots via canvas snapshots.

### Camera capture

On supported devices, a node can list cameras and capture photos or short video clips. Camera operations typically require the node app to be in the foreground.

### Screen recording

Nodes can record the device screen (subject to platform permissions). On some platforms (notably Android), the operating system may prompt the user to approve screen capture.

### Location

If enabled in settings and permitted by the OS, nodes can provide location readings with an accuracy and timestamp.

### System commands (node host)

A headless **node host** can be used to execute `system.run` and related commands on a remote machine. Execution is gated by OpenClaw’s exec approvals/allowlist mechanism.

## Foreground and permission requirements

Many node features (notably `canvas.*`, `camera.*`, and `screen.record`) require the node app to be foregrounded; background calls can fail with an error indicating the node is unavailable in the background.

Nodes may also report a permissions map (for example whether screen recording permission is granted), which can help diagnose failures.

## See also

- [OpenClaw Gateway](OpenClaw%20Gateway.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [OpenClaw Mission Control](OpenClaw%20Mission%20Control.md)

## References

- OpenClaw Docs: “Nodes”. https://docs.openclaw.ai/nodes
- OpenClaw Docs: “Node troubleshooting”. https://docs.openclaw.ai/nodes/troubleshooting
- OpenClaw Docs: “CLI reference”. https://docs.openclaw.ai/cli
- OpenClaw Docs: “Tools”. https://docs.openclaw.ai/tools
