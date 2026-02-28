# A2A x402 Extension

The **A2A x402 Extension** is an extension specification for the **Agent-to-Agent (A2A) protocol** that adds a standardized way for agents to request, authorize, verify, and (when applicable) settle payments as part of A2A task execution. It is intended to support paid agent services (for example, API calls, data processing, or AI inference) by defining a payment-required handshake carried in A2A task/message metadata. [1] [3]

## What it is (and what it is not)

- **What it is:** an **A2A protocol extension** that defines **message metadata fields** and **task-state transitions** for a payment lifecycle (e.g., “payment required” → “payment submitted” → “verified/settled”). [3]
- **What it is not:** the underlying payment rail. The extension describes how payment requirements and proofs are communicated inside A2A; the actual payment scheme/network and settlement mechanics are defined by the x402 concepts and the extension spec’s required/payload structures. [3]

## Overview

In the A2A ecosystem, agents can act as service providers. The A2A x402 extension describes how a service-providing agent can require payment before fulfilling a request, and how a client agent can submit a payment authorization that the service agent verifies (and may settle) before completing the task. [3]

Google’s announcement of the **Agent Payments Protocol (AP2)** positions the A2A x402 extension as a production-ready approach for agent-based payments and frames it as an extension to AP2 for “web3” payment rails. [2]

## Design goals

The extension repository describes the goal as providing a standardized way for agents to charge for services and receive payments, effectively turning an A2A agent into a commercial service endpoint. [1]

## Protocol flow (A2A task + metadata)

The specification defines a payment lifecycle represented using both:

- **A2A task state** (for example, `input-required`, `completed`), and
- **x402-specific metadata fields** (for example, `x402.payment.status`) carried in A2A messages. [3]

In the standalone flow described by the specification:

- the merchant/service agent includes an `x402PaymentRequiredResponse` object in task message metadata under `x402.payment.required`, and
- the client agent responds with a signed `PaymentPayload` under `x402.payment.payload`. [3]

A typical interaction involves a **client agent** and a **merchant (service) agent**: [3]

1. **Payment required**: the merchant responds with a task in an `input-required`-style state and includes payment requirements in metadata (for example, `x402.payment.status: "payment-required"` and `x402.payment.required: { ... }`).
2. **Payment submitted**: the client selects an accepted payment option, obtains a signature over the payment requirements (typically via a wallet or signing service), and returns a message containing a signed payment payload correlated to the original task (for example, `x402.payment.status: "payment-submitted"` and `x402.payment.payload: { ... }`).
3. **Verified / completed**: the merchant verifies the payment and returns an updated task, optionally including receipts/settlement details (for example, `x402.payment.receipts`) with status values such as `payment-verified` and `payment-completed`. [3]

## Extension declaration

Agents that support the extension declare it in the `extensions` array of their A2A `AgentCard` capabilities, using the canonical URI for the extension version they implement. [3]

## Relationship to x402 (HTTP 402)

The A2A x402 extension is related to the broader **x402** payments concept, which uses the HTTP **402 Payment Required** status code to enable programmatic payments over HTTP.

In the x402 HTTP flow described by the Coinbase x402 repository and documentation:

- a client requests a resource,
- the server can respond with **402 Payment Required** and include payment instructions (e.g., in a `PAYMENT-REQUIRED` header),
- the client constructs a **PaymentPayload** and re-requests with a payment authorization/signature header (e.g., `PAYMENT-SIGNATURE`), and
- the server verifies and (directly or via a **facilitator**) settles the payment before returning the resource (optionally with a payment response header). [5] [6]

While x402 is often described in terms of HTTP request/response semantics, the A2A x402 extension adapts the same “payment required → payment proof → verification/settlement” idea to **A2A task/message exchanges**, using A2A-defined task states and message metadata rather than raw HTTP responses. [3]

## See also

* Agent2Agent (A2A) Protocol
* Agent Payments Protocol (AP2)
* x402

## References

1. Google (GitHub). "google-agentic-commerce/a2a-x402: The A2A x402 Extension brings cryptocurrency payments to the Agent-to-Agent (A2A) protocol." https://github.com/google-agentic-commerce/a2a-x402 (accessed 2026-02-27).
2. Google Cloud. "Announcing Agent Payments Protocol (AP2)." https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol (accessed 2026-02-27).
3. Google (GitHub). "A2A Protocol: x402 Payments Extension v0.2" (specification). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md (accessed 2026-02-27).
4. Mozilla Developer Network (MDN). "HTTP response status code 402 Payment Required." https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402 (accessed 2026-02-28).
5. Coinbase (GitHub). "coinbase/x402: A payments protocol for the internet. Built on HTTP." https://github.com/coinbase/x402 (accessed 2026-02-28).
6. Coinbase Developer Documentation. "Welcome to x402." https://docs.cdp.coinbase.com/x402/welcome (accessed 2026-02-28).
