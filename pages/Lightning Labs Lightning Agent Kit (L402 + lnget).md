# Lightning Labs Lightning Agent Kit (L402 + lnget)

The **Lightning Agent Kit** (also referred to as **Lightning agent tools**) is an open-source toolkit from **Lightning Labs** aimed at giving AI agents the ability to **transact natively on the Bitcoin Lightning Network**. It is designed to support agent-to-service commerce by combining:

- **L402** (an HTTP 402 “Payment Required” based authentication + payment scheme),
- **lnget** (an L402-aware HTTP CLI client), and
- optional server-side components like **Aperture** (an L402-aware reverse proxy).

Lightning Labs frames this as infrastructure for a “machine-payable web,” where autonomous software can pay for APIs and resources without identity-based signup flows or API keys.[1]

## What it enables

According to Lightning Labs, the kit provides a set of composable “skills” that can be used by agents (or agent frameworks) to:

- run and manage a Lightning node,
- isolate private keys via a **remote signer** architecture,
- create least-privilege credentials using **macaroons** (for example, “pay-only”),
- pay for L402-gated HTTP resources, and
- host paid endpoints (for example, behind an L402 reverse proxy).[1]

## L402 in brief

**L402** is a protocol pattern that uses the HTTP **402 Payment Required** status code as the entry point for programmatic payments.

In the flow described by Lightning Labs, when a client hits an L402-protected endpoint, the server responds with a 402 challenge containing:

- a **Lightning invoice** to pay, and
- an authentication token (commonly described as a **macaroon**).

After paying the invoice, the client receives a cryptographic proof of payment (**preimage**) and uses it (together with the macaroon) to authenticate subsequent requests.[1]

## lnget

**lnget** is an L402-aware command-line HTTP client (positioned as analogous to `curl`/`wget`) that automates the “pay then retry” loop for L402-gated resources.

Lightning Labs describes lnget as:

- detecting 402 payment challenges,
- paying the Lightning invoice via a configured Lightning backend, and
- retrying the request with the correct authorization material, caching credentials for reuse.[1]

Lightning Labs describes support for multiple Lightning backends, including direct connection to an `lnd` node and Lightning Node Connect (LNC).[1]

## Security model: remote signer + scoped credentials

Because agents may operate autonomously with access to real funds, Lightning Labs emphasizes a security model based on:

- **remote signer architecture**: private keys are held on a separate signer machine and are not present on the agent machine, and
- **scoped macaroons**: credentials can be constrained to least privilege (for example, pay-only vs invoice-only vs read-only).[1]

## Relationship to other “HTTP 402 payments” work

L402 is one approach to “HTTP 402 payments.” In parallel, other ecosystems (for example, stablecoin-based HTTP payment schemes) have proposed similar request/response patterns that also revolve around a **payment-required response** followed by a **client-supplied payment proof**.

## References

1. Lightning Labs. “The Agents Are Here and They Want to Transact: Powering the AI Economy with Lightning.” https://lightning.engineering/posts/2026-02-11-ln-agent-tools/ (accessed 2026-02-27).
2. Lightning Labs (GitHub). “lightning-agent-kit” repository. https://github.com/lightninglabs/lightning-agent-kit (accessed 2026-02-27).
3. Lightning Labs (GitHub). “L402” repository. https://github.com/lightninglabs/L402 (accessed 2026-02-27).
