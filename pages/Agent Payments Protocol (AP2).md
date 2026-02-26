# Agent Payments Protocol (AP2)

The **Agent Payments Protocol** (**AP2**) is an open protocol intended to enable AI agents to initiate and complete payments on behalf of users in a way that preserves user authorization, merchant trust, and an auditable record of intent. AP2 was announced by Google as an extension that can be used alongside the **Agent2Agent (A2A)** protocol and the **Model Context Protocol (MCP)** to support interoperable “agentic commerce” across platforms.\[1\]\[2\]

**Type:** Open protocol (agent-led payments)  
**Status:** Active (specification and reference implementations published)  
**Website:** https://ap2-protocol.org/  
**Repository:** https://github.com/google-agentic-commerce/AP2  
**Related protocols:** Agent2Agent (A2A), Model Context Protocol (MCP)\[1\]\[2\]

## Background

Traditional online payments typically assume a human is directly reviewing and approving a purchase (“clicking buy”) on a trusted interface. In agent-led purchasing, an autonomous or semi-autonomous agent may assemble carts, select merchants, and submit payment requests, which raises questions about (1) whether the user actually authorized the purchase, (2) whether the request accurately reflects the user’s intent, and (3) how disputes and accountability should work when an agent is involved.\[1\]\[2\]

## Design goals

AP2 is described as aiming to provide a **payment-agnostic** framework for agent-led commerce while supporting interoperability across merchants, agent platforms, and payment providers.\[1\] The AP2 documentation emphasizes goals including user control, privacy, and creating a cryptographic audit trail that can support dispute resolution.\[2\]

## Core concepts

### Mandates and verifiable credentials

AP2’s public materials describe a trust model based on **mandates**—cryptographically signed digital objects that represent user instructions and authorizations.\[1\]\[2\] The AP2 documentation refers to these objects as **verifiable digital credentials (VDCs)** and describes several mandate types, including:\[2\]

- **Intent mandate:** captures conditions under which an agent is authorized to shop or purchase, particularly for “human-not-present” delegated tasks.\[2\]
- **Cart mandate:** captures the user’s explicit authorization for a specific cart (items and price), particularly for “human-present” approvals.\[1\]\[2\]
- **Payment mandate:** an object intended for the payment network/issuer to signal agent involvement and transaction context.\[2\]

### Human-present and human-not-present flows

AP2’s announcement and documentation distinguish between:

- **Human-present** flows, where a user reviews and approves a cart assembled by an agent before payment.\[1\]\[2\]
- **Human-not-present** flows, where a user delegates a task with constraints (for example, price limits or timing) and the agent executes when conditions are met.\[1\]\[2\]

## Relationship to other protocols

AP2 is positioned as complementary to:

- **Agent2Agent (A2A):** a protocol for agent-to-agent communication and coordination.\[1\]\[2\]
- **Model Context Protocol (MCP):** a protocol for connecting AI applications to external tools and data sources.\[1\]\[2\]

## Implementations and ecosystem

Google’s announcement describes AP2 as being developed with participation from payments and technology companies and published with documentation and reference implementations in a public GitHub repository.\[1\]\[2\]

## See also

- [Model Context Protocol (MCP)](./Model%20Context%20Protocol%20(MCP).md)
- [ERC-8004 (Trustless Agents)](./ERC-8004%20(Trustless%20Agents).md)

## References

1. Google Cloud Blog. “Announcing Agent Payments Protocol (AP2).” https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
2. AP2 Protocol Documentation. “AP2 - Agent Payments Protocol Documentation.” https://ap2-protocol.org/

## External links

- AP2 GitHub repository: https://github.com/google-agentic-commerce/AP2
- Agent2Agent (A2A) protocol website: https://a2a-protocol.org/
- Model Context Protocol (MCP) website: https://modelcontextprotocol.io/
