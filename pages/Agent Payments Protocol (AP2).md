# Agent Payments Protocol (AP2)

**Agent Payments Protocol (AP2)** is an open protocol announced by Google for enabling AI agents to securely initiate and transact payments on behalf of users across platforms. In Google's description, AP2 is designed to provide a payment-agnostic framework for agent-led commerce, and it can be used as an extension alongside the **Agent2Agent (A2A) protocol** and the **Model Context Protocol (MCP)**.

## Overview

As described by Google, AP2 aims to address challenges that arise when autonomous or semi-autonomous agents initiate transactions, including:

- **Authorization**: demonstrating that a user granted an agent the authority to make a specific purchase.
- **Authenticity**: helping a merchant validate that an agent's request reflects user intent.
- **Accountability**: supporting auditability when disputes, fraud, or mistakes occur.

Google positions AP2 as a shared protocol intended to reduce fragmentation across agentic commerce implementations.

## Design concepts

### Mandates

Google's announcement describes AP2 as building trust using **mandates**: cryptographically signed digital artifacts intended to serve as tamper-evident proof of a user's instructions.

In the blog post, mandates are discussed in terms of capturing a chain of evidence from user intent to purchase details (for example, an "intent" step followed by a "cart" step), with the goal of producing an auditable record connecting what the user authorized to what was ultimately paid for.

### Verifiable digital credentials

In AP2 documentation, mandates are expressed as **verifiable digital credentials (VDCs)**: tamper-evident, cryptographically signed objects exchanged between roles in a transaction. The documentation describes three primary VDC types: an **Intent Mandate**, a **Cart Mandate**, and a **Payment Mandate**. 

## Documentation, specification, and samples

AP2 documentation is published at **ap2-protocol.org** and mirrored in the project’s GitHub repository. The repository also includes reference implementations and samples, including scenarios for **human-present** card payments and **human-present** payments via the **x402** protocol.

## Relationship to other protocols

Google's announcement describes AP2 as complementary to existing agent interoperability work, including:

- **Agent2Agent (A2A) protocol**
- **Model Context Protocol (MCP)**

The announcement also references an **A2A x402 extension** (related to HTTP-based payments) as an example of extending the protocol's constructs for cryptocurrency or stablecoin payment flows.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [x402](x402.md)
- [Verifiable Credentials (W3C)](Verifiable%20Credentials%20(W3C).md)

## References

1. Google Cloud. "Announcing Agent Payments Protocol (AP2)." https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol (accessed 2026-02-28).
2. AP2 Protocol. "AP2 - Agent Payments Protocol Documentation" (docs mirror of the GitHub repository). https://ap2-protocol.org/ (accessed 2026-02-28).
3. GitHub. "google-agentic-commerce/AP2" (repository; documentation and samples). https://github.com/google-agentic-commerce/AP2 (accessed 2026-02-28).
