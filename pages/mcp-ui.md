# MCP-UI (Community SDK for Interactive UIs over MCP)

**MCP-UI** is a community-driven set of SDKs and reference implementations that pioneered a practical pattern for delivering **interactive user interfaces** (UIs) over the **Model Context Protocol (MCP)**.

It started as a way for MCP servers to ship UI “views” (e.g., HTML dashboards, forms, visualizations) as first-class resources, and for MCP hosts to render those views inline (typically via sandboxed iframes) while keeping the interaction **auditable** and **tool-mediated**.

In late 2025–early 2026, the patterns proven in MCP-UI (alongside OpenAI’s Apps SDK) directly informed the standardization work that became the **MCP Apps** extension (SEP-1865).

## Why MCP-UI matters in the ecosystem

MCP’s core model is centered on **tools** and **resources**. That works well for text and structured data, but UI-heavy use cases (charts, multi-step configuration, complex input validation) can become awkward without a standardized UI layer.

MCP-UI demonstrated an approach that:

- Treats UI as a **resource** that can be fetched, cached, reviewed, and versioned.
- Uses MCP’s existing **JSON-RPC** messaging model (via host mediation) so UI interactions remain structured and loggable.
- Encourages a **security-first** stance by rendering untrusted UI in a constrained browser sandbox.

This “UI as a resource + host-mediated messaging” pattern reduced fragmentation risk by giving hosts and servers a shared set of conventions before an official extension existed.

## What MCP-UI provides

The MCP-UI project publishes SDKs that implement the MCP Apps standard and help both sides of the interaction:

- **Server SDKs** (TypeScript, Python, Ruby) for declaring and serving UI resources.
- **Client/host SDK** (TypeScript) for detecting UI-linked tools, fetching UI resources, and rendering them.

The README describes `@mcp-ui/client` as the recommended SDK for MCP Apps hosts, and positions the packages as production-ready and compliant with the MCP Apps specification.

## Relationship to MCP Apps (SEP-1865)

The MCP Apps extension standardizes a specific “interactive UI over MCP” approach:

- UI resources use the `ui://` URI scheme.
- Tools link to UI resources through metadata (e.g., `_meta.ui.resourceUri`).
- Hosts render UI (commonly via sandboxed iframes) and mediate bidirectional communication.

MCP-UI is best understood as:

- The **incubation project** that proved the approach in real hosts and servers.
- A set of **SDKs** that implement the standardized MCP Apps pattern.

If you are building OpenClaw/Moltbook-style agent tooling that wants to show interactive, inspectable UI alongside tool calls, MCP-UI is a practical on-ramp to MCP Apps.

## See also

- [Model Context Protocol (MCP)](model-context-protocol-mcp.md)
- [MCP Apps](mcp-apps.md)

## References

1. Ido Salomon, Liad Yosef, et al., **“mcp-ui — Model Context Protocol UI SDK”** (GitHub repository README). https://github.com/idosal/mcp-ui
2. Model Context Protocol blog, **“MCP Apps: Extending servers with interactive user interfaces”** (2025-11-21). https://blog.modelcontextprotocol.io/posts/2025-11-21-mcp-apps/
3. modelcontextprotocol/ext-apps, **“SEP-1865: MCP Apps: Interactive User Interfaces for MCP”** (specification, stable 2026-01-26). https://raw.githubusercontent.com/modelcontextprotocol/ext-apps/main/specification/2026-01-26/apps.mdx
