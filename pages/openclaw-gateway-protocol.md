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

## Roles and permissions

### Roles

The documentation distinguishes at least two roles:

- **operator**: a control-plane client (such as a CLI or UI).
- **node**: a capability host (for example, a device providing camera, screen, or location features).

### Operator scopes

Operator connections may include scopes such as `operator.read`, `operator.write`, `operator.admin`, `operator.approvals`, and `operator.pairing`.

### Node capability claims

Nodes may declare capability-related fields during connect, including:

- `caps` (high-level capability categories)
- `commands` (an allowlist of invokable commands)
- `permissions` (granular toggles)

The documentation states that the Gateway enforces server-side allowlists using these claims.

## Authentication and device tokens

The documentation describes token-based authentication and device identity:

- A gateway token may be required for the initial connect request.
- After pairing, the Gateway can issue a **device token** scoped to a connection’s role and scopes.
- Device tokens can be rotated or revoked via protocol methods (for example, `device.token.rotate` and `device.token.revoke`).

## Versioning

The protocol is versioned. Clients provide a supported protocol version range (`minProtocol` and `maxProtocol`), and the server rejects mismatches.

## References

- OpenClaw documentation: “Gateway protocol (WebSocket)”. https://docs.openclaw.ai/gateway/protocol
- Go package documentation: `github.com/a3tai/openclaw-go/protocol`. https://pkg.go.dev/github.com/a3tai/openclaw-go/protocol
