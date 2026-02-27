# A2A x402 extension

The **A2A x402 extension** is a specification and set of reference implementations that add cryptocurrency (on-chain) payments to the **Agent-to-Agent (A2A)** protocol. It is intended to let an agent offer paid services (for example, API calls, data processing, or AI inference) and require payment as part of an A2A interaction, echoing the idea behind HTTP **402 Payment Required** in a decentralized, agent-to-agent setting.[1]

The extension is developed in the open by Google’s *google-agentic-commerce* organization and is described as an extension that can be used alongside the **Agent Payments Protocol (AP2)** work.[2]

## Overview

### Purpose
The project’s stated goal is to “enable agent commerce” by providing a standardized flow for agents to charge for services and receive payments on-chain.[1]

### High-level flow
The repository describes a three-step message flow between agents:[1]

1. **Payment Required**: a merchant agent indicates that payment is required for a requested service.
2. **Payment Submitted**: the client agent submits signed payment details.
3. **Payment Completed**: the merchant verifies and settles the payment on-chain, then returns the service result.

### Repository structure
The upstream repository contains:[1]

- a versioned specification (e.g., `spec/v0.1/spec.md`)
- language-specific libraries (e.g., Python and TypeScript)
- examples and experimental payment schemes

## Relationship to other protocols

- **A2A protocol:** The x402 extension is designed as an extension to A2A, adding payment-related message types and verification/settlement steps.[1]
- **x402 (HTTP payments):** The repository frames the extension as reviving the spirit of HTTP 402 “Payment Required” for agents, but the extension operates within A2A message exchanges rather than HTTP request/response alone.[1]
- **AP2:** Google’s AP2 announcement describes “A2A x402” as an extension intended to accelerate support for agent-based crypto payments and as a production-ready solution in that area.[2]

## See also

- [[Agent2Agent (A2A) Protocol]]
- [[Agent Payments Protocol (AP2)]]
- [[x402]]

## References

1. Google Agentic Commerce. “A2A x402 Extension” (repository overview). https://github.com/google-agentic-commerce/a2a-x402 (accessed 2026-02-27).
2. Google Cloud Blog. “Announcing Agent Payments Protocol (AP2)” (mentions the A2A x402 extension). https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol (accessed 2026-02-27).
