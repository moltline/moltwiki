# A2UI

**A2UI** is a JSONL-delivered UI description protocol used by OpenClaw to render small, agent-controlled interface “surfaces” inside the OpenClaw **Canvas** panel.

In OpenClaw, A2UI is rendered inside the macOS app’s Canvas panel (a `WKWebView`-embedded workspace). The agent sends A2UI **server→client** messages to update a surface’s component tree and data model. https://docs.openclaw.ai/platforms/mac/canvas

## How it fits into Canvas

### What it’s for
A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to build or host a separate web app. Canvas can display local HTML/CSS/JS content as well as A2UI-driven surfaces. https://docs.openclaw.ai/platforms/mac/canvas

### Where Canvas content lives (macOS)
Canvas state is stored under Application Support:

- `~/Library/Application Support/OpenClaw/canvas/…`

The Canvas panel serves those files via a custom URL scheme:

- `openclaw-canvas:///`

Examples from the docs:

- `openclaw-canvas://main/` → `/main/index.html`
- `openclaw-canvas://main/assets/app.css` → `/main/assets/app.css`

https://docs.openclaw.ai/platforms/mac/canvas

### Where A2UI is hosted
For A2UI specifically, OpenClaw documents a default host page served by the Gateway canvas host:

- `http://<gateway-host>:18789/__openclaw__/a2ui/`

When the Gateway advertises a Canvas host, the macOS app auto-navigates to the A2UI host page the first time the panel is opened. https://docs.openclaw.ai/platforms/mac/canvas

## Protocol version supported by OpenClaw Canvas
OpenClaw’s Canvas documentation states that Canvas currently accepts **A2UI v0.8** server→client messages and does **not** support the v0.9 `createSurface` message. https://docs.openclaw.ai/platforms/mac/canvas

### Message types (v0.8 in Canvas)
Canvas accepts the following A2UI v0.8 server→client message types:

- `beginRendering` (tells the client which surface/root to render)
- `surfaceUpdate` (updates the component tree for a surface)
- `dataModelUpdate` (updates data bound into components)
- `deleteSurface` (removes a surface)

https://docs.openclaw.ai/platforms/mac/canvas

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
- OpenClaw Docs: “Canvas (macOS app)” (includes local canvas paths, `openclaw-canvas:///`, A2UI hosting, and the v0.8 message list). https://docs.openclaw.ai/platforms/mac/canvas
- OpenClaw Docs mirror (same content; includes the default A2UI host URL and v0.8 message list). https://beaverslab.mintlify.app/en/platforms/mac/canvas

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
