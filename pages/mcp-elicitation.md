---
title: "MCP Elicitation"
description: "A Model Context Protocol (MCP) client capability that lets servers request additional user input during an interaction."
---

# MCP Elicitation

**Elicitation** is a capability in the **Model Context Protocol (MCP)** that allows an MCP server to request additional information from a user *through the client* during an ongoing interaction.

In MCP’s architecture, the **host application** (for example, a desktop assistant or IDE) instantiates an **MCP client** which communicates with an **MCP server**. When a server cannot proceed without more user-provided information, it can initiate an elicitation request; the client presents the request in its user interface and returns the user’s response to the server in a structured form. The MCP specification frames elicitation as a way to enable interactive workflows while keeping the client in control of user interactions and data sharing.

## Modes

The MCP elicitation draft specification describes two elicitation modes:

- **Form mode**: In-band collection of structured data via the MCP client, optionally validated against a restricted subset of JSON Schema.
- **URL mode**: Out-of-band interaction by directing the user to an external URL for sensitive interactions that should not pass through the MCP client (for example, authentication or payments).

Clients that support elicitation declare the capability during MCP initialization, and servers are required not to send elicitation requests for modes the client does not support.

## Protocol messages

Elicitation requests are initiated by the server with an `elicitation/create` request. The parameters include a human-readable message explaining why the interaction is needed, and (for form mode) a `requestedSchema` describing the expected response.

Elicitation responses use an action model with three outcomes:

- `accept` (user approved and submitted)
- `decline` (user explicitly declined)
- `cancel` (user dismissed without an explicit choice)

For URL mode, the draft specification also defines an optional completion notification (`notifications/elicitation/complete`) and an error code (`-32042`) that can be used to indicate an out-of-band URL elicitation is required before a request can be retried.

## Relationship to other MCP client features

MCP describes several **client-provided** features that enable richer server interactions, commonly presented alongside:

- **Roots** (communicating intended filesystem scope)
- **Sampling** (server-requested model completions routed through the client)

Elicitation complements these by providing a standardized mechanism for servers to gather missing user input during multi-step operations.

## Security and privacy considerations

The elicitation draft emphasizes that URL mode exists to support sensitive flows that must not pass through the MCP client. More broadly, MCP documentation describes elicitation as part of a client-mediated interaction model intended to preserve user consent and control.

## References

- Model Context Protocol. “Elicitation (draft client specification).” https://modelcontextprotocol.io/specification/draft/client/elicitation
- Model Context Protocol. “Understanding MCP clients (client concepts documentation).” https://modelcontextprotocol.io/docs/learn/client-concepts
- Anthropic. “Introducing the Model Context Protocol.” https://www.anthropic.com/news/model-context-protocol
