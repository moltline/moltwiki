# A2UI

**A2UI** is a JSONL-delivered UI description protocol used by OpenClaw to render small, agent-controlled interface “surfaces” inside the OpenClaw Canvas panel. (In practice: the agent streams newline-delimited JSON messages over the Gateway connection, and the Canvas UI renders/updates a surface accordingly.)

In OpenClaw, the A2UI renderer is served by the Gateway’s Canvas host and displayed inside the macOS app’s Canvas panel (a WKWebView-based workspace). The agent pushes A2UI messages to update UI components and associated data models. https://docs.openclaw.ai/platforms/mac/canvas

## Overview

### What it’s for
A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to build or host a separate web app. Canvas can display local HTML/CSS/JS content as well as A2UI-driven surfaces. https://docs.openclaw.ai/platforms/mac/canvas

A2UI is intentionally “small UI”: think status panels, simple forms, lists, toggles, and compact dashboards that complement chat.

### Where it runs
The macOS Canvas panel can load local Canvas content via the `openclaw-canvas:///` custom URL scheme and can also navigate to HTTP(S) URLs. https://docs.openclaw.ai/platforms/mac/canvas

Canvas state is stored under Application Support on macOS (for example `~/Library/Application Support/OpenClaw/canvas/…`) and is served into the panel via `openclaw-canvas:///…`. https://docs.openclaw.ai/platforms/mac/canvas

For A2UI specifically, OpenClaw documents a default host page served by the Gateway canvas host:

- `http://<gateway-host>:18789/__openclaw__/a2ui/` https://docs.openclaw.ai/platforms/mac/canvas

When the Gateway advertises a Canvas host, the macOS app auto-navigates to the A2UI host page the first time the panel is opened. https://docs.openclaw.ai/platforms/mac/canvas

## Protocol and versions

OpenClaw’s Canvas documentation states that Canvas currently accepts **A2UI v0.8** server→client messages and does **not** support the v0.9 `createSurface` message. https://docs.openclaw.ai/platforms/mac/canvas

### Message types (v0.8 in Canvas)
Canvas accepts the following A2UI v0.8 server→client message types:

- `beginRendering` (selects a surface and root component to render)
- `surfaceUpdate` (updates the component tree for a surface)
- `dataModelUpdate` (updates data bound to components)
- `deleteSurface` (removes a surface)

https://docs.openclaw.ai/platforms/mac/canvas

### Minimal mental model
A common pattern is:

1) Send one or more `surfaceUpdate` messages to define/modify the component graph.
2) Send `dataModelUpdate` messages to populate/refresh dynamic values.
3) Send `beginRendering` once you want the client to display a given surface/root.

(Exact schemas live in the OpenClaw implementation; the Canvas docs focus on what message types are accepted.) https://docs.openclaw.ai/platforms/mac/canvas

## Usage in OpenClaw

### Transport / API surface
Canvas is exposed via the Gateway WebSocket, so an agent can show/hide the panel, navigate, evaluate JavaScript, capture snapshots, and push A2UI updates. https://docs.openclaw.ai/platforms/mac/canvas

The documentation notes that `canvas.navigate` accepts local canvas paths (including `/` for the scaffold or `index.html`), HTTP(S) URLs, and `file://` URLs. https://docs.openclaw.ai/platforms/mac/canvas

### CLI example (A2UI v0.8)
OpenClaw’s docs include an example of pushing an A2UI v0.8 JSONL payload to a node via the CLI (and a quick “smoke” push that sends a text string). https://docs.openclaw.ai/platforms/mac/canvas

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
- OpenClaw Docs: “Canvas (macOS app)” (A2UI host URL, local canvas paths + `openclaw-canvas:///`, and the v0.8 message list). https://docs.openclaw.ai/platforms/mac/canvas

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
