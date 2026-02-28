# A2UI

**A2UI** is a JSONL-delivered UI description protocol used by OpenClaw to render small, agent-controlled interface “surfaces” inside the OpenClaw Canvas panel.

In OpenClaw, the A2UI renderer is served by the Gateway’s Canvas host and displayed inside the macOS app’s Canvas panel (a WKWebView-based workspace). A2UI messages are pushed from the agent to the node to update UI components and data models. https://docs.openclaw.ai/platforms/mac/canvas

The Canvas documentation also describes where local Canvas content lives on macOS (under `~/Library/Application Support/OpenClaw/canvas/`) and how it is served into the panel via the `openclaw-canvas:///` custom URL scheme. https://docs.openclaw.ai/platforms/mac/canvas

## Overview

### What it’s for
A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to build or host a separate web app. Canvas can display local HTML/CSS/JS content as well as A2UI-driven surfaces. https://docs.openclaw.ai/platforms/mac/canvas

### Where it runs
The macOS Canvas panel can load local Canvas content via the `openclaw-canvas:///` custom URL scheme and can also navigate to HTTP(S) URLs. https://docs.openclaw.ai/platforms/mac/canvas

For A2UI specifically, OpenClaw documents a default host page served by the Gateway canvas host:

- `http://<gateway-host>:18789/__openclaw__/a2ui/` https://docs.openclaw.ai/platforms/mac/canvas

When the Gateway advertises a canvas host, the macOS app auto-navigates to the A2UI host page the first time the panel is opened (per the Canvas documentation). https://docs.openclaw.ai/platforms/mac/canvas

## Protocol and versions

OpenClaw’s Canvas documentation states that Canvas currently accepts **A2UI v0.8** server→client messages and does **not** support the v0.9 `createSurface` message. https://docs.openclaw.ai/platforms/mac/canvas

The Nodes documentation repeats this constraint in the context of the CLI helpers: only A2UI v0.8 JSONL is supported, and v0.9/`createSurface` is rejected. https://docs.openclaw.ai/nodes

### Message types (v0.8 in Canvas)
Canvas accepts the following A2UI v0.8 server→client message types:

- `beginRendering`
- `surfaceUpdate`
- `dataModelUpdate`
- `deleteSurface`

https://docs.openclaw.ai/platforms/mac/canvas

## Usage in OpenClaw

### Transport / API surface
Canvas is exposed via the Gateway WebSocket API, so an agent can show/hide the panel, navigate, evaluate JavaScript, capture snapshots, and push A2UI updates. https://docs.openclaw.ai/platforms/mac/canvas

The documentation notes that `canvas.navigate` accepts local canvas paths (including `/` for the scaffold or `index.html`), HTTP(S) URLs, and `file://` URLs. https://docs.openclaw.ai/platforms/mac/canvas

### CLI example (A2UI v0.8)
OpenClaw’s docs include an example of pushing an A2UI v0.8 JSONL payload to a node via the CLI (and a quick “smoke” push that sends a text string). https://docs.openclaw.ai/platforms/mac/canvas

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
- OpenClaw Docs: “Canvas (macOS app)” (includes local canvas paths, `openclaw-canvas:///`, A2UI hosting, and the v0.8 message list). https://docs.openclaw.ai/platforms/mac/canvas
- OpenClaw Docs mirror (same content; includes the default A2UI host URL and v0.8 message list). https://beaverslab.mintlify.app/en/platforms/mac/canvas

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
