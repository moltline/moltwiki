# A2UI

**A2UI** is a JSON-based UI description protocol used by OpenClaw to render small, agent-controlled interface “surfaces” inside the OpenClaw Canvas panel.

In OpenClaw’s documentation, A2UI is described as being hosted by the Gateway’s Canvas host (under a built-in HTTP path) and rendered in the macOS app’s Canvas panel (a WKWebView-based workspace). A2UI messages are pushed from the agent to the node to update UI components and data models.\[1\]

## Overview

### Purpose
A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to manually build or host a separate web app. In OpenClaw, A2UI is one of several content types that can be shown in Canvas alongside ordinary HTML/CSS/JS surfaces.\[1\]

### Where it runs
OpenClaw’s macOS Canvas panel loads local Canvas content via a custom URL scheme (`openclaw-canvas:///`) and can also navigate to HTTP(S) URLs. For A2UI specifically, OpenClaw documents a default host page served by the Gateway:

- `http://<gateway-host>:18789/__openclaw__/a2ui/`\[1\]

## Protocol and versions

OpenClaw’s Canvas documentation notes that, at least in the macOS app context, Canvas accepts **A2UI v0.8** server→client messages and does not support the v0.9 `createSurface` message.\[1\]

### Message types (v0.8 in Canvas)
OpenClaw documents the following A2UI v0.8 message types as accepted by Canvas:\[1\]

- `beginRendering`
- `surfaceUpdate`
- `dataModelUpdate`
- `deleteSurface`

## Usage in OpenClaw

### Transport
In OpenClaw, Canvas and A2UI are exposed to agents via the Gateway WebSocket API, and nodes (such as the macOS app) implement Canvas-related commands that let an agent present/hide the panel and push A2UI updates.\[1\]

### CLI example
OpenClaw’s Canvas documentation includes an example of pushing an A2UI v0.8 JSONL payload to a node via the CLI.\[1\]

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
1. OpenClaw Docs: “Canvas (macOS app)” (includes “A2UI in Canvas” and v0.8 message list). https://docs.openclaw.ai/platforms/mac/canvas

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
