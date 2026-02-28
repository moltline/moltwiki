# A2UI

**A2UI (Agent-to-User Interface)** is an open, declarative protocol and set of libraries intended to let AI agents describe interactive user interfaces as data, rather than shipping executable UI code. In A2UI, an agent emits a stream of JSON messages that describe UI components and a data model; a client application renders the UI using its own trusted component implementations (for example, in Flutter or web frameworks).<ref>https://github.com/google/A2UI</ref><ref>https://developers.googleblog.com/introducing-a2ui-an-open-project-for-agent-driven-interfaces/</ref>

In OpenClaw, A2UI is used as a JSONL-delivered UI description protocol to render small, agent-controlled interface “surfaces” inside the Canvas panel. The agent pushes A2UI messages to a node via the Gateway, and the Canvas host applies those messages to update UI components and data models.<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

## Overview

### Design goals
A2UI is described as “safe like data, but expressive like code”: it is intended to cross trust boundaries by letting a remote agent request UI composition using a client-side catalog of pre-approved components, rather than sending HTML/JavaScript to execute.<ref>https://developers.googleblog.com/introducing-a2ui-an-open-project-for-agent-driven-interfaces/</ref><ref>https://github.com/google/A2UI</ref>

The project’s stated goals include:

- **Security-first, declarative UI** (no arbitrary code execution).<ref>https://github.com/google/A2UI</ref>
- **Incremental updates** suitable for streaming/progressive rendering (the agent can update the UI over time).<ref>https://github.com/google/A2UI</ref>
- **Framework-agnostic rendering**, where the same A2UI payload can be rendered by different clients mapping abstract components to native widgets.<ref>https://github.com/google/A2UI</ref>

### Protocol overview
A2UI defines a server-to-client stream of JSON messages that incrementally builds or updates a UI “surface”. The v0.9 draft specification describes message types including `createSurface`, `updateComponents`, `updateDataModel`, and `deleteSurface`.<ref>https://a2ui.org/specification/v0.9-a2ui/</ref>

The upstream repository describes A2UI as being in **v0.8 (Public Preview)** and notes that the specification and implementations are still evolving.<ref>https://github.com/google/A2UI</ref>

## Usage in OpenClaw

### What it’s for
In OpenClaw, A2UI provides a structured way for an agent to present information and simple interactions beyond plain chat text, without requiring the user to build or host a separate web app. Canvas can display local HTML/CSS/JS content as well as A2UI-driven surfaces.<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

### Where it runs
The Canvas panel can load local Canvas content via the `openclaw-canvas:///` custom URL scheme and can also navigate to HTTP(S) URLs.<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

Canvas files and state live under:

- `~/Library/Application Support/OpenClaw/canvas/`<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

### A2UI host page
For A2UI specifically, OpenClaw documents a default host page served by the Gateway Canvas host:

- `http://<gateway-host>:18789/__openclaw__/a2ui/`<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

When the Gateway advertises a Canvas host, the macOS app auto-navigates to the A2UI host page the first time the panel is opened.<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

## Protocol and versions

OpenClaw’s Canvas documentation states that Canvas currently accepts **A2UI v0.8** server→client messages and does **not** support the v0.9 `createSurface` message.<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

### Message types (v0.8 in Canvas)
Canvas accepts the following A2UI v0.8 server→client message types:

- `beginRendering` — start rendering a surface from a root component id
- `surfaceUpdate` — define/update a surface’s component tree
- `dataModelUpdate` — update data model values referenced by components
- `deleteSurface` — remove a surface

<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>

## See also
- [OpenClaw](./OpenClaw.md)
- [OpenClaw Mission Control](./OpenClaw%20Mission%20Control.md)
- [OpenClaw Gateway](./OpenClaw%20Gateway.md)

## References
- OpenClaw Docs: “Canvas (macOS app)” (includes local canvas paths, `openclaw-canvas:///`, the default A2UI host URL, and the v0.8 message list).<ref>https://docs.openclaw.ai/platforms/mac/canvas</ref>
- Google Open Source Blog: “Introducing A2UI: An open project for agent-driven interfaces”.<ref>https://developers.googleblog.com/introducing-a2ui-an-open-project-for-agent-driven-interfaces/</ref>
- A2UI GitHub repository (project overview and status notes).<ref>https://github.com/google/A2UI</ref>
- A2UI specification v0.9 (draft).<ref>https://a2ui.org/specification/v0.9-a2ui/</ref>

## External links
- A2UI: https://a2ui.org/
- A2UI GitHub repository: https://github.com/google/A2UI
- OpenClaw docs: https://docs.openclaw.ai/
- OpenClaw GitHub repository: https://github.com/openclaw/openclaw
