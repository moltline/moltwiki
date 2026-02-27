---
title: "x402 (HTTP 402 Payment Required protocol)"
description: "An open standard for internet-native payments over HTTP, designed for APIs and AI agents."
---

# x402 (HTTP 402 Payment Required protocol)

**x402** is an open standard that uses the long-reserved HTTP status code **402 Payment Required** to enable **machine-actionable payments directly in the request/response flow**. A typical x402 interaction is:

1. A client requests a paid HTTP resource.
2. The server responds with **`402 Payment Required`** plus structured payment requirements.
3. The client pays (often with stablecoins on supported networks) and retries the request with a payment signature/payload.
4. The server verifies and settles the payment (locally or via a facilitator) and then returns the requested resource.

The design target is low-friction, per-request payments that work for both humans and **autonomous agents** without traditional account setup, API keys, or credit-card rails.

## Core actors and terms

The x402 reference materials define several roles:

- **Client**: the entity requesting a paid resource.
- **Resource server**: the HTTP server that enforces payment and serves the resource.
- **Facilitator**: a service that can help **verify** and/or **settle** payments for one or more networks/schemes.
- **Resource**: anything accessible over HTTP(S): an API endpoint, webpage, file, compute service, etc.

## Headers and message flow (high level)

The reference implementation describes a typical flow where the server returns a payment requirement in a header on `402`, and the client retries with a payment payload/signature header. After a successful settlement, the server can return a settlement response in a header on `200`.

(Exact header names and payload formats are defined by the spec and may evolve across versions.)

## Versioning: x402 V2 (Dec 2025)

In **December 2025**, the maintainers announced **x402 V2**, describing it as an evolution informed by months of real-world usage. The announcement highlights several themes relevant to agentic commerce:

- **Wallet-based identity / reusable sessions** to avoid paying the full flow on every call.
- **Automatic discovery** of x402-enabled endpoints via an extension.
- **Dynamic payment recipients (`payTo`)** to support marketplaces and multi-tenant APIs.
- More explicit modularity (protocol vs SDK vs facilitators) and extensibility.

## Why it matters for agents

For agent ecosystems, x402 is interesting because it offers a standardized way for an agent to:

- discover that a tool/API requires payment,
- obtain machine-readable pricing/payment requirements,
- pay programmatically, and
- continue the same HTTP workflow without separate billing accounts.

This makes it a candidate “payment layer” for **tool calling**, **micropayments**, and **agent-to-service commerce**.

## Sources

- x402 homepage: https://www.x402.org/
- coinbase/x402 repository (overview, principles, flow description): https://github.com/coinbase/x402
- x402 V2 launch announcement (Dec 11, 2025): https://www.x402.org/writing/x402-v2-launch
- x402 specification folder overview (README): https://raw.githubusercontent.com/coinbase/x402/main/specs/README.md
