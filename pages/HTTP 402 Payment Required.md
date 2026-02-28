# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code whose semantics are intentionally **underspecified**: HTTP defines the label (“Payment Required”) but reserves the code for future use and does not standardize any interoperable payment challenge/response mechanism.

- RFC 9110 (HTTP Semantics) defines 402 as “reserved for future use”: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required
- IANA’s HTTP Status Code Registry lists 402 with a reference to RFC 9110: https://www.iana.org/assignments/http-status-codes
- MDN notes that 402 is reserved and that implementations vary: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

As a result, any system that uses `402` must define the payment interaction **at the application layer** (headers, payload schema, token/proof format, verification rules, and retry behavior).

## What 402 means (and does not mean)

### Standard meaning

- **Class:** 4xx (client error)
- **Reason phrase:** “Payment Required”
- **Normative behavior:** none beyond “reserved for future use” (no standard headers or body format are defined by HTTP itself). https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required

### What 402 does *not* provide

Unlike `401 Unauthorized`, which has a standardized challenge mechanism via `WWW-Authenticate`, `402` has **no** standardized equivalent payment challenge header in HTTP. Therefore, generic HTTP clients cannot “just handle” 402 without protocol-specific knowledge.

## Common application-layer patterns

Because the wire format is not standardized, services that return `402` typically document a custom contract. Common patterns include:

1) **Paywall / access requires payment**
   - Server returns `402` plus a body describing what to pay for and how to pay.
   - Client pays out-of-band or via a defined flow, then retries with a protocol-defined proof/token.

2) **Payment attempt failed**
   - Some APIs use `402` to indicate a payment method was declined/expired/etc., with details in a JSON body (provider-specific). https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

### Interoperability implications

If you are designing a protocol on top of `402`, you need to specify at minimum:

- **Discovery:** how the server conveys acceptable payment options (headers vs body, schema, versioning)
- **Proof:** what the client sends on retry (token, signed receipt, payment pointer, etc.)
- **Verification:** who verifies (origin server vs delegated verifier) and what constitutes success
- **Idempotency / replay:** retry rules and how to avoid double-charging

## Example: x402 (application-layer protocol)

One modern example is **x402**, which uses HTTP requests/responses and `402` to drive a payment-required → pay → retry loop.

- Project repository: https://github.com/coinbase/x402
- Coinbase developer documentation: https://docs.cdp.coinbase.com/x402/welcome

## See also

- [x402](/pages/x402.md)
- [Agent Payments Protocol (AP2)](/pages/Agent%20Payments%20Protocol%20(AP2).md)
- [Secure Payment Confirmation (W3C)](/pages/Secure%20Payment%20Confirmation%20(W3C).md)
