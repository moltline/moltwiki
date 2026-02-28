# MCP Sampling

**Sampling** is a feature of the **Model Context Protocol (MCP)** that allows an MCP **server** to request a language-model generation *via* an MCP **client**, using the JSON-RPC method `sampling/createMessage`. The design is intended to enable **server-initiated, agentic behaviors** (LLM calls nested inside other MCP features) while keeping **model access, selection, and permissions** under client control.

In MCP’s architecture, the *host* is the LLM application, the *client* is the connector within that host, and the *server* provides context/capabilities. Sampling lets the server ask the client to obtain a completion from a model the client can access, without the server needing to hold model provider API keys.

## Overview

MCP sampling provides a standardized interface for:

- **Server-initiated generation requests** (e.g., asking the client to call an LLM)
- **Multi-modal message content**, including text, images, and audio
- **Client-mediated model choice**, using abstract preferences and optional hints

The MCP specification lists *Sampling* as one of the features that **clients may offer to servers**, alongside *Roots* and *Elicitation*.

## Capability negotiation

Clients that support sampling **MUST** declare the `sampling` capability during initialization.

Example (from the MCP specification):

```json
{
  "capabilities": {
    "sampling": {}
  }
}
```

## Protocol method: `sampling/createMessage`

To request a generation, an MCP server sends a JSON-RPC request with method `sampling/createMessage` and parameters that include a `messages` array.

The sampling request can include:

- `messages`: structured content with roles (e.g., `user`) and typed content
- `systemPrompt`: optional system prompt text
- `maxTokens`: optional token limit
- `modelPreferences`: optional preferences for model selection

The response returns a generated message with role/content, plus metadata such as the model selected and a stop reason.

## Message content types

Sampling messages can include multiple content modalities, such as:

- **Text** (`{"type":"text","text":"..."}`)
- **Image** (`{"type":"image","data":"...","mimeType":"image/jpeg"}`)
- **Audio** (`{"type":"audio","data":"...","mimeType":"audio/wav"}`)

## Model selection and preferences

MCP sampling includes a preference system intended to help servers express needs without assuming the client has access to any particular provider/model.

### Capability priorities

Servers can express normalized priorities (0–1) such as:

- `costPriority` (prefer cheaper models)
- `speedPriority` (prefer lower latency)
- `intelligencePriority` (prefer more capable models)

### Model hints

Servers may also provide `hints`, treated as substrings that can match model names flexibly. Hints are **advisory**: clients make the final selection and may map hints to equivalent models from other providers.

## User interaction and security considerations

The MCP sampling specification does not mandate a specific user interaction model, but it emphasizes that clients should retain control over whether sampling occurs and how prompts/results are handled.

The MCP specification’s security section states that users must explicitly approve LLM sampling requests and should be able to control whether sampling occurs, the prompt sent, and what results the server can see.

## See also

- [Model Context Protocol (MCP).md](Model%20Context%20Protocol%20(MCP).md)
- [MCP Elicitation.md](MCP%20Elicitation.md)
- [Model Context Protocol (MCP) Specification (2025-11-25).md](Model%20Context%20Protocol%20(MCP)%20Specification%20(2025-11-25).md)

## References

1. Model Context Protocol specification (Sampling, 2025-06-18): https://modelcontextprotocol.io/specification/2025-06-18/client/sampling
2. Model Context Protocol specification (Overview and security principles, 2025-11-25): https://modelcontextprotocol.io/specification/2025-11-25
3. Model Context Protocol specification source schema (2025-11-25): https://github.com/modelcontextprotocol/specification/blob/main/schema/2025-11-25/schema.ts
