# OpenClaw Chrome extension (browser relay)

The **OpenClaw Chrome extension** (also called the **browser relay**) is a Manifest V3 (MV3) Chrome extension that allows OpenClaw to control an *existing* user Chrome tab (a “daily driver” Chrome window/profile) rather than launching a separate, OpenClaw-managed browser profile.

This capability is typically used for **computer-use** and **web automation** workflows where the agent needs to interact with sites already logged in within the user’s normal browser session.

## Overview

In the OpenClaw browser-relay architecture, the extension is one of three cooperating components:

1. **Browser control service** (running in the OpenClaw Gateway or on a paired node host): provides the API surface the agent calls.
2. **Local relay server** (loopback CDP bridge): connects the browser control service to the extension over a local HTTP endpoint (default `http://127.0.0.1:18792`).
3. **Chrome MV3 extension**: attaches to the active tab using Chrome’s `chrome.debugger` API and pipes Chrome DevTools Protocol (CDP) messages through the relay.

OpenClaw then controls the attached tab by selecting an appropriate browser profile (commonly the built-in profile named `chrome`).

## Installation

OpenClaw ships the extension as static files inside its release distribution (no separate build step).
A typical “unpacked extension” installation flow is:

- Install/copy the extension files to a stable on-disk directory:

  ```sh
  openclaw browser extension install
  ```

- Print the installed extension directory path:

  ```sh
  openclaw browser extension path
  ```

- In Chrome, open `chrome://extensions`, enable **Developer mode**, then **Load unpacked** and select the directory printed by the CLI. Pin the extension to the toolbar.

After upgrading OpenClaw, users typically re-run `openclaw browser extension install` and then click **Reload** for the extension in `chrome://extensions`.

## Configuration and use

OpenClaw includes a built-in browser profile named `chrome` intended for extension relay control. Before first use, the extension’s Options page is used to set:

- **Port** (default `18792`)
- **Gateway token** (must match the Gateway configuration, e.g. `gateway.auth.token` / `OPENCLAW_GATEWAY_TOKEN`)

To control a tab, the user opens the desired tab and clicks the extension’s toolbar button:

- **Badge ON** indicates the tab is attached and can be controlled.
- Clicking again detaches.

The extension does not automatically control whichever tab is focused; it controls only the tab(s) explicitly attached.

### Custom Gateway ports

If the OpenClaw Gateway is configured to listen on a non-default port, OpenClaw documents a derived default for the extension relay port:

> **Extension relay port = Gateway port + 3**

For example, if the Gateway port is `19001`, the relay port would be `19004`.

## Security considerations

The browser relay is powerful and increases risk relative to a dedicated, isolated browser profile:

- When attached, the agent can **click, type, navigate**, and **read page content** in that tab.
- The agent can access whatever the tab’s **logged-in session** can access.

OpenClaw documentation recommends using a **dedicated Chrome profile** for relay usage (separate from personal browsing), keeping the Gateway and any node hosts on a private network/tailnet, and avoiding exposure of relay ports to LAN or the public Internet.

## See also

- [Browser tool (OpenClaw)](./OpenClaw%20Skills.md) (tooling overview is typically linked from OpenClaw docs)
- [OpenClaw security audit](./OpenClaw%20security%20audit.md)

## References

1. OpenClaw documentation, “Chrome extension (browser relay)”. https://docs.openclaw.ai/tools/chrome-extension
2. OpenClaw documentation, “browser (CLI)”. https://docs.openclaw.ai/cli/browser
