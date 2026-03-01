# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code whose semantics are **reserved for future use** in core HTTP. In practice, that means HTTP itself does not define an interoperable way for a server to describe acceptable payment methods or for a client to present proof-of-payment; any such mechanism must be defined at the application/protocol layer. (RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required)

MDN summarizes `402` as “nonstandard … reserved for future use”, and notes that real-world behavior varies across implementations. https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

## What the standard says

- **Status meaning:** “Payment Required” (client error class). RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required
- **Standardization status:** reserved for future use; no HTTP-wide challenge/response format is defined. RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required
- **Registry entry:** IANA’s HTTP Status Code Registry lists `402 Payment Required` with a reference to RFC 9110. https://www.iana.org/assignments/http-status-codes

## Practical use patterns

Because there is no standard “payment challenge” header equivalent to `WWW-Authenticate` for `401`, services that return `402` typically define their own conventions (headers, token formats, signing rules, etc.) at the application layer.

Common patterns include:

- **Paywall / payment required:** the response indicates the resource is available if the client pays, and the client retries with whatever proof/token the service defines.
- **Payment attempt failed:** some payment APIs use `402` as a generic “request failed due to payment” response, with details in a JSON body. (Examples and notes: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402)

### Example: Stripe API error mapping

Stripe documents `402` as “Request Failed” for API requests where the parameters were valid but the request failed (commonly due to a failed payment). https://docs.stripe.com/api/errors

### Interoperability implications

If you build a generic HTTP client, you generally cannot treat `402` as a standardized payment negotiation flow. Interoperability requires protocol-specific support (e.g., understanding service-defined headers/body fields and how to construct a retry request).

## Example: x402 (application-layer protocol)

One modern example is **x402**, a payment protocol that uses HTTP requests/responses and `402` to drive a pay-and-retry flow:

- A server returns `402 Payment Required` along with protocol-defined metadata describing acceptable payment options.
- The client selects an option, pays, and retries with protocol-defined payment information that the server (or a delegated verifier) can validate.

Project overview and docs:
- GitHub repository: https://github.com/coinbase/x402
- Coinbase developer docs: https://docs.cdp.coinbase.com/x402/welcome

## See also

- [x402](/pages/x402.md)
- [Payment Request API](/pages/Payment%20Request%20API.md)
- [Payment Handler API](/pages/Payment%20Handler%20API.md)
