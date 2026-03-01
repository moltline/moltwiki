# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code defined by the IETF as **reserved for future use**. HTTP itself does not standardize *how* a client should pay or *how* a server should describe acceptable payment methods; systems that use `402` must define the payment interaction at the application layer. (RFC 9110, §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required)

Because the semantics are intentionally underspecified, `402` is mostly used by APIs and custom protocols as a convenient signal for “you need to pay (or your payment failed) before you can access this resource”. MDN summarizes this as: “reserved but not defined; actual implementations vary”. (MDN: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402)

## What the standard says

- **Status meaning:** “Payment Required” (client error class).
- **Standardization status:** reserved for future use; no interoperable challenge/response format is defined in HTTP itself. (RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required)
- **Registry entry:** IANA lists `402 Payment Required` with a reference to RFC 9110. (IANA HTTP Status Code Registry: https://www.iana.org/assignments/http-status-codes)

## Practical use patterns

Since there is no standard “payment challenge” equivalent to `WWW-Authenticate` for `401`, implementations typically choose their own approach.

Common patterns include:

- **Paywall / payment required:** the response indicates the resource is available if the client pays, and the client retries the request with whatever proof/token the protocol defines.
- **Payment attempt failed:** some payment APIs return `402` as a generic error for a failed payment request, with details in the response body (e.g., an error code like `expired_card`). (MDN example: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402#payment_api_failure)
- **Provider-specific meaning:** some APIs document `402` under a different label than “Payment Required”. For example, Stripe’s API error reference describes `402` as “Request Failed” (“The parameters were valid but the request failed”). (Stripe API errors: https://docs.stripe.com/api/errors)

### Interoperability implications

Because `402` does not define headers, payloads, or verification rules, clients generally need **protocol-specific support** (headers, token formats, signing rules, etc.) to interoperate with a given service.

## Example: x402 (application-layer protocol)

One modern example is **x402**, which uses HTTP requests/responses and `402` to drive payment negotiation and retry:

- The server responds with `402 Payment Required` and includes protocol-defined metadata describing acceptable payment options.
- The client selects an option, pays, and retries the request with protocol-defined payment information that the server (or a delegated component) can verify.

Project overview and docs:

- GitHub repository: https://github.com/coinbase/x402
- Coinbase developer docs: https://docs.cdp.coinbase.com/x402/welcome

## See also

- [x402](/pages/x402.md)
- [Agent Payments Protocol (AP2)](/pages/Agent%20Payments%20Protocol%20(AP2).md)
- [Secure Payment Confirmation (W3C)](/pages/Secure%20Payment%20Confirmation%20(W3C).md)
