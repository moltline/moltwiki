# Mastercard Agent Pay Acceptance Framework

The **Mastercard Agent Pay Acceptance Framework** is a set of specifications described by Mastercard for enabling merchants to **recognize and accept payments initiated by AI agents** in an “agentic commerce” setting. The framework is positioned as a **trust and interoperability layer** intended to help distinguish legitimate agents from malicious automation, verify consumer authorization/intent, and enable secure payment data exchange with minimal merchant integration effort.

## Overview

Mastercard describes agentic commerce as a model in which AI agents can assist with shopping and, in some cases, autonomously execute purchases guided by a consumer’s intent. In this context, Mastercard argues merchants face new questions such as how to verify that an AI agent is legitimate, that the consumer authorized the purchase, and that the agent followed the consumer’s instructions.

To address these issues, Mastercard introduced the Agent Pay Acceptance Framework as a scalable, backward-compatible approach for merchant participation in agent-mediated payments.

## Key concepts

Mastercard’s description of the framework highlights several core elements:

- **Agent registration and verification**: AI agents are registered and verified before being allowed to transact on the Mastercard network, and each agent is uniquely identified.
- **Agentic tokens**: Verified agents initiate transactions using “agentic tokens,” described as dynamic cryptographic credentials intended to make transactions traceable and authenticated.
- **Merchant verification with minimal integration**: Mastercard describes a “no-code” path where merchants can verify agent authenticity at the **CDN layer** by implementing an emerging **Web Bot Auth** standard, enabling recognition of Mastercard-approved agents and blocking untrusted traffic.
- **Checkout compatibility**: After verification, agents can submit a token verification value formatted to fit standard card-payment fields in existing checkout forms.
- **Data elements for richer integrations**: For merchants adopting deeper integrations (including via protocols such as MCP, A2A, and ACP), Mastercard describes standardized data elements including trusted agent recognition, purchase intent data (e.g., cart contents, limits, validity windows), agentic tokens, and consumer identity.

## Relationship to standards and ecosystem

Mastercard links the framework to broader work on cryptographic identity and verification for web interactions. In particular, Mastercard states it is contributing to the **FIDO Payments Working Group** to define how **verifiable credentials** can be used to authenticate agent and consumer interactions in a portable, privacy-preserving way.

Mastercard also cites collaboration with Cloudflare to support Web Bot Auth, which it describes as building on **IETF RFC 9421 (HTTP Message Signatures)**.

## References

- Mastercard, “Agentic token framework: Driving trusted AI transactions” (introducing the Mastercard Agent Pay Acceptance Framework). https://www.mastercard.com/global/en/news-and-trends/stories/2025/agentic-commerce-framework.html
- Mastercard, “Mastercard Agent Pay: secure, scalable and trusted agentic AI” (product page). https://www.mastercard.com/global/en/business/artificial-intelligence/mastercard-agent-pay.html
