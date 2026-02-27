# Agent Payments Protocol (AP2)

The **Agent Payments Protocol (AP2)** is an open protocol intended to support **agent-led payments**—payments initiated by software agents acting on behalf of a user—by providing a standardized way to communicate and verify an agent’s authority to transact. Google describes AP2 as an extension that can be used with the **Agent2Agent (A2A)** protocol and the **Model Context Protocol (MCP)**.

## Overview

Conventional online payments typically assume a human is directly authorizing a purchase (for example, by clicking a checkout button). AP2 is presented as addressing cases where an autonomous or semi-autonomous agent initiates or completes a transaction, by introducing protocol-level constructs meant to support authorization, authenticity of intent, and accountability in disputes.

AP2’s public documentation describes it as a non-proprietary protocol for interoperable “agent commerce”, with a design that emphasizes user control and privacy, and a cryptographic audit trail for transactions.

## Design

### Mandates and verifiable credentials

Google’s AP2 announcement describes AP2 as using **mandates**—cryptographically signed digital contracts—tied to verifiable credentials, to provide evidence of a user’s instructions across a transaction flow.

The AP2 documentation describes three primary mandate types:

- **Intent mandate**, representing the conditions under which an agent is authorized to act.
- **Cart mandate**, representing explicit authorization for a specific cart (items and price).
- **Payment mandate**, a separate object intended for payment networks and issuers to signal context such as agent involvement and user presence.

## Relationship to other agent protocols

Google’s product announcements and AP2 documentation position AP2 as compatible with, or an extension to, other protocols used in agent ecosystems:

- **Agent2Agent (A2A)**, for agent-to-agent interoperability.
- **Model Context Protocol (MCP)**, for connecting LLM applications to external tools and data.

## Availability

AP2 documentation and reference implementations are published in a public GitHub repository maintained under the **google-agentic-commerce** organization.

## References

1. Google Cloud Blog. “Announcing Agent Payments Protocol (AP2).” *Google Cloud Blog*. https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
2. AP2 Documentation. “AP2 – Agent Payments Protocol Documentation.” https://ap2-protocol.org/
3. Google Blog. “New tech and tools for retailers to succeed in an agentic shopping era.” *Google Blog* (Jan 11, 2026). https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
