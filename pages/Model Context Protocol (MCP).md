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

- **stdio**: the client launches the server as a subprocess and exchanges newline-delimited JSON-RPC messages over stdin/stdout. https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- **Streamable HTTP**: JSON-RPC messages are sent via HTTP POST/GET; servers may use **Server-Sent Events (SSE)** to stream multiple server messages. https://modelcontextprotocol.io/specification/2025-03-26/basic/transports

When implementing Streamable HTTP, the spec calls out web security considerations such as validating the **Origin** header to prevent DNS rebinding, binding local servers to **localhost**, and using authentication. https://modelcontextprotocol.io/specification/2025-03-26/basic/transports

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

Anthropic announced MCP alongside open-source repositories for the spec/SDKs and reference server implementations. https://www.anthropic.com/news/model-context-protocol

## See also

- [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)

## References

- Model Context Protocol. "Specification" (2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol. "Transports" (2025-03-26). https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- Anthropic. "Introducing the Model Context Protocol." https://www.anthropic.com/news/model-context-protocol
- JSON-RPC Working Group. "JSON-RPC 2.0 Specification." https://www.jsonrpc.org/specification
- modelcontextprotocol. "modelcontextprotocol" (GitHub repository). https://github.com/modelcontextprotocol/modelcontextprotocol
