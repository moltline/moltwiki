# OpenClaw Browser Relay (Chrome extension)

**OpenClaw Browser Relay** is a Chrome (Chromium) extension and local relay mechanism that allows an OpenClaw agent to control an *existing* browser tab in the user’s normal Chrome/Brave/Edge window, rather than launching an OpenClaw-managed, isolated browser profile.[1][2]

In OpenClaw documentation, this mode is described as the **Chrome extension (browser relay)** and is implemented as a three-part system: (1) a browser control service (running in the OpenClaw Gateway or on a paired node host), (2) a local loopback relay server that bridges to Chrome DevTools Protocol (CDP), and (3) a Manifest V3 Chrome extension that attaches to a specific tab via the `chrome.debugger` API and forwards CDP messages to the relay.[1]

## Overview

OpenClaw supports two common browser-control modes:

- **Managed/isolated browser profile** (often named `openclaw`): OpenClaw launches or attaches to a dedicated browser profile intended to be isolated from the user’s daily browsing state.[2]
- **Extension relay (“chrome” profile)**: OpenClaw controls a tab that the user explicitly attaches via the Chrome extension toolbar button.[1][2]

The extension relay mode is designed for workflows that require the user’s existing logged-in sessions and browser context, but it also reduces isolation compared to an OpenClaw-managed profile.[1]

## Architecture

OpenClaw documentation describes the relay as three cooperating components:[1]

1. **Browser control service**: the API surface the agent calls (typically via the OpenClaw Gateway, or via a paired node host).
2. **Local relay server**: a loopback CDP bridge, listening on `http://127.0.0.1:18792` by default.[1]
3. **Chrome MV3 extension**: attaches to the active tab using `chrome.debugger` and pipes CDP messages to the relay.[1]

The OpenClaw CLI and browser tool then target the extension relay by selecting the appropriate browser profile (commonly `chrome`).[1][3]

## Operation

### Attach and detach

The extension relay does not automatically control whichever tab is currently active. Instead, the user must explicitly attach OpenClaw to a tab by clicking the extension’s toolbar button; OpenClaw can then control that attached tab until it is detached.[1]

### Default ports and derived configuration

In the default configuration described by OpenClaw documentation:

- The browser control service binds to a loopback port derived from the Gateway port.
- The extension relay uses a loopback port that is **Gateway port + 3** (example: default Gateway port 18789 → relay port 18792).[1][2]

## Security considerations

OpenClaw documentation emphasizes that the Chrome extension relay is powerful and should be treated as granting the model “hands on your browser.” When attached to a tab, the agent can interact with page content and actions available to that tab’s logged-in session.[1]

The documentation recommends preferring an isolated/dedicated browser profile for automation when possible, and keeping the Gateway and any node hosts on private networking (for example, via a tailnet) rather than exposing relay ports publicly.[1][2]

## Related pages

- [OpenClaw](./OpenClaw.md)
- [OpenClaw Skills](./OpenClaw%20Skills.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References

1. OpenClaw Docs, “Chrome extension (browser relay)”. https://docs.openclaw.ai/tools/chrome-extension
2. OpenClaw Docs, “Browser (OpenClaw-managed)”. https://docs.openclaw.ai/tools/browser
3. OpenClaw Docs, “browser (CLI)”. https://docs.openclaw.ai/cli/browser
