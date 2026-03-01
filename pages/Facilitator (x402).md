# Facilitator (x402)

A **facilitator** in **x402** is an optional service that performs payment **verification** and/or **settlement** on behalf of a resource server. The facilitator role is intended to reduce the amount of chain- and scheme-specific payment logic that resource servers must implement, while keeping the x402 interaction HTTP-native.[1][2]

## Role in the x402 flow

In a typical x402 exchange, a resource server can delegate payment processing to a facilitator:

1. The client requests a paid endpoint.
2. The resource server returns **HTTP 402 Payment Required** with payment requirements (e.g., in the `PAYMENT-REQUIRED` header).
3. The client retries the request with a signed payment payload (e.g., in the `PAYMENT-SIGNATURE` header).
4. The resource server verifies the payment payload either **locally** or by sending it to a facilitator’s **`/verify`** endpoint.[1]
5. If the payment is accepted, the resource server fulfills the request and then settles the payment either directly on-chain or by using a facilitator’s **`/settle`** endpoint.[1]
6. After settlement, the resource server returns the requested resource and may include settlement details (e.g., in a `PAYMENT-RESPONSE` header).[1][2]

## Responsibilities

Implementations and documentation commonly describe facilitators as handling tasks such as:[1][2]

- **Scheme/network-specific verification** of payment payloads (for example, supporting particular *(scheme, network)* combinations).
- **Submitting settlement transactions** to the underlying network and waiting for confirmation.
- Returning structured responses that resource servers can use to decide whether to serve the requested resource and how to report settlement outcomes.

Because x402 aims to support multiple networks and payment schemes, the facilitator is a natural place to centralize chain integrations (RPC access, gas/fee logic, signing standards) while keeping resource servers comparatively simple.[2]

## Trust and security considerations

The x402 project describes the protocol as **trust-minimizing**, and notes that payment schemes should not allow a facilitator (or resource server) to move funds other than in accordance with client intentions.[2] In practice, the trust model depends on the scheme and network pair in use, and on how payment payloads authorize value transfer.

## See also

- [x402](x402.md)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)

## References

1. Coinbase Developer Documentation. "How x402 Works." https://docs.cdp.coinbase.com/x402/core-concepts/how-it-works (accessed 2026-03-01).
2. Coinbase. "coinbase/x402: A payments protocol for the internet. Built on HTTP." GitHub repository. https://github.com/coinbase/x402 (accessed 2026-03-01).
