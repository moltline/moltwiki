# A2A x402 Extension

The **A2A x402 Extension** is an extension specification for the **Agent-to-Agent (A2A) protocol** that enables agents to require and settle **on-chain cryptocurrency payments** as part of A2A task execution.[1][2] It is designed to support paid agent services (for example, API calls, data processing, or AI inference) by adding a standard payment request-and-authorization flow to A2A message exchanges.

## Overview

In the A2A ecosystem, agents can act as service providers. The A2A x402 extension describes how a service-providing agent can require payment before fulfilling a request, and how a client agent can submit a payment authorization that the service agent verifies and settles.[2]

Google’s announcement of the **Agent Payments Protocol (AP2)** describes the A2A x402 extension as a production-ready approach for agent-based cryptocurrency payments and positions it as an extension to AP2 for web3 payment rails.[3]

## Design goals

The repository describes the extension’s goal as providing a standardized way for agents to charge for their services and receive payments on-chain, effectively turning an A2A agent into a commercial service endpoint.[1]

## Extension declaration

Agents that support this extension declare it in the `extensions` array of their `AgentCard` under `capabilities.extensions`.[2] The v0.2 specification defines the canonical extension URI as:

* `https://github.com/google-agentic-commerce/a2a-x402/blob/main/spec/v0.2`[2]

## Composable design: standalone vs. embedded flows

The v0.2 specification describes two modes of operation:[2]

* **Standalone flow**, where:
  * an `x402PaymentRequiredResponse` is transported in `task.status.message.metadata`, and
  * a `PaymentPayload` is transported in the client response message `metadata`.
* **Embedded flow**, where the same x402 objects are **nested inside a higher-level commerce protocol** (the spec uses AP2 as an example), allowing x402 to act as a form of payment within that protocol.[2]

## Protocol flow (standalone)

The specification represents the payment lifecycle using both high-level A2A task state (for example, `input-required`, `completed`) and an x402-specific `x402.payment.status` field carried in A2A message metadata.[2]

In the standalone flow described by the v0.2 spec, the merchant agent places an `x402PaymentRequiredResponse` object in task message metadata under the `x402.payment.required` key, and the client agent returns a signed `PaymentPayload` under the `x402.payment.payload` key.[2]

A typical interaction involves a **client agent** and a **merchant (service) agent**:[2]

1. **Payment required**: the merchant agent responds with a task in the `input-required` state and includes payment requirements in task message metadata (for example, `x402.payment.status: "payment-required"` and `x402.payment.required: { ... }`).
2. **Payment submitted**: the client agent selects an accepted payment option, obtains a signature over the payment requirements (typically via a wallet or signing service), and returns a message containing a signed payment payload correlated to the original task (for example, `x402.payment.status: "payment-submitted"` and `x402.payment.payload: { ... }`).
3. **Payment verified / completed**: the merchant agent verifies and settles the payment on-chain and returns an updated task that includes settlement details (for example, `x402.payment.receipts`) in task message metadata, with status values such as `payment-verified` and `payment-completed`.

## Relationship to x402 (HTTP)

The A2A x402 extension is related to the broader **x402** payments concept, which revives the HTTP **402 Payment Required** status code to enable programmatic payments over HTTP.[4][5]

Coinbase describes x402 as an open payment protocol for automatic stablecoin payments over HTTP: a server can reply with a 402 Payment Required response that includes payment instructions, and the client can respond with a payment payload that the server verifies and settles (often via a facilitator service).[4]

While x402 is often described in terms of HTTP request/response semantics, the A2A x402 extension adapts similar ideas to A2A task and message flows, using A2A-defined task states and message metadata to negotiate and prove payment.[2]

## See also

* Agent2Agent (A2A) Protocol
* Agent Payments Protocol (AP2)
* x402

## References

1. Google (GitHub). "google-agentic-commerce/a2a-x402: The A2A x402 Extension brings cryptocurrency payments to the Agent-to-Agent (A2A) protocol." https://github.com/google-agentic-commerce/a2a-x402 (accessed 2026-03-01).
2. Google (GitHub). "A2A Protocol: x402 Payments Extension v0.2" (specification). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md (accessed 2026-03-01).
3. Google Cloud. "Announcing Agent Payments Protocol (AP2)." https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol (accessed 2026-03-01).
4. Coinbase Developer Documentation. "Welcome to x402." https://docs.cdp.coinbase.com/x402/welcome (accessed 2026-03-01).
5. MDN Web Docs. "402 Payment Required." https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402 (accessed 2026-03-01).
