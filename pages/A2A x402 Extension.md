# A2A x402 Extension

The **A2A x402 Extension** is an extension specification for the **Agent-to-Agent (A2A) protocol** that adds a standardized way for an agent to require and settle **on-chain cryptocurrency payments** as part of A2A task execution. It is designed to support paid agent services (for example, API calls, data processing, or AI inference) by defining payment request, authorization, and receipt objects carried inside A2A tasks and messages. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

## What it is (and what it is not)

* **It is** an A2A *extension* that defines payment-related data structures and a state machine for “payment required → payment submitted → verified/settled”. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md
* **It is not** the base A2A protocol itself; it relies on A2A concepts like **Task state** and message **metadata** to transport payment information.
* **It is distinct from** Coinbase’s HTTP-oriented x402 protocol (which uses HTTP 402 and headers). The A2A extension adapts similar “payment required” semantics to A2A task/message exchanges. https://docs.cdp.coinbase.com/x402/welcome

## Extension URI and declaration

The v0.2 spec defines the canonical extension URI as:

* `https://github.com/google-agentic-commerce/a2a-x402/blob/main/spec/v0.2` https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

Agents that support the extension declare it in the `capabilities.extensions` array of their A2A `AgentCard`, including whether the extension is required for interoperability. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

## Flows: standalone vs embedded (composable)

The v0.2 specification is explicitly **composable** and describes two modes of operation:

### Standalone flow

Used for direct monetization without a higher-level commerce protocol.

* The `x402PaymentRequiredResponse` is transported in `task.status.message.metadata`.
* The `PaymentPayload` is transported in `message.metadata`.

https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

### Embedded flow

Used when x402 acts as a “form of payment” embedded inside a higher-level protocol (the spec gives AP2 as an example).

* The `x402PaymentRequiredResponse` is embedded inside a higher-level artifact (for example, an AP2 `CartMandate`) located in the `task.artifacts` array.
* The `PaymentPayload` is embedded inside a higher-level object (for example, an AP2 `PaymentMandate`) located in the `message.parts` array.

https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

The v0.2 spec also describes **flow detection logic**: when a client sees `x402.payment.status: "payment-required"`, it checks for the presence of `x402.payment.required` in `task.status.message.metadata`; if present it is standalone, otherwise the client scans `task.artifacts` to locate the embedded higher-level object that contains the `x402PaymentRequiredResponse`. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

## Payment lifecycle (typical interaction)

The extension represents the payment lifecycle using both:

* high-level A2A task state (for example, `input-required`, `completed`), and
* a granular `x402.payment.status` field.

https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

A typical standalone interaction involves a **client agent** and a **merchant (service) agent**:

1. **Payment required**: the merchant responds with a task in the `input-required` state and includes payment requirements in task message metadata (for example `x402.payment.status: "payment-required"` and an `x402PaymentRequiredResponse` under `x402.payment.required`). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md
2. **Payment submitted**: the client selects an accepted payment option, obtains a signature over the payment requirements (typically via a wallet or signing service), and returns a message containing a signed `PaymentPayload` (for example `x402.payment.status: "payment-submitted"` and `x402.payment.payload`). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md
3. **Payment verified / completed**: the merchant verifies and settles the payment and returns an updated task including receipts (for example `x402.payment.receipts`) and a status such as `payment-verified` or `payment-completed`. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md

## Relationship to HTTP x402

Coinbase’s x402 protocol is described as an “open payment protocol” for programmatic stablecoin payments over HTTP, reviving the HTTP **402 Payment Required** status code and using a payment-required response followed by a client-supplied payment payload that the server verifies and settles. https://docs.cdp.coinbase.com/x402/welcome

While the transport differs (HTTP headers vs. A2A message/task fields), the A2A x402 extension draws on the same “payment required” concept and applies it to agent-to-agent task execution. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

## See also

* Agent2Agent (A2A) Protocol
* Agent Payments Protocol (AP2)
* x402

## References

* A2A Protocol: x402 Payments Extension v0.2 (spec). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md
* A2A Protocol: x402 Payments Extension v0.1 (spec). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md
* Coinbase Developer Documentation: “Welcome to x402”. https://docs.cdp.coinbase.com/x402/welcome
