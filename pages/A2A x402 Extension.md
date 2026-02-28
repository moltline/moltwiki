# A2A x402 Extension

The **A2A x402 Extension** is an extension specification for the **Agent-to-Agent (A2A) protocol** that enables agents to require and settle **on-chain cryptocurrency payments** as part of A2A task execution. It is designed to support paid agent services (for example, API calls, data processing, or AI inference) by adding a standard payment request-and-authorization flow to A2A message exchanges.[1]

## Overview

In the A2A ecosystem, agents can act as service providers. The A2A x402 extension describes how a service-providing agent can require payment before fulfilling a request, and how a client agent can submit a payment authorization that the service agent verifies and settles.

Google’s announcement of the **Agent Payments Protocol (AP2)** describes the A2A x402 extension as a production-ready approach for agent-based cryptocurrency payments and positions it as an extension to AP2 for web3 payment rails.[2]

## Design goals

The extension is designed to let agents **monetize** A2A skills by requiring **on-chain cryptocurrency payment** before performing work, using a standardized request/authorization pattern that can be reused across implementations.[1][3]

## Composable design (standalone vs. embedded)

The specification is explicitly designed to be **composable**, supporting two modes:[4]

* **Standalone flow**: payment requirements and payload are transported directly in A2A message metadata.
* **Embedded flow**: the same x402 objects are embedded inside a higher-level commerce protocol (for example, AP2), allowing x402 to act as a “form of payment” within an atomic checkout flow.[4]

The v0.2 spec also describes how embedded flows can avoid extra user prompts via different signing models (for example, “atomic signing” in a human-present flow, delegated signing, or escrow-style designs).[4]

## Protocol flow

The specification represents the payment lifecycle using both high-level A2A task state (for example, `input-required`, `completed`) and a granular `x402.payment.status` field carried in A2A messages.[3][4]

In the **standalone** flow, the merchant agent places an `x402PaymentRequiredResponse` object in task message metadata under the `x402.payment.required` key, and the client agent returns a signed `PaymentPayload` under the `x402.payment.payload` key.[3][4]

A typical interaction involves a **client agent** and a **merchant (service) agent**:[3][4]

1. **Payment required**: the merchant agent responds with a task in the `input-required` state and includes payment requirements in task message metadata (for example, `x402.payment.status: "payment-required"` and `x402.payment.required: { ... }`).
2. **Payment submitted**: the client agent selects an accepted payment option, obtains a signature over the payment requirements (typically via a wallet or signing service), and returns a message containing a signed payment payload correlated to the original task (for example, `x402.payment.status: "payment-submitted"` and `x402.payment.payload: { ... }`).
3. **Payment verified / completed**: the merchant agent verifies and settles the payment on-chain and returns an updated task that includes settlement details (for example, `x402.payment.receipts`) in task message metadata, with status values such as `payment-verified` and `payment-completed`.

## Extension declaration

Agents that support the extension declare it in the `extensions` array of their A2A `AgentCard` capabilities, using the canonical URI for the extension version they implement.[3][4]

## Relationship to x402

The A2A x402 extension is related to the broader **x402** payments concept, which revives the HTTP **402 Payment Required** status code to enable programmatic payments over HTTP. Coinbase describes x402 as an open payment protocol for automatic stablecoin payments over HTTP, using a payment-required response followed by a client-supplied payment payload that the server verifies and settles.[4]

While x402 is often described in terms of HTTP request/response semantics, the A2A x402 extension adapts similar ideas to A2A task and message flows, using A2A-defined task states and message metadata to negotiate and prove payment.[3]

## See also

* Agent2Agent (A2A) Protocol
* Agent Payments Protocol (AP2)
* x402

## References

1. Google (GitHub). "google-agentic-commerce/a2a-x402: The A2A x402 Extension brings cryptocurrency payments to the Agent-to-Agent (A2A) protocol." https://github.com/google-agentic-commerce/a2a-x402 (accessed 2026-02-28).
2. Google Cloud. "Announcing Agent Payments Protocol (AP2)." https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol (accessed 2026-02-28).
3. Google (GitHub). "A2A Protocol: x402 Payments Extension v0.1" (specification). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md (accessed 2026-02-28).
4. Google (GitHub). "A2A Protocol: x402 Payments Extension v0.2" (specification). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md (accessed 2026-02-28).
5. Coinbase Developer Documentation. "Welcome to x402." https://docs.cdp.coinbase.com/x402/welcome (accessed 2026-02-28).
