# Model Context Protocol (MCP)

The **Model Context Protocol** (**MCP**) is an open protocol for connecting LLM applications to external **tools** and **data sources** via standardized interfaces. MCP uses **JSON-RPC 2.0** messages and a lifecycle with **capability negotiation** so that hosts can compose integrations across many servers (similar in spirit to how the Language Server Protocol standardized editor ↔ language tooling). https://modelcontextprotocol.io/specification/2025-11-25

## What MCP standardizes

MCP is designed to reduce bespoke, per-tool connectors by providing common primitives:

- **Resources**: context and data made available to the host/model. https://modelcontextprotocol.io/specification/2025-11-25
- **Tools**: functions the host can invoke (often on behalf of a model). https://modelcontextprotocol.io/specification/2025-11-25
- **Prompts**: templated messages/workflows exposed by servers. https://modelcontextprotocol.io/specification/2025-11-25

## Roles and architecture

The specification distinguishes:

- **Host**: the LLM application that coordinates one or more connections. https://modelcontextprotocol.io/specification/2025-11-25
- **Client**: a connector component inside the host that maintains a connection to a particular server. https://modelcontextprotocol.io/specification/2025-11-25
- **Server**: a service that provides resources/prompts/tools over MCP. https://modelcontextprotocol.io/specification/2025-11-25

## Protocol characteristics

- **Message format**: JSON-RPC 2.0. https://modelcontextprotocol.io/specification/2025-11-25
- **Connections**: stateful, with server/client capability negotiation. https://modelcontextprotocol.io/specification/2025-11-25
- **Feature sets**:
  - Servers may expose **resources**, **prompts**, and/or **tools**. https://modelcontextprotocol.io/specification/2025-11-25
  - Clients may support server-initiated features such as **sampling**, **roots**, and **elicitation**. https://modelcontextprotocol.io/specification/2025-11-25

### Transports (how messages move)

MCP defines standard transports in the specification:

- **stdio**: the client launches the MCP server as a subprocess and exchanges newline-delimited JSON-RPC messages over stdin/stdout (messages MUST NOT contain embedded newlines). https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- **Streamable HTTP**: JSON-RPC messages are sent via HTTP POST/GET; servers may optionally use **Server-Sent Events (SSE)** to stream multiple server messages. https://modelcontextprotocol.io/specification/2025-03-26/basic/transports

For Streamable HTTP, the spec includes a security warning recommending validation of the **Origin** header (to mitigate DNS rebinding), binding local servers to **localhost**, and using authentication. https://modelcontextprotocol.io/specification/2025-03-26/basic/transports

## Security and trust considerations

The MCP spec emphasizes that integrating arbitrary data access and code execution paths introduces security and trust & safety risks. It highlights principles including:

- **User consent and control**
  - Users must explicitly consent to data access and operations.
  - Hosts must obtain explicit user consent before invoking any tool. https://modelcontextprotocol.io/specification/2025-11-25
- **Data privacy**
  - Hosts must obtain explicit user consent before exposing user data to servers.
  - Hosts must not transmit resource data elsewhere without user consent. https://modelcontextprotocol.io/specification/2025-11-25
- **Tool safety**
  - Tools represent arbitrary code execution and should be treated with appropriate caution.
  - Tool descriptions/annotations should be considered untrusted unless obtained from a trusted server. https://modelcontextprotocol.io/specification/2025-11-25
- **LLM sampling controls**
  - Users must explicitly approve sampling requests and control what prompt is sent and what results the server can see. https://modelcontextprotocol.io/specification/2025-11-25

## Ecosystem

Anthropic announced MCP alongside open-source repositories for the specification, SDKs, and reference server implementations. https://www.anthropic.com/news/model-context-protocol

### Official extensions

The MCP project has introduced **official protocol extensions** for common patterns that sit on top of the core protocol. One published example is **MCP Apps**, described as an extension that lets tools return interactive UI components that render in the host application (for example, dashboards and forms), with a sandboxing model based on iframes and JSON-RPC messaging. http://blog.modelcontextprotocol.io/posts/2026-01-26-mcp-apps/

### Roadmap and governance

The MCP project publishes a public roadmap describing priorities for upcoming specification releases (for example, work on asynchronous operations, scalability, server identity via .well-known metadata, and SDK support tiering). https://modelcontextprotocol.io/development/roadmap

## See also

- [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)

## References

- Model Context Protocol. "Specification" (2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol. "Transports" (2025-03-26). https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- Model Context Protocol. "Roadmap." https://modelcontextprotocol.io/development/roadmap
- Model Context Protocol Blog. "MCP Apps - Bringing UI Capabilities To MCP Clients" (2026-01-26). http://blog.modelcontextprotocol.io/posts/2026-01-26-mcp-apps/
- Anthropic. "Introducing the Model Context Protocol." https://www.anthropic.com/news/model-context-protocol
- JSON-RPC Working Group. "JSON-RPC 2.0 Specification." https://www.jsonrpc.org/specification
- modelcontextprotocol. "modelcontextprotocol" (GitHub repository). https://github.com/modelcontextprotocol/modelcontextprotocol
