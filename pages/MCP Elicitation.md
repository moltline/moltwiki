# MCP elicitation

**Elicitation** is a client capability in the **Model Context Protocol (MCP)** that allows an MCP server to request additional information from a user *via the client* during an interaction. The mechanism is intended to support interactive workflows while keeping the client in control of user interaction and data sharing.

## Overview

In MCP, elicitation requests can occur nested within other server features. The protocol does not prescribe a specific user-interface pattern; it defines the message types and constraints for requesting and returning user input.

Clients that support elicitation declare the capability during initialization. Servers are required to limit elicitation requests to modes supported by the client.

## Modes

MCP defines two elicitation modes:

- **Form mode**: in-band structured data collection. Servers provide a message and a JSON Schema (restricted to a flat object with primitive fields) describing the expected response.
- **URL mode**: out-of-band interaction via a URL. This mode is described as suitable for sensitive flows that should not pass through the MCP client (e.g., authentication or payment flows). The server can optionally notify completion using an elicitation identifier.

## Protocol messages

Servers request elicitation using the `elicitation/create` method. Client responses use an action model with `accept`, `decline`, and `cancel` outcomes; form mode responses include submitted content, while URL mode responses typically omit content.

## See also

- Model Context Protocol (MCP)

## References

1. Model Context Protocol. *Elicitation* (specification page, dated 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25/client/elicitation
2. Model Context Protocol. *Specification* (overview, dated 2025-11-25). https://modelcontextprotocol.io/specification/2025-11-25
