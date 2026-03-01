# x402 (payment protocol)

**x402** is an open protocol for **HTTP-native payments**, designed to let clients (including automated agents) pay for access to web resources and APIs using the semantics of the HTTP **402 (Payment Required)** status code. In the x402 flow, a server can respond to an unpaid request with a 402 response that includes payment instructions; the client then retries the request with a payment authorization payload, and a payment facilitator can verify and settle the transaction.

## Overview

x402 is positioned as an “internet-native” payments standard intended to reduce friction for pay-per-request API monetization and machine-to-machine commerce, including scenarios where AI agents autonomously purchase access to tools or content.

Coinbase’s documentation describes x402 as an open payment protocol enabling automatic stablecoin payments over HTTP, using 402 responses and request headers to convey payment requirements and payment signatures.

## Protocol flow

While implementations can vary, documentation describes a basic interaction pattern:

1. **Client requests a resource** from a server.
2. If payment is required, the server responds with **HTTP 402 Payment Required**, including machine-readable payment instructions.
3. The client **constructs a payment payload** and retries the request, supplying payment authorization in headers.
4. A **facilitator** verifies the payment payload and settles the payment.
5. The server returns the requested resource along with a confirmation of payment outcome.

## Relationship to agent tooling

Cloudflare has described integrating x402 into its Agents SDK and Model Context Protocol (MCP) integrations, including support for MCP servers exposing paid tools that return 402 responses when payment is required.

## See also

- HTTP 402 (Payment Required)
- Micropayments
- Stablecoin
- Model Context Protocol (MCP)

## References

1. x402.org. “x402 – Payment Required.” https://www.x402.org/
2. Coinbase Developer Platform documentation. “Welcome to x402.” https://docs.cdp.coinbase.com/x402/welcome
3. Cloudflare Blog (2025-09-23). “Launching the x402 Foundation with Coinbase, and support for x402 transactions.” https://blog.cloudflare.com/x402/
