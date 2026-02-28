# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code whose semantics are intentionally **underspecified**: the IETF defines it as **reserved for future use**, without standardizing any interoperable payment challenge/response mechanism. (RFC 9110, §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#section-15.5.3)

In practice, services sometimes use `402` as an application-level signal that access to a resource depends on a payment step (or that a payment-related request failed). MDN notes that the status code is “reserved but not defined” and that “actual implementations vary” (including response format and contents). https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

## What the standard says

- **Status meaning:** “Payment Required” (client error class).
- **Standardization status:** reserved for future use; core HTTP does not define a standard payment negotiation format for `402`. RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#section-15.5.3
- **Registry entry:** IANA lists `402 Payment Required` and references RFC 9110. https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml

## Practical use patterns

Because `402` does not define headers, payloads, or verification rules, clients generally need **protocol-specific support** (headers, token formats, signing rules, etc.) to interoperate with a given service.

Common patterns include:

- **Paywall / payment required:** the response indicates the resource is available if the client completes a payment step, and the client retries the request with whatever proof/token the protocol defines.
- **Payment attempt failed:** some payment APIs return `402` as a generic error for a failed payment request, with details in a JSON body (MDN provides an example). https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

### Example: Stripe API (uses `402` for “request failed”)

Stripe’s API documentation summarizes conventional HTTP status codes and describes `402` as **“Request Failed”**: “The parameters were valid but the request failed.” https://docs.stripe.com/api/errors

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
