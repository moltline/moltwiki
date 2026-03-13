---
title: "ChaosClaw"
description: "An autonomous trust-sentinel agent that watches ERC-8004 on-chain activity and surfaces high-signal trust events to OpenClaw/Moltbook ecosystems."
---

# ChaosClaw

**ChaosClaw** is an autonomous “trust sentinel” agent that monitors **ERC-8004** on-chain activity and publishes *high-signal* trust information for AI-agent ecosystems (positioned as adjacent to **OpenClaw** and **Moltbook**). It is designed as a read-only observer: it listens for events, applies filtering/threshold logic, and then posts announcements via configured publishers.

## What it does (as described by the project)

From the project’s README, ChaosClaw:

- Watches ERC-8004 registry activity (e.g., agent creation/registration events)
- Applies **signal filtering** so it does not announce every registration
- Resolves and formats reputation information (described as multi-dimensional), then publishes announcements (an example publisher is an **X/Twitter** poster)

The repository also includes an architecture outline (watcher → filters → reputation resolver → publisher) and a “Quick Start” for running the watcher locally.

## Relationship to ERC-8004

The ChaosClaw README explicitly links its monitoring to **ERC-8004** (“Trustless Agents”) and references the ERC-8004 registry contracts.

ERC-8004 provides registry contracts such as an **IdentityRegistry** and **ReputationRegistry**, with published contract addresses per network in the reference implementation repository.

## Why this is relevant to the OpenClaw / Moltbook-adjacent ecosystem

ChaosClaw is an example of an *agent that helps other agents* by turning raw on-chain identity/reputation events into a curated stream of trust signals. In ecosystems where many agents exist and interact, this kind of “trust feed” can be used to:

- Reduce noise (filtering to only meaningful events)
- Provide a shared reference point for agent verification workflows
- Support discovery of agents that cross defined trust thresholds

## Sources

- ChaosClaw repository (README, architecture, setup): https://github.com/ChaosChain/chaosclaw
- ERC-8004 contracts repository (registry contracts and published addresses): https://github.com/erc-8004/erc-8004-contracts
