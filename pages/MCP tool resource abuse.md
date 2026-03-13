# MCP tool resource abuse

**MCP tool resource abuse** refers to attempts—malicious or accidental—to consume excessive compute, bandwidth, storage, or third-party API quota via tool calls exposed through the Model Context Protocol (MCP). Resource abuse can manifest as oversized parameters (e.g., large radii, long time ranges, or extreme media duration), repeated calls, or requests that trigger expensive database queries or external fetches.

## Background

MCP is an open protocol for connecting large language models and agentic applications to external tools and services. Because tool invocations can translate into real-world resource consumption (server-side processing, upstream API calls, and data transfer), MCP deployments may require explicit controls to prevent denial of service, unexpected costs, and degraded quality of service.

## Abuse patterns

Resource abuse patterns vary by tool modality and schema, but may include:

- **Oversized request parameters**, such as large geographic search radii or long media durations.
- **High-frequency invocation**, including repeated calls that exceed rate limits or quotas.
- **Expensive query shapes**, including unbounded database queries or large result sets.
- **Cross-modality amplification**, where a single request triggers multiple downstream fetches (for example, metadata plus media retrieval).

## Mitigations

Common mitigations discussed for MCP deployments include:

- **Input validation and caps**, such as maximum radii, duration limits, pagination defaults, and bounded result sizes.
- **Rate limiting and quotas**, potentially per user, per agent identity, or per tool.
- **Policy enforcement gateways**, where tool calls are evaluated against centralized policies before execution.
- **Observability controls**, including logging and monitoring for anomalous usage patterns.

## Research

A 2025 ACSAC case study described cross-domain resource abuse risks across multiple tool modalities and evaluated policy enforcement by interposing a component into agent tool interactions, integrating with an Open Policy Agent (OPA) policy engine and a pluggable MCP gateway framework.

## References

- IBM Research. "Preventing Multimodal Cross-Domain Resource Abuse in MCP Tools" (ACSAC 2025). https://research.ibm.com/publications/preventing-multimodal-cross-domain-resource-abuse-in-mcp-tools
- CoSAI (OASIS). "Model Context Protocol (MCP) Security" (approved 8 January 2026). https://raw.githubusercontent.com/cosai-oasis/ws4-secure-design-agentic-systems/main/model-context-protocol-security.md
