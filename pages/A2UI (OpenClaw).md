# A2UI (OpenClaw)

**A2UI** (“agent-to-UI”) is a JSON message protocol used by OpenClaw to let an agent drive lightweight user interfaces in the OpenClaw **Canvas**. In OpenClaw’s macOS app, A2UI content is rendered inside the Canvas panel (a WKWebView-based visual workspace).

In current OpenClaw documentation, Canvas supports **A2UI v0.8** server→client messages (including `beginRendering`, `surfaceUpdate`, `dataModelUpdate`, and `deleteSurface`) and explicitly notes that **A2UI v0.9**’s `createSurface` is not supported.

## Overview

### What A2UI is for
A2UI is intended for presenting structured, UI-like output beyond plain chat text—such as small interactive surfaces, dashboards, or forms—within the Canvas.

### Where A2UI is hosted
OpenClaw hosts the A2UI page from the Gateway’s HTTP server. The Canvas panel can be navigated to the Gateway’s A2UI host path (by default under `__openclaw__/a2ui/`).

## Canvas integration (macOS)

OpenClaw’s macOS app embeds a resizable Canvas panel using WKWebView. The Canvas can render:

- local HTML/CSS/JS content
- A2UI surfaces
- small interactive UI surfaces

The documentation describes that when the Gateway advertises a Canvas host, the macOS app auto-navigates to the A2UI host page on first open.

## Protocol notes (as documented)

OpenClaw’s Canvas currently accepts **A2UI v0.8** messages from server to client:

- `beginRendering`
- `surfaceUpdate`
- `dataModelUpdate`
- `deleteSurface`

The docs also state:

- `createSurface` (A2UI v0.9) is not supported by Canvas.

## Developer workflow

### Pushing A2UI to a node Canvas
OpenClaw exposes Canvas and A2UI operations via its tool/CLI surface. The documentation shows a JSONL format used to push A2UI updates.

Example JSONL from the docs (abridged):

```jsonl
{"surfaceUpdate":{"surfaceId":"main","components":[{"id":"root","component":{"Column":{"children":{"explicitList":["title","content"]}}}}]}}
{"beginRendering":{"surfaceId":"main","root":"root"}}
```

## Related pages

- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)

## References

1. OpenClaw Docs, “Canvas (macOS app)” (A2UI section; v0.8 message types; default host URL). https://docs.openclaw.ai/platforms/mac/canvas
2. OpenClaw Docs, “Tools” (Canvas tool notes; A2UI v0.8 vs v0.9 mention). https://docs.openclaw.ai/tools

## External links

- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
