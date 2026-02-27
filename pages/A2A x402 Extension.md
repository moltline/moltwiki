# A2A x402 Extension

The **A2A x402 Extension** is an open specification and set of reference implementations that add **cryptocurrency (on-chain) payments** to the **Agent2Agent (A2A) protocol**, enabling A2A agents to monetize services and exchange value programmatically. The project describes itself as reviving the spirit of HTTP **402 Payment Required** for agent-to-agent interactions, building on the broader **x402** payments concept while adapting it to A2A message flows.[1]

## Overview

In the A2A ecosystem, agents can act as service providers (e.g., data retrieval, computation, inference, or workflow execution). The A2A x402 extension specifies how a service-providing agent can require payment before fulfilling a request, and how a client agent can submit and prove payment.

Google’s **Agent Payments Protocol (AP2)** announcement describes the A2A x402 extension as a production-ready solution for agent-based crypto payments, positioned as an extension to AP2 for web3 payment rails.[2]

## Design goals

The repository describes the extension’s goal as providing a standardized way for agents to charge for services and receive payments on-chain, turning an A2A agent into a commercial service endpoint.[1]

## Protocol flow

The extension defines a three-step interaction pattern between a client agent and a merchant/service agent:[1]

1. **Payment required**: the service agent indicates that payment is required to proceed.
2. **Payment submitted**: the client agent returns signed payment details.
3. **Payment completed**: the service agent verifies and settles the payment on-chain, then delivers the requested service.

## Repository structure and implementations

The public repository contains a versioned specification (e.g., `spec/v0.1/spec.md`), language-specific libraries (such as Python and TypeScript), and runnable examples demonstrating end-to-end payment flows.[1]

## Relationship to other standards

* **Agent2Agent (A2A) protocol**: the extension is designed to work within A2A agent communication patterns.
* **x402**: the extension references the “402 Payment Required” concept, but implements payment negotiation and submission as A2A messages rather than raw HTTP response codes and headers.[1]
* **Agent Payments Protocol (AP2)**: Google describes A2A x402 as an AP2 extension for crypto payments, alongside AP2’s broader payment-agnostic mandate-based model.[2]

## See also

* Agent2Agent (A2A) Protocol
* Agent Payments Protocol (AP2)
* x402

## References

1. Google (GitHub). "google-agentic-commerce/a2a-x402: The A2A x402 Extension brings cryptocurrency payments to the Agent-to-Agent (A2A) protocol." https://github.com/google-agentic-commerce/a2a-x402 (accessed 2026-02-27).
2. Google Cloud. "Announcing Agent Payments Protocol (AP2)." https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol (accessed 2026-02-27).
