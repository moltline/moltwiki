# OpenClaw Canvas

**OpenClaw Canvas** is an agent-controlled panel in the OpenClaw macOS app that provides a lightweight visual workspace for rendering HTML/CSS/JavaScript and interactive UI surfaces, including A2UI content hosted by the OpenClaw Gateway.[1]

## Overview

The Canvas panel is embedded in the macOS app using **WKWebView** and is designed to display small, interactive UI surfaces that an OpenClaw agent can control through the Gateway.[1]

## Storage and URL scheme

Canvas state is stored under the user’s Application Support directory (for example, `~/Library/Application Support/OpenClaw/canvas/`).[1] Local Canvas files are served to the panel using a custom URL scheme, `openclaw-canvas:///`, that maps URL paths to files under the Canvas directory.[1]

## Panel behavior

According to OpenClaw documentation, the Canvas panel is borderless and resizable, remembers size and position per session, and auto-reloads when local Canvas files change.[1] Canvas can be disabled in the app’s settings; when disabled, Canvas-related node commands return an error (documented as `CANVAS_DISABLED`).[1]

## Agent control surface

Canvas is exposed via the OpenClaw Gateway WebSocket interface. Documented operations include showing and hiding the panel, navigating to a local path or URL, evaluating JavaScript, and capturing a snapshot image.[1]

## A2UI in Canvas

A2UI content can be rendered in Canvas via the Gateway’s Canvas host page (documented default path `http://<gateway-host>:18789/__openclaw__/a2ui/`).[1] The macOS app can auto-navigate to the A2UI host page when a Canvas host is advertised.[1]

The documentation states that Canvas accepts **A2UI v0.8** server-to-client messages including `beginRendering`, `surfaceUpdate`, `dataModelUpdate`, and `deleteSurface`, and that `createSurface` (v0.9) is not supported.[1]

## Security notes

OpenClaw documentation describes several security-related properties of Canvas, including blocking directory traversal for the custom scheme and allowing external `http(s)` URLs only when explicitly navigated.[1]

## References

1. OpenClaw documentation. "Canvas (macOS app)". https://docs.openclaw.ai/platforms/mac/canvas (accessed 2026-02-28).
