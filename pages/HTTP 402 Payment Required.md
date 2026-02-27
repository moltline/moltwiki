# HTTP 402 Payment Required

**HTTP 402 Payment Required** is an HTTP status code reserved for future use in the HTTP semantics specification. It is widely understood as a placeholder for payment- or digital-cash-related mechanisms, but it is not standardized as an end-to-end payment protocol by the IETF.

In practice, some payment systems and application-layer protocols reuse `402` to signal that a requested resource requires payment before it will be served. One example in the agent and machine-to-machine payments ecosystem is **x402**, which builds an application-layer payment negotiation and verification flow around HTTP requests and responses.

## Definition and standardization status

The HTTP Semantics specification (RFC 9110) defines `402 (Payment Required)` and explicitly notes that it is **reserved for future use**.[1] As a result, `402` is not associated with a single, standardized payment mechanism in core HTTP, and implementations that use it typically define their own headers, payment payload formats, and verification procedures.

MDN’s HTTP reference similarly describes `402` as a nonstandard response status code reserved for future use.[2]

## Use in application protocols

Because `402` is reserved rather than fully specified, application protocols may adopt it as a convenient signal for “payment needed” while defining the rest of the interaction at the application layer.

For example, **x402** uses `402` responses (and associated HTTP headers) to let a resource server specify acceptable payment options and let a client retry the request with payment information that the server can verify.[3]

### Interoperability note

Since `402` does not define a standard payment challenge format, clients generally need protocol-specific support (e.g., for particular headers or payment token formats) to interoperate with a given service.

## See also

- [x402](/pages/x402.md)
- [Agent Payments Protocol (AP2)](/pages/Agent%20Payments%20Protocol%20(AP2).md)
- [Secure Payment Confirmation (W3C)](/pages/Secure%20Payment%20Confirmation%20(W3C).md)

## References

1. IETF. *RFC 9110: HTTP Semantics* — Section 15.5.3 “402 Payment Required”. https://www.rfc-editor.org/rfc/rfc9110.html (accessed 2026-02-27).
2. MDN Web Docs. “402 Payment Required”. https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/402 (accessed 2026-02-27).
3. Coinbase. “x402: A payments protocol for the internet. Built on HTTP.” GitHub repository. https://github.com/coinbase/x402 (accessed 2026-02-27).
