# Universal Commerce Protocol (UCP)

The **Universal Commerce Protocol (UCP)** is an open-source protocol developed by Google intended to standardize “agentic commerce” workflows—enabling AI agents and consumer interfaces to interact with merchants and payment providers through a shared set of primitives and discovery mechanisms.[^google-ucp-blog] UCP describes a standardized manifest published by businesses (e.g., at `/.well-known/ucp`) that allows agents to discover supported services, capabilities, endpoints, and payment configuration without bespoke, per-surface integrations.[^google-ucp-blog]

According to Google, UCP is designed to be compatible with the **Agent Payments Protocol (AP2)** and to support multiple integration/transport options, including APIs, the **Agent2Agent (A2A)** protocol, and the **Model Context Protocol (MCP)**.[^google-ucp-blog]

## Overview

### Goals
Google describes UCP as addressing integration complexity in commerce by providing a common language and capability model across consumer “surfaces” (such as conversational interfaces), merchant backends, and payment providers.[^google-ucp-blog] The protocol’s design emphasizes:

- **Standardized capability discovery** (via a well-known manifest) for dynamic feature and endpoint discovery.[^google-ucp-blog]
- **Extensibility** through capabilities and extensions that can augment core flows (e.g., discounts extending checkout).[^google-ucp-blog]
- **Interoperable payments** through a modular “payment handler” architecture separating payment instruments from processors/handlers.[^google-ucp-blog]

### Discovery manifest
In Google’s description, businesses publish a JSON manifest at `/.well-known/ucp` that enumerates services and capabilities (with versioning and schema/spec links), enabling agents to discover how to interact with the business programmatically.[^google-ucp-blog]

## Relationship to other agent ecosystem protocols
Google’s UCP write-up positions the protocol as interoperating with other emerging standards used in agentic systems, including:

- **Agent Payments Protocol (AP2)** for agent-mediated payments.[^google-ucp-blog]
- **Agent2Agent (A2A)** for agent-to-agent communication/transport.[^google-ucp-blog]
- **Model Context Protocol (MCP)** for tool/context integration patterns.[^google-ucp-blog]

## Development and availability
Google states that UCP is open-source and community-driven, and points developers to a GitHub organization/repository for building and contributing to the protocol and related SDKs and samples.[^google-ucp-blog]

## References

[^google-ucp-blog]: Amit Handa; Ashish Gupta. “Under the Hood: Universal Commerce Protocol (UCP).” *Google for Developers Blog*, Jan. 11, 2026. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ (accessed 2026-02-26).
