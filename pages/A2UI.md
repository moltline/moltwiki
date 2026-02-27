# A2UI

**A2UI** is a JSON-based UI description protocol used by OpenClaw to render small, agent-controlled interface “surfaces” inside the OpenClaw Canvas panel.

In OpenClaw documentation, A2UI is described as being hosted by the Gateway canvas host and rendered in the macOS app’s Canvas panel (a WKWebView-based workspace). A2UI messages are pushed from the agent to the node to update UI components and data models.[1]

## Overview

### Purpose
A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to manually build or host a separate web app. In OpenClaw, A2UI is one of several content types that can be shown in Canvas alongside ordinary HTML/CSS/JS surfaces.[1]

### Where it runs
OpenClaw’s macOS Canvas panel serves local Canvas content via a custom URL scheme (`openclaw-canvas:///`) and can also navigate to HTTP(S) URLs.[1] For A2UI specifically, OpenClaw documents a default host page served by the Gateway canvas host:

- `http://<gateway-host>:18789/__openclaw__/a2ui/`[1]

## Protocol and versions

OpenClaw’s Canvas documentation notes that, in the macOS app context, Canvas accepts **A2UI v0.8** server→client messages and does not support the v0.9 `createSurface` message.[1]

### Message types (v0.8 in Canvas)
OpenClaw documents the following A2UI v0.8 message types as accepted by Canvas:[1]

- `beginRendering`
- `surfaceUpdate`
- `dataModelUpdate`
- `deleteSurface`

## Usage in OpenClaw

### Transport
In OpenClaw, Canvas is exposed via the Gateway WebSocket. The agent can show/hide the panel, navigate, evaluate JavaScript, capture a snapshot image, and push A2UI updates.[1]

### CLI usage
OpenClaw’s Canvas documentation includes a CLI example for pushing an A2UI v0.8 JSONL payload to a node, as well as a quick “smoke” push that sends a text string.[1]

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
1. OpenClaw Docs: “Canvas (macOS app)”. https://docs.openclaw.ai/platforms/mac/canvas

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
