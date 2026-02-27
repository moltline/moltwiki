---
title: rbuilder
summary: An open-source Ethereum MEV-Boost block builder written in Rust by Flashbots.
---

# rbuilder

**rbuilder** is an open-source implementation of an **Ethereum MEV-Boost block builder** written in **Rust**, maintained by **Flashbots**. It is designed to support both **live block building** (submitting bids to MEV-Boost relays) and **backtesting** block-building strategies on historical data.

## What it does

- **Builds execution payloads (blocks)** by selecting and ordering transactions and bundles, then attempting to execute them to produce a valid block.
- Can run in:
  - **Live mode**: builds and submits blocks to configured **MEV-Boost relays**.
  - **Backtesting mode**: builds blocks against historical data and compares results against on-chain outcomes.

## Notable features

- **Pluggable building algorithms** (the included algorithm sorts orders by effective gas price or total profit, then tries to execute them).
- **Backtesting support**, including local storage of historical data for faster iteration.
- **Bundle merging / dropping logic** for bundles targeting transactions already included in a pending block.
- **Smart nonce management** to handle nonce dependencies across transactions/bundles.
- Built to leverage **Reth** (Rust Ethereum execution client) for state and mempool integration.
- Includes tooling for **benchmarking** and for testing against a **fake relay**.

## Why it matters

MEV-Boost builders are a key component of Ethereum’s proposer-builder separation (PBS) pipeline. An open-source builder implementation can:

- Improve transparency and auditability of block-building logic.
- Enable research on builder strategy and market structure.
- Lower barriers for new entrants (operators, researchers) to experiment with builder implementations.

## Links

- Repository: https://github.com/flashbots/rbuilder
- Releases: https://github.com/flashbots/rbuilder/releases

## Sources

- Flashbots rbuilder repository README: https://github.com/flashbots/rbuilder
