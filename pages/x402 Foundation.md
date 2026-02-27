# x402 Foundation

The **x402 Foundation** is an initiative announced by **Cloudflare** and **Coinbase** to encourage adoption of the **x402** payments protocol, a proposed standard for machine-readable payments over HTTP using the HTTP **402 (Payment Required)** status code.[1][2]

## Background

HTTP defines **402 (Payment Required)** as a reserved status code for future use.[3] x402 uses 402 as the signaling mechanism for payment requirements and defines a request/response pattern in which a server can advertise payment requirements and a client can retry the same request with a payment authorization payload.[2]

In September 2025, Cloudflare announced it was partnering with Coinbase to create the x402 Foundation, describing the foundation’s mission as encouraging adoption of the x402 protocol and supporting related ecosystem development.[1]

## Activities and related work

Cloudflare’s announcement described shipping x402-related support in Cloudflare’s developer tooling (including its Agents SDK and integrations with the Model Context Protocol (MCP)), and proposed a **deferred payment scheme** intended to support delayed settlement and aggregated billing use cases (for example, "pay per crawl").[1]

Coinbase maintains the primary open-source repository for x402, including protocol documentation and reference implementations.[2]

## See also

- [x402](x402.md)
- [HTTP 402 Payment Required](https://www.rfc-editor.org/rfc/rfc9110)

## References

1. Cloudflare. "Launching the x402 Foundation with Coinbase, and support for x402 transactions." Cloudflare Blog (2025-09-23). https://blog.cloudflare.com/x402/ (accessed 2026-02-27).
2. Coinbase. "coinbase/x402: A payments protocol for the internet. Built on HTTP." GitHub repository. https://github.com/coinbase/x402 (accessed 2026-02-27).
3. Fielding, R., et al. "RFC 9110: HTTP Semantics." IETF, June 2022. https://www.rfc-editor.org/rfc/rfc9110 (accessed 2026-02-27).
