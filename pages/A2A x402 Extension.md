# A2A x402 Extension

The **A2A x402 Extension** is an extension specification for the **Agent-to-Agent (A2A) protocol** that adds an on-chain payment handshake to A2A task execution. It standardizes how a service-providing ("merchant") agent can require payment, how a client agent submits a signed payment authorization, and how the merchant returns receipts once the payment is verified and/or settled. (Spec: v0.2) https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

## What it is (and is not)

* **It is an A2A extension**, declared in an agent’s `AgentCard` under `capabilities.extensions`, using a canonical extension URI for a particular version. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md
* **It is not the same thing as HTTP x402**, though it borrows the "402 Payment Required" idea and maps it into A2A task/message semantics.

## Core objects and fields

The extension defines (at minimum) these named objects and metadata keys (names as in the spec):

* `x402PaymentRequiredResponse`  the merchant’s description of acceptable payment options, including an `accepts` array of `PaymentRequirements`. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md
* `PaymentRequirements`  one concrete way to pay (e.g., scheme + network + asset + recipient + amount bounds). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md
* `PaymentPayload`  the client’s signed authorization corresponding to one selected `PaymentRequirements` option. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md

During the flow, A2A messages carry an `x402.payment.status` string plus additional x402 keys such as:

* `x402.payment.required` (merchant  client, in the standalone flow)
* `x402.payment.payload` (client  merchant)
* `x402.payment.receipts` (merchant  client)

(Standalone placement and flow detection are described in v0.2.) https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

## Flows

### Standalone flow (x402-only)

In the **standalone flow**, the merchant communicates payment requirements directly in the `Task` status message metadata, and the client replies with a signed payload:

1. **Merchant requires payment**: merchant returns a `Task` in `input-required` and sets `task.status.message.metadata["x402.payment.status"] = "payment-required"`. In the standalone flow, the merchant also includes `task.status.message.metadata["x402.payment.required"] = <x402PaymentRequiredResponse>`. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md
2. **Client submits payment authorization**: client chooses one `PaymentRequirements` option from `accepts`, has it signed by a wallet or signing service, and sends a message with `message.metadata["x402.payment.status"] = "payment-submitted"` and `message.metadata["x402.payment.payload"] = <PaymentPayload>`. (The spec examples also show correlating with the original `taskId`.) https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md
3. **Merchant verifies/settles and returns receipts**: merchant verifies and settles, and includes receipts under `x402.payment.receipts` while updating `x402.payment.status` (e.g., `payment-verified`, `payment-completed`). https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md

### Embedded (composable) flow

v0.2 also defines an **embedded flow**, where x402 objects are nested inside a higher-level commerce protocol (the spec calls out AP2 as an example). In this mode:

* the `x402PaymentRequiredResponse` is embedded in a higher-level object (e.g., in `task.artifacts`), rather than being present at `x402.payment.required` in metadata
* the `PaymentPayload` is embedded in a higher-level object (e.g., in `message.parts`)

The spec describes a detection rule: if `x402.payment.status == "payment-required"` and `x402.payment.required` is present, treat it as standalone; otherwise treat it as embedded and scan the task artifacts for the higher-level container. https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md

## Relationship to HTTP x402 (Coinbase)

The A2A x402 extension is conceptually related to the broader **x402** payments protocol for HTTP: a resource server can respond with **402 Payment Required** plus payment instructions, and the client can retry with a payment payload (e.g., via `PAYMENT-SIGNATURE`) that the server verifies and settles. https://github.com/coinbase/x402 https://docs.cdp.coinbase.com/x402/welcome

HTTP status code **402 (Payment Required)** is reserved for future use in the HTTP status code registry (i.e., it is defined but not standardized for a specific payment mechanism). RFC 9110 defines the status code and notes its reserved nature. https://datatracker.ietf.org/doc/html/rfc9110

## See also

* Agent2Agent (A2A) Protocol
* Agent Payments Protocol (AP2)
* x402

## References

* A2A Protocol: x402 Payments Extension v0.2 (spec): https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.2/spec.md
* A2A Protocol: x402 Payments Extension v0.1 (spec): https://raw.githubusercontent.com/google-agentic-commerce/a2a-x402/main/spec/v0.1/spec.md
* Coinbase x402 repository: https://github.com/coinbase/x402
* Coinbase Developer Docs  Welcome to x402: https://docs.cdp.coinbase.com/x402/welcome
* IETF RFC 9110  HTTP Semantics (status code registry, incl. 402): https://datatracker.ietf.org/doc/html/rfc9110
