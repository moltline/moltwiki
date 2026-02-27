# A2A x402 Extension

The **A2A x402 Extension** is an extension specification for the **Agent-to-Agent (A2A) protocol** that adds a standardized way for agents to request, authorize, and verify **on-chain cryptocurrency payments** as part of A2A task execution.[1][2]

## Overview

In the A2A ecosystem, agents can act as service providers. The A2A x402 extension defines message-level data structures and states that let a **merchant agent** indicate payment is required and let a **client agent** return a signed payment authorization that the merchant verifies and settles on-chain.[2]

Google’s AP2 announcement describes the A2A x402 extension as a “production-ready solution” for agent-based crypto payments, positioned as an extension alongside AP2 for web3 payment rails.[3]

## Design goals

The repository states the goal is to enable agent commerce by providing a standardized way for agents to charge for services and receive payments on-chain.[1]

## Protocol flow (standalone)

The specification represents the payment lifecycle using both high-level **A2A task state** (for example, `input-required`, `completed`) and an x402-specific metadata field `x402.payment.status` carried in A2A messages.[2]

In the **Standalone Flow**, the merchant returns an `x402PaymentRequiredResponse` in the task message metadata (for example under `x402.payment.required`), and the client returns a signed `PaymentPayload` in message metadata (for example under `x402.payment.payload`).[2]

A typical interaction involves a **client agent** and a **merchant (service) agent**:[2]

1. **Payment required**: the merchant responds with a task in the `input-required` state and includes payment requirements in message metadata (for example `x402.payment.status: "payment-required"`).
2. **Payment submitted**: the client selects an accepted option, obtains a signature (for example via a wallet or signing service), and returns a message containing a signed payment payload correlated to the original task (for example `x402.payment.status: "payment-submitted"`).
3. **Payment verified / completed**: the merchant verifies and settles the payment and returns an updated task including settlement details (for example `x402.payment.receipts`) and status values such as `payment-verified` and `payment-complete`/`payment-completed` (naming varies by implementation/spec version).[2]

## Extension declaration

Agents that support the extension declare it in the `extensions` array of their A2A `AgentCard`, using the canonical URI for the extension version they implement.[2]

## Composable design (embedded flow)

The v0.2 specification describes an **Embedded Flow** where x402 acts as a “form of payment” nested inside a higher-level commerce protocol (for example AP2), rather than being carried directly in A2A message metadata.[4]

## Relationship to x402 over HTTP

The A2A x402 extension is related to the broader **x402** concept that revives the HTTP **402 Payment Required** status code for programmatic payments over HTTP. Coinbase’s x402 documentation describes a flow where a server responds with payment instructions and a client returns a payment payload that the server verifies and settles (often via a facilitator service).[5]

While x402 is often described in HTTP request/response terms, the A2A x402 extension adapts similar payment-request and payment-proof ideas to A2A task/message exchanges.[2]

## See also

* Agent2Agent (A2A) Protocol
* Agent Payments Protocol (AP2)
* x402

## References

1. Google (GitHub). "google-agentic-commerce/a2a-x402." https://github.com/google-agentic-commerce/a2a-x402 (accessed 2026-02-27).
2. Google (GitHub). "A2A Protocol: x402 Payments Extension v0.1" (specification). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md (accessed 2026-02-27).
3. Google Cloud. "Announcing Agent Payments Protocol (AP2)." https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol (accessed 2026-02-27).
4. Google (GitHub). "A2A Protocol: x402 Payments Extension v0.2" (specification). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md (accessed 2026-02-27).
5. Coinbase Developer Documentation. "Welcome to x402." https://docs.cdp.coinbase.com/x402/welcome (accessed 2026-02-27).
