# MCP-UI

**MCP-UI** is a community project that explores adding **interactive user interfaces** to applications built on the **Model Context Protocol (MCP)**. It is discussed in the context of MCP’s broader effort to standardize how MCP servers can deliver UI resources that render inside compatible hosts.

## Overview

MCP-UI is commonly described as an experimental extension that builds on MCP’s resource model to allow MCP servers to provide UI components (for example, HTML content rendered in an iframe) and to support bidirectional communication between the embedded UI and the host.

The draft MCP Apps specification (SEP-1865) cites MCP-UI as a project that demonstrated the viability of MCP apps built on UI resources and that influenced the design of the standardization effort.

## Relationship to MCP Apps (SEP-1865)

The MCP Apps draft specification proposes an MCP extension (`io.modelcontextprotocol/ui`) for interactive UIs. It describes a standardized pattern for:

- Declaring UI resources using a `ui://` URI scheme
- Linking tools to UI resources via metadata
- Communicating between UI iframes and hosts using MCP’s JSON-RPC base protocol
- Applying a security model that includes iframe sandboxing and auditable communication

## Implementations and ecosystem

MCP-UI is referenced alongside other efforts to bring UI into MCP-enabled applications. The SEP-1865 draft also mentions OpenAI’s “Apps SDK” as another validation of demand for rich UI within conversational interfaces.

## See also

- [[MCP Apps]]
- [[Model Context Protocol (MCP)]]

## References

- Model Context Protocol (GitHub). *SEP-1865: MCP Apps: Interactive User Interfaces for MCP* (draft). https://raw.githubusercontent.com/modelcontextprotocol/ext-apps/main/specification/draft/apps.mdx
- MCP-UI. *Project site*. https://mcpui.dev/
- WorkOS. *MCP-UI: A Technical Overview of Interactive Agent Interfaces* (blog). https://workos.com/blog/mcp-ui-a-technical-deep-dive-into-interactive-agent-interfaces
