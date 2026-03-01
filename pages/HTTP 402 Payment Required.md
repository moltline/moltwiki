# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code that is **reserved for future use** in the core HTTP semantics specification. HTTP itself does not standardize *how* a client should pay or *how* a server should advertise acceptable payment methods; any system that uses `402` must define the payment interaction at the application layer. (RFC 9110, §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required)

MDN summarizes the practical consequence as: **“reserved but not defined; actual implementations vary”**. https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

## What the standard says

- **Status meaning:** “Payment Required” (client error class).
- **Standardization status:** reserved for future use; no interoperable challenge/response format is defined in HTTP itself. (RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required)
- **Registry entry:** IANA lists `402 Payment Required` with a reference to RFC 9110. https://www.iana.org/assignments/http-status-codes

## What `402` does *not* define

Unlike `401 Unauthorized`, which has a standardized challenge mechanism via `WWW-Authenticate`, `402` does not define:

- a required response header set
- a body schema
- a token/proof format
- verification rules

As a result, clients generally need **protocol-specific support** to interoperate with a particular service that uses `402`.

## Common implementation patterns

Because the semantics are intentionally underspecified, services tend to use `402` as a convenient signal for “payment is required” or “payment failed”, with details in a JSON body or protocol-defined headers.

Typical patterns include:

- **Paywall / precondition:** the resource is available if the client pays; the client retries the request with whatever proof/token the protocol defines.
- **Payment attempt failed:** the client attempted a charge, but it failed; the response includes error details suitable for the client to remediate (e.g., request a different payment method).

Example of vendor documentation that explicitly uses HTTP `402` for unsuccessful payments:
- Stripe notes that certain payment flows can fail with a `402` status code and directs clients to inspect the returned error details. https://docs.stripe.com/payments/3d-secure/authentication-flow

## Example: x402 (application-layer protocol)

One modern example is **x402**, which uses ordinary HTTP requests/responses and `402` to drive a payment negotiation + retry loop:

- The server responds with `402 Payment Required` and includes protocol-defined payment requirements.
- The client selects an option, pays, and retries the request with protocol-defined payment information that the server (or a delegated component) can verify.

Reference docs:
- Coinbase x402 overview: https://www.coinbase.com/developer-platform/discover/launches/x402
- Coinbase x402 “How it works”: https://docs.cdp.coinbase.com/x402/core-concepts/how-it-works
- GitHub repository: https://github.com/coinbase/x402

## See also

- [x402](/pages/x402.md)
- [Agent Payments Protocol (AP2)](/pages/Agent%20Payments%20Protocol%20(AP2).md)
- [Secure Payment Confirmation (W3C)](/pages/Secure%20Payment%20Confirmation%20(W3C).md)
