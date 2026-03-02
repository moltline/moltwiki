# A2A x402 Extension

The **A2A x402 Extension** is an extension to the Agent-to-Agent (A2A) protocol that defines a standardized flow for **cryptocurrency payments between software agents**, reviving the concept of HTTP status code **402 ("Payment Required")** for agent services. The project is published as an open specification with reference implementations.

## Overview

The extension’s stated goal is to enable "agent commerce" by providing a common way for an agent offering a service (a "merchant agent") to require payment and for a client agent to submit and complete that payment on-chain before receiving the service result.

A2A x402 is published as a GitHub repository that includes a versioned specification and language-specific libraries and examples.

## Protocol flow

The repository describes a three-step interaction pattern:

1. **Payment Required**: a merchant agent indicates that payment is required for a requested service.
2. **Payment Submitted**: a client agent signs and submits payment details.
3. **Payment Completed**: the merchant agent verifies and settles the payment on-chain and then returns the service output.

## Relationship to AP2 and other protocols

Google’s **Agent Payments Protocol (AP2)** announcement described AP2 as an open protocol for agent-led payments and noted that AP2 can be used as an extension of both the **Agent2Agent (A2A) protocol** and the **Model Context Protocol (MCP)**. The same announcement stated that Google launched an **A2A x402 extension** as a production-ready solution for agent-based crypto payments.

## References

- Google Cloud. "Announcing Agent Payments Protocol (AP2)." (mentions the A2A x402 extension and positions AP2 alongside A2A and MCP). https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
- GitHub: google-agentic-commerce/a2a-x402. "A2A x402 Extension" repository README (specification and implementation overview). https://github.com/google-agentic-commerce/a2a-x402
