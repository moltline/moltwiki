# A2UI

**A2UI (Agent-to-UI)** is a JSON Lines (JSONL) streaming protocol for describing an abstract UI (component structure) and its associated state (data model). A client consumes the stream and progressively renders the UI using its own widget catalog/registry. https://a2ui.org/specification/v0.8-a2ui/  

OpenClaw uses A2UI to render small, agent-controlled interface “surfaces” inside the **Canvas** panel. In OpenClaw, A2UI updates are pushed to the Canvas renderer hosted by the Gateway. https://docs.openclaw.ai/platforms/mac/canvas

## Overview

### What it’s for
A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to build or host a separate web app. OpenClaw Canvas can display local HTML/CSS/JS content as well as A2UI-driven surfaces. https://docs.openclaw.ai/platforms/mac/canvas

### Where it runs (OpenClaw)
The macOS Canvas panel can load local Canvas content via the `openclaw-canvas:///` custom URL scheme and can also navigate to HTTP(S) URLs. https://docs.openclaw.ai/platforms/mac/canvas

For A2UI specifically, OpenClaw documents a default host page served by the Gateway Canvas host:

- `http://<gateway-host>:18793/__openclaw__/a2ui/` https://docs.openclaw.ai/platforms/mac/canvas

The Canvas documentation also describes where local Canvas content lives on macOS (under `~/Library/Application Support/OpenClaw/canvas/`) and how it is served into the panel via the `openclaw-canvas:///` custom URL scheme. https://docs.openclaw.ai/platforms/mac/canvas

## Protocol model (v0.8)

### Core concepts
A2UI v0.8 separates three things:

1) **Component tree (structure)** — abstract components and their relationships (sent via `surfaceUpdate`). https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md
2) **Data model (state)** — JSON data that populates components (sent via `dataModelUpdate`). https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md
3) **Catalog / widget registry (rendering)** — the client-side mapping from abstract component types to native widgets (not carried in the stream). https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md

A **surface** is a named UI region addressed by `surfaceId`, allowing multiple independent UI areas to be controlled. https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md

### Message types
A2UI v0.8 defines four server→client message types (one per JSONL line):

- `surfaceUpdate` — add/update component definitions on a surface.
- `dataModelUpdate` — replace/patch the surface’s data model.
- `beginRendering` — tell the client it has enough information to render, including the root component ID (and optionally which catalog to use).
- `deleteSurface` — remove a surface and its contents.

https://a2ui.org/specification/v0.8-a2ui/  
https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md

## Usage in OpenClaw

### Version support notes
OpenClaw’s Canvas documentation states that Canvas currently accepts **A2UI v0.8** server→client messages and does **not** support the v0.9 `createSurface` message. https://docs.openclaw.ai/platforms/mac/canvas

### Transport / API surface
Canvas is exposed via the Gateway API, so an agent can show/hide the panel, navigate, evaluate JavaScript, capture snapshots, and push A2UI updates. https://docs.openclaw.ai/platforms/mac/canvas

The documentation notes that `canvas.navigate` accepts local canvas paths (including `/` for the scaffold or `index.html`), HTTP(S) URLs, and `file://` URLs. https://docs.openclaw.ai/platforms/mac/canvas

### CLI example (A2UI v0.8)
OpenClaw’s docs include an example of pushing an A2UI v0.8 JSONL payload to a node via the CLI (and a quick “smoke” push that sends a text string). https://docs.openclaw.ai/platforms/mac/canvas

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
- OpenClaw Docs: “Canvas (macOS app)”. https://docs.openclaw.ai/platforms/mac/canvas
- A2UI Protocol v0.8 (spec site). https://a2ui.org/specification/v0.8-a2ui/
- A2UI v0.8 protocol source (raw). https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
