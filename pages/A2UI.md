# A2UI

**A2UI** is a JSONL-delivered UI description protocol used by OpenClaw to render small, agent-controlled interface “surfaces” inside the OpenClaw Canvas panel.

In OpenClaw, A2UI is rendered inside the macOS app’s Canvas panel (a WKWebView-based workspace). Agents push A2UI messages to a node via the Gateway so the client can update UI component trees and data models. https://docs.openclaw.ai/platforms/mac/canvas

## Overview

### What it’s for
A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to build or host a separate web app. Canvas can display local HTML/CSS/JS content as well as A2UI-driven surfaces. https://docs.openclaw.ai/platforms/mac/canvas

### Where it runs
The macOS Canvas panel can load local Canvas content via the `openclaw-canvas:///` custom URL scheme and can also navigate to HTTP(S) URLs. https://docs.openclaw.ai/platforms/mac/canvas

Canvas state is stored under Application Support (macOS):

- `~/Library/Application Support/OpenClaw/canvas/` https://docs.openclaw.ai/platforms/mac/canvas

For A2UI specifically, OpenClaw documents a default host page served by the Gateway canvas host:

- `http://<gateway-host>:18789/__openclaw__/a2ui/` https://docs.openclaw.ai/platforms/mac/canvas

When the Gateway advertises a Canvas host, the macOS app auto-navigates to the A2UI host page the first time the panel is opened (per the Canvas documentation). https://docs.openclaw.ai/platforms/mac/canvas

## Protocol and versions

OpenClaw’s Canvas documentation states that Canvas currently accepts **A2UI v0.8** server→client messages and does **not** support the v0.9 `createSurface` message. https://docs.openclaw.ai/platforms/mac/canvas

### Message types (v0.8 in Canvas)
Canvas accepts the following A2UI v0.8 server→client message types:

- `beginRendering`
- `surfaceUpdate`
- `dataModelUpdate`
- `deleteSurface`

https://docs.openclaw.ai/platforms/mac/canvas

#### Minimal lifecycle (typical)
A common pattern is:

1) Send a `surfaceUpdate` that defines/updates the component tree for a `surfaceId`.
2) Send `dataModelUpdate` messages as data changes.
3) Send `beginRendering` to select a `root` component id to render.
4) Send `deleteSurface` when the surface should be removed.

(Exact semantics are defined by the Canvas implementation; the docs primarily enumerate supported message types.) https://docs.openclaw.ai/platforms/mac/canvas

## Usage in OpenClaw

### Transport / API surface
Canvas is exposed via the Gateway WebSocket API, so an agent can:

- show/hide the panel
- navigate to a path or URL
- evaluate JavaScript
- capture a snapshot image
- push A2UI updates

https://docs.openclaw.ai/platforms/mac/canvas

The documentation notes that `canvas.navigate` accepts local canvas paths (including `/` for the scaffold or `index.html`), HTTP(S) URLs, and `file://` URLs. https://docs.openclaw.ai/platforms/mac/canvas

### CLI example (A2UI v0.8)
OpenClaw’s docs include an example of pushing an A2UI v0.8 JSONL payload to a node via the CLI (and a quick “smoke” push that sends a text string). https://docs.openclaw.ai/platforms/mac/canvas

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
- OpenClaw Docs: “Canvas (macOS app)” (Canvas storage paths, `openclaw-canvas:///`, A2UI hosting, and supported v0.8 message list). https://docs.openclaw.ai/platforms/mac/canvas

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
