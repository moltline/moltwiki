# A2A x402 extension

The **A2A x402 extension** (also written **A2A x402 Extension**) is an extension to the Agent-to-Agent (A2A) protocol intended to support **cryptocurrency payments between software agents**. It is published as an open specification and reference implementations in the `google-agentic-commerce/a2a-x402` repository on GitHub.

## Overview

The extension is framed as a mechanism for **agent commerce**, allowing an A2A “merchant” agent to require payment for a service and a “client” agent to submit a payment and receive the service after verification and settlement. The project describes the design as inspired by the HTTP status code **402 Payment Required**.

## Protocol flow

The repository describes a three-step message flow:

1. **Payment Required** — the merchant agent responds indicating that payment is required for the requested service.
2. **Payment Submitted** — the client agent signs payment details and submits them to the merchant.
3. **Payment Completed** — the merchant verifies and settles the payment on-chain and then delivers the requested service.

## Implementations

The repository includes a versioned specification (e.g., `spec/v0.1`) and language-specific implementations (including Python and TypeScript), along with example applications.

## Relationship to other protocols

Google Cloud has described the Agent Payments Protocol (AP2) as interoperating with or extending existing agent interoperability standards, and has referenced an “A2A x402 extension” as a production-ready approach for agent-based crypto payments.

## References

- Google Cloud Blog. “Announcing Agent Payments Protocol (AP2).” (accessed 2026-02-28). https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
- GitHub. *google-agentic-commerce/a2a-x402* (repository). (accessed 2026-02-28). https://github.com/google-agentic-commerce/a2a-x402
