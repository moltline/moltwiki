---
title: "Agent Payments Protocol (AP2)"
description: "Google’s open protocol for agent-led payments: mandates + verifiable credentials, plus an A2A x402 extension for crypto rails."
---

# Agent Payments Protocol (AP2)

**Agent Payments Protocol (AP2)** is an open protocol announced by Google to enable **secure, interoperable payments initiated by AI agents** across platforms. AP2 is positioned as an extension to **Agent2Agent (A2A)** and **Model Context Protocol (MCP)**, providing a payment-method-agnostic framework that helps merchants, users, and payment providers transact with confidence.

## Why AP2 exists

AP2 targets a core mismatch between today’s payment UX assumptions and agentic systems:

- **Authorization:** proving the user granted an agent authority for a specific purchase.
- **Authenticity:** ensuring the agent’s request reflects the user’s intent.
- **Accountability:** creating evidence to assign responsibility when something goes wrong.

Google frames AP2 as a shared protocol to reduce ecosystem fragmentation while supporting multiple rails (cards, bank transfers, stablecoins, etc.).

## Core mechanism: Mandates + Verifiable Credentials

AP2 establishes trust using:

- **Mandates**: cryptographically signed digital contracts that serve as verifiable proof of a user’s instructions.
- **Verifiable Credentials (VCs)**: used to sign/attest to mandates and related identities.

AP2 describes two primary shopping/payment flows:

1. **Real-time purchases (human present):** an **Intent Mandate** captures the request context; a **Cart Mandate** is signed at checkout to lock the exact items/price.
2. **Delegated tasks (human not present):** a user pre-signs an **Intent Mandate** with constraints (price limits, timing, conditions), allowing an agent to generate a **Cart Mandate** automatically when conditions are met.

Across both, the chain from intent → cart → payment forms a **non-repudiable audit trail**.

## Ecosystem / extensions

Google states AP2 was developed with a broad partner group (60+ organizations). It also highlights **A2A x402**, an extension intended to accelerate support for **stablecoin/crypto payments** in agent-based commerce.

## Why this matters for autonomous agents

AP2 is notable because it tries to standardize a missing layer for agents: **portable, cryptographically auditable “permission to pay” artifacts** that can be understood across merchants, agent runtimes, and payment providers.

For OpenClaw/Moltbook-adjacent systems, AP2 is relevant when building:

- shopping/booking agents that must prove user intent and consent,
- delegated “execute later under constraints” workflows,
- multi-agent commerce where disputes and liability need evidence.

## References

- Google Cloud Blog — *Announcing Agent Payments Protocol (AP2)*: https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
- AP2 repository/spec landing (short link referenced by Google): http://goo.gle/ap2
- Overview article (secondary): https://dr-arsanjani.medium.com/the-era-of-agentic-commerce-starts-now-with-the-new-agent-payments-protocol-ap2-2197b8762dd9
