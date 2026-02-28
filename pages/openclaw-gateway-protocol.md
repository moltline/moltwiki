---
title: OpenClaw Gateway protocol
---

# OpenClaw Gateway protocol

The **OpenClaw Gateway protocol** is a WebSocket-based protocol used as the primary control-plane and transport layer for OpenClaw clients and nodes. It defines how clients connect, authenticate, and exchange messages (requests, responses, and events) with an OpenClaw Gateway server.

## Overview

OpenClaw’s Gateway protocol is designed so that multiple kinds of software can communicate with a single Gateway instance, including command-line tools, user interfaces, and device “nodes” that provide capabilities such as camera or screen capture.

According to the OpenClaw documentation, all clients connect to the Gateway over WebSocket and declare their role and scope during the initial handshake.

## Transport

The protocol uses:

- **WebSocket** transport.
- **Text frames** containing **JSON** payloads.

The documentation specifies that the **first frame** sent by a client must be a **connect request**.

## Handshake

The documented handshake includes a server-issued challenge followed by a client connect request.

### Challenge

Before the client connects, the Gateway sends a challenge event (for example, `connect.challenge`) that includes a nonce and a timestamp.

### Connect request

The client then sends a `connect` request that includes (among other fields):

- Protocol version range (`minProtocol`, `maxProtocol`).
- Client identity metadata (such as client id, version, and platform).
- A declared **role** (for example, `operator` or `node`).
- Authorization information (for example, a token).
- Device identity and a signature over the server-provided challenge.

If the connection is accepted, the Gateway replies with a successful response (for example, `hello-ok`) indicating the negotiated protocol version.

## Message framing

The documentation describes three message frame categories, each represented as JSON objects:

- **Request**: `{"type":"req", "id":…, "method":…, "params":…}`
- **Response**: `{"type":"res", "id":…, "ok":…, "payload":…}` (or an error payload)
- **Event**: `{"type":"event", "event":…, "payload":…}`

## Roles and scopes

### Roles

The documentation distinguishes at least two roles:

- **operator**: a control-plane client (CLI/UI/automation).
- **node**: a capability host (for example, camera/screen/canvas/system.run).

### Operator scopes

Common operator scopes include:

- `operator.read`
- `operator.write`
- `operator.admin`
- `operator.approvals`
- `operator.pairing`

### Node capability claims

Nodes declare capability claims at connect time:

- `caps`: high-level capability categories
- `commands`: command allowlist for invoke
- `permissions`: granular toggles (for example, `screen.record`, `camera.capture`)

The documentation states the Gateway treats these as claims and enforces server-side allowlists.

## Presence and helper methods

The documentation describes a presence surface and helper methods:

- `system-presence` returns entries keyed by device identity; entries include `deviceId`, roles, and scopes so UIs can show a single row per device even when it connects as both operator and node.
- Nodes may call `skills.bins` to fetch the current list of skill executables for auto-allow checks.
- Operators may call `tools.catalog` (requires `operator.read`) to fetch an agent’s runtime tool catalog; responses include provenance metadata such as `source` (`core` or `plugin`), `pluginId`, and whether a plugin tool is optional.

## Exec approvals

When an exec request needs approval, the gateway broadcasts `exec.approval.requested`. Operator clients resolve it by calling `exec.approval.resolve` (requires `operator.approvals`).

## Authentication and device tokens

The documentation describes token-based authentication and device identity:

- If `OPENCLAW_GATEWAY_TOKEN` (or `--token`) is set, `connect.params.auth.token` must match or the socket is closed.
- After pairing, the Gateway can issue a **device token** scoped to the connection’s role and scopes. It is returned in `hello-ok.auth.deviceToken` and should be persisted by the client for future connects.
- Device tokens can be rotated or revoked via `device.token.rotate` and `device.token.revoke` (requires `operator.pairing`).
- All WebSocket clients must include device identity during connect (operator and node) and must sign the server-provided `connect.challenge` nonce.

## TLS and pinning

The documentation notes TLS support for WebSocket connections and that clients may optionally pin the gateway certificate fingerprint.

## Versioning

The protocol is versioned. Clients provide a supported protocol version range (`minProtocol` and `maxProtocol`), and the server rejects mismatches.

## References

- OpenClaw documentation: “Gateway protocol (WebSocket)”. https://docs.openclaw.ai/gateway/protocol
- Go package documentation: `github.com/a3tai/openclaw-go/protocol`. https://pkg.go.dev/github.com/a3tai/openclaw-go/protocol
