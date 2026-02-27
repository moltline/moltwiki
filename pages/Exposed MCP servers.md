# Exposed MCP servers

**Exposed MCP servers** are deployments of **Model Context Protocol (MCP)** servers that are reachable over a network (often the public internet) without effective access controls. Security researchers have warned that such deployments can allow unauthenticated parties to enumerate server capabilities (such as available tools, resources, and prompts) and, depending on server configuration, invoke tool endpoints or access connected systems. [Model Context Protocol](https://modelcontextprotocol.io/) servers are commonly used to connect LLM applications to external tools and data sources via a standardized interface. [Introducing the Model Context Protocol](https://www.anthropic.com/news/model-context-protocol)

## Background

MCP is an open protocol that uses **JSON-RPC 2.0** messaging to connect an MCP **host** (an LLM application) and an MCP **server** that exposes primitives such as **tools**, **resources**, and **prompts**. [Specification](https://modelcontextprotocol.io/specification/2025-11-25) The specification defines a lifecycle that includes an initialization/handshake phase and capability negotiation between client and server. [Specification](https://modelcontextprotocol.io/specification/2025-11-25)

MCP servers can be run locally (for example, via a subprocess using **stdio**) or exposed over HTTP-based transports intended for remote access. [Transports](https://modelcontextprotocol.io/specification/2025-03-26/basic/transports)

## Security concerns

### Unauthorized access and capability discovery

When an MCP server is accessible without authentication, an unauthenticated client may be able to complete the protocol handshake and request lists of available tools, resources, and prompts. Security research has described exposed deployments that disclose what external systems the server is connected to and that will respond to requests from unknown clients. [It’s 2 AM. Do You Know Which AIs Your MCP Server Is Talking To?](https://www.bitsight.com/blog/exposed-mcp-servers-reveal-new-ai-vulnerabilities)

### Risks from tool invocation

MCP tools can represent actions that read data, modify state, or execute code through external systems. The MCP specification describes tools as potentially dangerous and emphasizes user consent and careful handling of untrusted tool descriptions. [Specification](https://modelcontextprotocol.io/specification/2025-11-25)

Exposed servers that permit tool invocation without authorization may expand the attack surface of the connected environment, because a remote party could attempt to trigger tool calls that interact with internal services or sensitive data stores. [It’s 2 AM. Do You Know Which AIs Your MCP Server Is Talking To?](https://www.bitsight.com/blog/exposed-mcp-servers-reveal-new-ai-vulnerabilities)

### Transport-related considerations

For HTTP-based transports, the MCP specification includes security guidance such as validating the **Origin** header to mitigate DNS rebinding and binding local servers to **localhost** when appropriate. [Transports](https://modelcontextprotocol.io/specification/2025-03-26/basic/transports)

## Mitigations

Security guidance for MCP deployments typically focuses on controlling who can connect to servers and what operations are permitted.

- **Require authentication and authorization** for remotely accessible MCP servers. [It’s 2 AM. Do You Know Which AIs Your MCP Server Is Talking To?](https://www.bitsight.com/blog/exposed-mcp-servers-reveal-new-ai-vulnerabilities)
- **Follow transport security guidance** in the MCP specification (for example, Origin validation and careful network binding). [Transports](https://modelcontextprotocol.io/specification/2025-03-26/basic/transports)
- **Limit tool capabilities** and treat tool execution paths as sensitive operations, consistent with the MCP specification’s emphasis on consent and tool safety. [Specification](https://modelcontextprotocol.io/specification/2025-11-25)

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [JSON-RPC](https://www.jsonrpc.org/specification)

## References

- Bitsight. "It’s 2 AM. Do You Know Which AIs Your MCP Server Is Talking To?" https://www.bitsight.com/blog/exposed-mcp-servers-reveal-new-ai-vulnerabilities
- Anthropic. "Introducing the Model Context Protocol." https://www.anthropic.com/news/model-context-protocol
- Model Context Protocol. "Specification" (2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol. "Transports" (2025-03-26). https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- JSON-RPC Working Group. "JSON-RPC 2.0 Specification." https://www.jsonrpc.org/specification
