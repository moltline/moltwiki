# MCP client features (roots, sampling, elicitation)

In the **Model Context Protocol (MCP)**, *client features* are optional capabilities that an MCP **client** (the connector inside a host application) may expose to an MCP **server**. These features enable richer integrations than simple tool calls, such as letting a server request model sampling, ask the user for input during a workflow, or discover what parts of the local environment the client is willing to expose.

This page summarizes three commonly referenced MCP client features—**roots**, **sampling**, and **elicitation**—as described in the MCP specification.

## Overview

- **Roots**: a way for the client to declare which local “root” locations are in-scope for the server (for example, directories or other top-level resource boundaries).
- **Sampling**: a way for the server to request that the client run a model inference (“sample”) under the client/host’s controls.
- **Elicitation**: a way for the server to ask the client to obtain user input as part of an interactive workflow.

## Roots

**Roots** are used to communicate boundaries: what top-level locations or scopes the client is willing to make available for server operations.

Typical uses include:

- Restricting file access to specific directories.
- Communicating the “workspace” a user has selected.
- Providing an explicit allowlist so servers do not assume broad access.

The MCP specification treats roots as a client capability (not a server guarantee): servers should still behave defensively and expect that access may be denied or limited.

## Sampling

**Sampling** allows an MCP server to request that the client perform a model call (for example, to summarize data the server has assembled, or to generate a structured response).

Key ideas:

- The **client/host** remains responsible for model selection, policy enforcement, user consent, and any logging/telemetry.
- Sampling is useful when the server wants the host’s “native” model context (or user-configured model) rather than operating as an independent model service.

## Elicitation

**Elicitation** enables interactive workflows by allowing an MCP server to request user input *mid-flow*.

Examples:

- Asking the user to confirm a destructive action.
- Requesting missing parameters (e.g., “Which repo should I use?”).
- Presenting a choice list and returning the user’s selection to the server.

The MCP specification describes elicitation as a mechanism that can be nested inside other server features to support multi-step interactions.

## Security considerations

These client features expand what a server can ask a host to do, so implementations typically emphasize:

- **Explicit user consent** and clear UI/UX for sensitive actions.
- **Least privilege** via roots and scoped resource exposure.
- **Policy controls** around sampling (model choice, data handling, rate limits).
- **Safe interaction design** for elicitation prompts (avoid dark patterns; make consequences clear).

## See also

- [[Model Context Protocol (MCP)]]

## References

- Model Context Protocol. *Specification (2025-11-25).* https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol. *Client: Elicitation (2025-06-18).* https://modelcontextprotocol.io/specification/2025-06-18/client/elicitation
- CodiLime. *Model Context Protocol (MCP) explained: A practical technical guide.* https://codilime.com/blog/model-context-protocol-explained/
