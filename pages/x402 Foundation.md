# x402 Foundation

The **x402 Foundation** is an initiative announced by Cloudflare in partnership with Coinbase to encourage adoption of the **x402** protocol, an open standard for exchanging value over HTTP using the `402 Payment Required` status code as part of a machine-readable payment flow.[^cloudflare-x402]

## Background

HTTP status code **402 Payment Required** has long existed but historically lacked a widely adopted, interoperable specification for how servers should describe payment requirements and how clients should respond programmatically.[^cloudflare-x402]

The **x402** protocol (maintained as an open-source project by Coinbase) describes a client–server flow in which a resource server can respond with `402 Payment Required` along with machine-readable payment requirements, and a client can retry the request with a payment payload that the server can verify and settle (directly or via a payment facilitator).[^coinbase-x402]

## Announcement

On 23 September 2025, Cloudflare announced it was partnering with Coinbase to create the **x402 Foundation**, with the stated mission of encouraging adoption of the x402 protocol.[^cloudflare-x402]

In the same announcement, Cloudflare described product work to support x402 transactions in its Agents SDK and Model Context Protocol (MCP) integrations, and proposed a deferred payment scheme intended for scenarios where settlement is aggregated or delayed (for example, batching charges).[^cloudflare-x402]

## Relationship to x402

The x402 Foundation is associated with the broader x402 ecosystem, which includes:

- **Clients** that interpret x402 payment requirements and attach payment payloads to HTTP requests.
- **Resource servers** that gate access to resources using x402.
- **Facilitators** that can verify and/or settle payments on behalf of resource servers for supported networks and schemes.[^coinbase-x402]

## See also

- [x402](x402.md)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

[^cloudflare-x402]: Cloudflare. "Launching the x402 Foundation with Coinbase, and support for x402 transactions" (23 September 2025). https://blog.cloudflare.com/x402/

[^coinbase-x402]: Coinbase. "coinbase/x402" (GitHub repository). https://github.com/coinbase/x402
