# A2UI

**A2UI (Agent-to-UI)** is a streaming protocol where an agent sends a sequence of JSON messages (typically as JSON Lines / JSONL) that describe:

- an **abstract component structure** (what the UI is), and
- a **data model** (what values to render),

while the **client** is responsible for mapping abstract component types to concrete widgets via a **catalog** (a widget registry). This separation is a core design goal: the same agent output can be rendered by different clients (web, native, etc.) as long as they share a catalog mapping. https://a2ui.org/specification/v0.8-a2ui/

OpenClaw uses A2UI to render small, agent-controlled interface surfaces inside the **Canvas** panel; the agent pushes A2UI updates to the Gateway, and the Canvas panel renders them. https://docs.openclaw.ai/platforms/mac/canvas

## Overview

### What it’s for
A2UI lets an agent present information and lightweight interactions beyond plain chat text without requiring a bespoke web app. In OpenClaw, Canvas can display local HTML/CSS/JS content as well as A2UI-driven surfaces. https://docs.openclaw.ai/platforms/mac/canvas

### Where it runs (OpenClaw)
The macOS Canvas panel can load local Canvas content via the `openclaw-canvas:///` custom URL scheme, and can also navigate to HTTP(S) URLs. https://docs.openclaw.ai/platforms/mac/canvas

For A2UI specifically, OpenClaw documents a default host page served by the Gateway Canvas host:

- `http://<gateway-host>:18789/__openclaw__/a2ui/` https://docs.openclaw.ai/platforms/mac/canvas

(If you see older references with different ports/paths, prefer the Canvas docs.)

## Protocol model (v0.8, stable)

A2UI v0.8 is the current **stable** release and is recommended for production use. https://a2ui.org/specification/v0.8-a2ui/

### Core concepts
A2UI v0.8 separates three concerns:

1) **Component definitions (structure)** — a set of abstract components and their relationships.
2) **Data model (state)** — JSON data that components bind to.
3) **Catalog (rendering contract)** — the client-side mapping from abstract component types to native widgets (not carried in the stream).

This split is intentional: it enables progressive rendering and efficient updates (you can update data without resending all component definitions). https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md

A **surface** is a named UI region addressed by `surfaceId`, allowing multiple independent UI areas to be controlled. https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md

### Transport shape
Server → client messages are streamed as **one JSON object per line** (JSONL). Clients can process each message incrementally to improve perceived responsiveness. https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md

### Message types (server → client)
A2UI v0.8 defines four server→client message types:

- `surfaceUpdate` — add/update component definitions on a surface.
- `dataModelUpdate` — update the surface’s data model.
- `beginRendering` — signal the client to perform the initial render, including which component is the root.
- `deleteSurface` — remove a surface and its contents.

https://a2ui.org/specification/v0.8-a2ui/

## Protocol evolution (v0.9, draft)

A2UI v0.9 is published as a **draft** and changes the lifecycle and message names.

- It introduces `createSurface` and uses `updateComponents` / `updateDataModel` (instead of `beginRendering`, `surfaceUpdate`, `dataModelUpdate`). https://a2ui.org/specification/v0.9-a2ui/
- The evolution guide explicitly describes `beginRendering` being replaced by `createSurface`. https://a2ui.org/specification/v0.9-evolution-guide/

## Usage in OpenClaw

### Version support notes
OpenClaw’s Canvas documentation states that Canvas currently accepts **A2UI v0.8** server→client messages:

- `beginRendering`
- `surfaceUpdate`
- `dataModelUpdate`
- `deleteSurface`

…and that `createSurface` (v0.9) is not supported. https://docs.openclaw.ai/platforms/mac/canvas

### Transport / API surface
Canvas is exposed via the Gateway API, so an agent can show/hide the panel, navigate, evaluate JavaScript, capture snapshots, and push A2UI updates. https://docs.openclaw.ai/platforms/mac/canvas

The docs note that `canvas.navigate` accepts local canvas paths (including `/` for the scaffold or `index.html`), HTTP(S) URLs, and `file://` URLs. https://docs.openclaw.ai/platforms/mac/canvas

### CLI example (A2UI v0.8)
OpenClaw’s Canvas docs include an example of pushing an A2UI v0.8 JSONL payload to a node via the CLI (and a quick “smoke” push that sends a text string). https://docs.openclaw.ai/platforms/mac/canvas

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
- OpenClaw Docs: “Canvas (macOS app)”. https://docs.openclaw.ai/platforms/mac/canvas
- A2UI Protocol v0.8 (stable). https://a2ui.org/specification/v0.8-a2ui/
- A2UI Protocol v0.9 (draft). https://a2ui.org/specification/v0.9-a2ui/
- A2UI v0.8 protocol source (raw). https://raw.githubusercontent.com/google/A2UI/main/specification/v0_8/docs/a2ui_protocol.md
- A2UI Evolution Guide (v0.8 → v0.9). https://a2ui.org/specification/v0.9-evolution-guide/

## External links
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
