# MCP Sampling

**MCP Sampling** is a feature of the [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md) that lets an MCP server request a language-model generation through an MCP client.
In this pattern, the **client** retains control over model access (including selection, permissions, and user interaction), while the **server** can incorporate model outputs into its own tool or workflow logic.

## Overview

In MCP, a server can ask a client to create a model-generated message (a “completion” / “generation”).
This enables *agentic* behaviors where a server performs tool operations and, when needed, asks the client to obtain an LLM response without the server holding model-provider API keys.

The MCP specification frames sampling as:

- **Client-mediated model access**: the client chooses and authorizes model usage.
- **Nested calls**: sampling requests can occur inside other server features.
- **Multiple modalities**: requests may include text, image, or audio content.

## Protocol

### Capability declaration

Clients that support sampling declare the `sampling` capability during initialization.

### `sampling/createMessage`

To request a generation, the server sends a JSON-RPC request using the method `sampling/createMessage`.
The request includes a list of input messages and may include:

- `systemPrompt`
- `maxTokens`
- `modelPreferences` (see below)

The response returns the generated message content, the model identifier selected by the client, and a stop reason.

## Model selection

Because servers and clients may use different model providers or naming schemes, MCP defines a **preference system** rather than requiring an exact model name.

### Capability priorities

Servers can express normalized priorities (0–1) such as:

- `costPriority`
- `speedPriority`
- `intelligencePriority`

### Model hints

Servers can also provide ordered **hints** (substrings) suggesting preferred model families.
Hints are advisory; the client makes the final selection and may map hints to equivalent models from other providers.

## User interaction and safety

The MCP specification does not mandate a specific user interaction model for sampling.
It recommends that clients implement controls such as user approval and rate limiting, and that both parties handle sensitive data appropriately.

## See also

- [Model Context Protocol (MCP).md](Model%20Context%20Protocol%20(MCP).md)
- [Model Context Protocol (MCP) Specification (2025-11-25).md](Model%20Context%20Protocol%20(MCP)%20Specification%20(2025-11-25).md)
- [MCP tool poisoning attacks.md](MCP%20tool%20poisoning%20attacks.md)

## References

- Model Context Protocol specification — Sampling (client): https://modelcontextprotocol.io/specification/2025-06-18/client/sampling
