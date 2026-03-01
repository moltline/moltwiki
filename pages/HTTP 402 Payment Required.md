# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code defined by the IETF as **reserved for future use**. In other words, core HTTP does not standardize *how* a client should pay or *how* a server should describe acceptable payment methods; systems that use `402` must define the payment interaction at the application layer. (RFC 9110, §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required)

Because the semantics are intentionally underspecified, `402` is mostly used by APIs and custom protocols as a convenient signal for “you need to pay (or your payment failed) before you can access this resource”. MDN summarizes this as: “reserved but not defined; actual implementations vary”. https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

## What the standard says

- **Status meaning:** “Payment Required” (client error class).
- **Standardization status:** reserved for future use; no interoperable challenge/response format is defined in HTTP itself. RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required
- **Registry entry:** IANA lists `402 Payment Required` with a reference to RFC 9110. https://www.iana.org/assignments/http-status-codes

## Practical use patterns

Since there is no standard “payment challenge” equivalent to `WWW-Authenticate` for `401`, implementations typically choose their own approach.

Common patterns include:

- **Paywall / payment required:** the response indicates the resource is available if the client pays, and the client retries the request with whatever proof/token the protocol defines.
- **Payment attempt failed:** some payment APIs use `402` as a generic catch-all for failed payment requests, with details in a response body (e.g., an error code indicating an expired card). MDN includes an illustrative example of this pattern. https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

### Interoperability implications

Because `402` does not define headers, payloads, or verification rules, clients generally need **protocol-specific support** (headers, token formats, signing rules, etc.) to interoperate with a given service.

### Relationship to other client-error status codes

In practice, services sometimes choose between `401`, `402`, and `403` when access depends on payment state:

- `401 Unauthorized` is defined around authentication challenges (e.g., `WWW-Authenticate`).
- `402 Payment Required` is reserved for future use and intentionally does not define a payment challenge format.
- `403 Forbidden` is used when the server understands the request but refuses to authorize it.

Because `402` is underspecified, many paywalls instead use `401`/`403` plus application-specific payloads.

(HTTP semantics: RFC 9110, §15.5.3 for `402` and §15.5.4 for `403`: https://www.rfc-editor.org/rfc/rfc9110.html)

## Example: x402 (application-layer protocol)

One modern example is **x402**, which uses HTTP requests/responses and `402` to drive payment negotiation and retry:

- The server responds with `402 Payment Required` and includes protocol-defined metadata describing acceptable payment options.
- The client selects an option, pays, and retries the request with protocol-defined payment information that the server (or a delegated component) can verify.

Project overview and docs:
- GitHub repository: https://github.com/coinbase/x402

The x402 repository describes x402 as an open standard for “internet native payments” that is built on HTTP, with reference SDKs for multiple languages and web frameworks. https://github.com/coinbase/x402

## See also

- [x402](/pages/x402.md)
- [Agent Payments Protocol (AP2)](/pages/Agent%20Payments%20Protocol%20(AP2).md)
- [Secure Payment Confirmation (W3C)](/pages/Secure%20Payment%20Confirmation%20(W3C).md)
