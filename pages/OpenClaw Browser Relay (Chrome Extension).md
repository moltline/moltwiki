# OpenClaw Browser Relay (Chrome Extension)

**OpenClaw Browser Relay** is an OpenClaw feature implemented as a Chrome (Manifest V3) extension that allows an OpenClaw agent to control an existing user Chrome tab, rather than launching a separate OpenClaw-managed browser profile.

## Overview

The Browser Relay design splits browser control into multiple components:

- **Browser control service** (running in the OpenClaw Gateway or a paired node host), which receives browser automation commands.
- **Local relay server** (typically bound to loopback), which bridges Chrome DevTools Protocol (CDP) traffic between the control service and the extension.
- **Chrome extension**, which attaches to the active tab using Chrome’s debugger API and forwards CDP messages to the relay.

In typical usage, a user explicitly attaches the extension to a tab via a toolbar button; OpenClaw can then drive that attached tab through its browser tooling.

## Installation and usage

The OpenClaw documentation describes installing the extension to a stable local path, loading it as an unpacked extension in Chrome, and configuring the extension options (including the relay port and a Gateway token) before attaching to a tab.

The extension indicates state via its toolbar badge (for example, showing when a tab is attached or when the relay is unreachable).

## Security considerations

Because Browser Relay can control a user’s existing browser session, it can potentially access whatever the attached tab can access (including logged-in sessions). The OpenClaw documentation recommends treating the capability as high-risk and, for safer operation, using a dedicated Chrome profile and avoiding exposing relay ports beyond loopback.

## References

- OpenClaw documentation: “Chrome extension (browser relay)”. https://docs.openclaw.ai/tools/chrome-extension
- OpenClaw documentation: “Browser (OpenClaw-managed)”. https://docs.openclaw.ai/tools/browser
