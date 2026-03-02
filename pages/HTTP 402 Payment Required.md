# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code defined by the IETF as **reserved for future use**. Core HTTP does not standardize *how* a client should pay or *how* a server should describe acceptable payment methods; any system that uses `402` must define the payment interaction at the application layer. (RFC 9110, §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required)

Because the semantics are intentionally underspecified, `402` is mostly used by APIs and custom protocols as a convenient signal for “you need to pay (or your payment failed) before you can access this resource”. MDN summarizes this as: “reserved but not defined; actual implementations vary”. https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402

## What the standard says

- **Status meaning:** “Payment Required” (client error class). RFC 9110 §15.5.3: https://www.rfc-editor.org/rfc/rfc9110.html#name-402-payment-required
- **Standardization status:** reserved for future use; HTTP does **not** define a challenge/response format, required headers, or a payment verification mechanism.
- **Registry entry:** IANA lists `402 Payment Required` with a reference to RFC 9110. https://www.iana.org/assignments/http-status-codes

## What `402` is (and is not)

- `402` is analogous to `401`/`407` only in the sense that it signals “you can’t proceed until a prerequisite is satisfied”.
- Unlike `401` (which uses `WWW-Authenticate`) and `407` (which uses `Proxy-Authenticate`), `402` has **no standardized** negotiation header or authentication scheme in HTTP.
- As a result, clients cannot implement generic `402` handling without knowing the **application protocol** (which headers/body fields to look for, how to construct proof-of-payment, how to retry, etc.).

## Practical use patterns

Since there is no standard “payment challenge” equivalent to `WWW-Authenticate` for `401`, implementations typically choose their own approach:

- **Paywall / payment required:** the response indicates the resource is available if the client pays, and the client retries the request with whatever proof/token the protocol defines.
- **Payment attempt failed:** some payment APIs return `402` as a generic error for a failed payment (e.g., declined/expired card), with details in a JSON body. (Example and compatibility notes: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402)

### Interoperability implications

Because `402` does not define headers, payloads, or verification rules, clients generally need **protocol-specific support** (headers, token formats, signing rules, etc.) to interoperate with a given service.

## Example: x402 (application-layer protocol)

One modern example is **x402**, an open standard that uses HTTP requests/responses and `402` to drive payment negotiation and retry.

A typical x402 flow (per the project spec) looks like:

1. Client makes an HTTP request to a resource server.
2. Resource server responds with `402 Payment Required` and includes a base64-encoded “PaymentRequired” object in a `PAYMENT-REQUIRED` header.
3. Client selects one of the returned payment requirements, creates a payment payload, and retries the request with a `PAYMENT-SIGNATURE` header.
4. Resource server verifies the payment payload locally or via a facilitator service, then fulfills the request and may return a `PAYMENT-RESPONSE` header containing settlement results.

Source (x402 repository / spec overview): https://github.com/coinbase/x402

## See also

- [x402](/pages/x402.md)
- [Agent Payments Protocol (AP2)](/pages/Agent%20Payments%20Protocol%20(AP2).md)
- [Secure Payment Confirmation (W3C)](/pages/Secure%20Payment%20Confirmation%20(W3C).md)
