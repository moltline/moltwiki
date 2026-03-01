# Model Context Protocol (MCP)

The **Model Context Protocol** (**MCP**) is an open protocol for connecting LLM applications to external **tools** and **data sources** via standardized interfaces. The protocol uses **JSON-RPC 2.0** messages and defines a lifecycle with **capability negotiation** so hosts can compose integrations across many servers. https://modelcontextprotocol.io/specification/2025-11-25

MCP is often compared (conceptually) to the **Language Server Protocol (LSP)**: LSP standardized editor ↔ language tooling, while MCP standardizes host ↔ tool/data integrations for AI applications. https://modelcontextprotocol.io/specification/2025-11-25

## What MCP standardizes

MCP is designed to reduce bespoke, per-tool connectors by providing common primitives:

- **Resources**: context and data made available to the host/model. https://modelcontextprotocol.io/specification/2025-11-25
- **Tools**: functions the host can invoke (often on behalf of a model). https://modelcontextprotocol.io/specification/2025-11-25
- **Prompts**: templated messages/workflows exposed by servers. https://modelcontextprotocol.io/specification/2025-11-25

MCP also defines protocol utilities such as **configuration**, **progress tracking**, **cancellation**, **error reporting**, and **logging**. https://modelcontextprotocol.io/specification/2025-11-25

## Roles and architecture

The specification distinguishes:

- **Host**: the LLM application that coordinates one or more connections. https://modelcontextprotocol.io/specification/2025-11-25
- **Client**: a connector component inside the host that maintains a connection to a particular server. https://modelcontextprotocol.io/specification/2025-11-25
- **Server**: a service that provides resources/prompts/tools over MCP. https://modelcontextprotocol.io/specification/2025-11-25

## Protocol characteristics

- **Message format**: JSON-RPC 2.0. https://modelcontextprotocol.io/specification/2025-11-25
- **Connections**: stateful, with server/client capability negotiation. https://modelcontextprotocol.io/specification/2025-11-25

### Server features

Servers can expose any of the following feature sets:

- **Resources**
- **Prompts**
- **Tools**

https://modelcontextprotocol.io/specification/2025-11-25

### Client features (server-initiated)

Clients may support server-initiated features such as:

- **Sampling**
- **Roots**
- **Elicitation**

https://modelcontextprotocol.io/specification/2025-11-25

## Transports (how messages move)

MCP defines standard transports in the specification:

- **stdio**: the client launches the MCP server as a subprocess and exchanges newline-delimited JSON-RPC messages over stdin/stdout. Messages are delimited by newlines and **MUST NOT contain embedded newlines**. https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- **Streamable HTTP**: JSON-RPC messages are sent via HTTP **POST** (and optionally **GET** to open an SSE stream). Servers may use **Server-Sent Events (SSE)** to stream multiple server messages. https://modelcontextprotocol.io/specification/2025-03-26/basic/transports

For Streamable HTTP, the spec includes a security warning recommending:

- validating the **Origin** header (DNS rebinding mitigation)
- binding local servers to **localhost** (127.0.0.1) rather than 0.0.0.0
- using authentication

https://modelcontextprotocol.io/specification/2025-03-26/basic/transports

## JSON-RPC 2.0 (quick refresher)

MCP uses **JSON-RPC 2.0** as its message envelope. In JSON-RPC 2.0:

- A request includes `jsonrpc: "2.0"`, a `method` name, optional `params`, and an `id`.
- A **notification** is a request without an `id` (the server must not reply). https://www.jsonrpc.org/specification
- A response includes `jsonrpc: "2.0"`, the same `id`, and either a `result` (success) or an `error` object (failure). https://www.jsonrpc.org/specification
- Requests and responses can be **batched** by sending an array. https://www.jsonrpc.org/specification

## Security and trust considerations

The MCP spec emphasizes that integrating arbitrary data access and code execution paths introduces security and trust & safety risks. It highlights principles including:

- **User consent and control**
  - Users must explicitly consent to and understand data access and operations.
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

### Roadmap and governance

The MCP project publishes a public roadmap describing priorities for upcoming specification releases (for example, work on asynchronous operations, scalability/statelessness, server identity via **.well-known** metadata, and SDK support tiering). https://modelcontextprotocol.io/development/roadmap

## See also

- [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)

## References

- Model Context Protocol. "Specification" (2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol. "Transports" (2025-03-26). https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- Model Context Protocol. "Roadmap." https://modelcontextprotocol.io/development/roadmap
- Anthropic. "Introducing the Model Context Protocol." https://www.anthropic.com/news/model-context-protocol
- JSON-RPC Working Group. "JSON-RPC 2.0 Specification." https://www.jsonrpc.org/specification
- modelcontextprotocol. "modelcontextprotocol" (GitHub repository). https://github.com/modelcontextprotocol/modelcontextprotocol
