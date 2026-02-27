---
title: "ERC-8004: Trustless Agents"
description: "An Ethereum ERC proposal for discovering agents and establishing trust via identity, reputation, and validation registries."
tags: [ethereum, eip, erc, agents, identity, reputation, validation]
---

# ERC-8004: Trustless Agents

**ERC-8004 ("Trustless Agents")** is an Ethereum **ERC (standards-track) proposal** that specifies a lightweight on-chain framework for **agent discovery** and **pluggable trust** across organizational boundaries.

At a high level, ERC-8004 proposes three registries (which can be deployed on mainnet or L2s):

- **Identity Registry**: an **ERC-721-based** registry that gives each agent a portable identifier and a URI pointing to an agent registration file.
- **Reputation Registry**: a standard interface for recording and retrieving feedback signals about agents.
- **Validation Registry**: hooks for recording independent checks (e.g., stake-secured re-execution, zkML verification, TEE attestations, or other validator schemes).

The motivation is to complement off-chain agent communication protocols (e.g., A2A, MCP) with mechanisms for **discovering agents** and reasoning about **trust** without requiring pre-existing relationships.

## Identity Registry (agent registration)

ERC-8004’s Identity Registry is defined as an ERC-721 contract (with URI storage) where each token represents an **agent**. The agent’s `tokenURI` (referred to as **agentURI**) must resolve to an **agent registration file** (JSON) describing the agent and its endpoints.

The proposal describes a registration file shape that includes fields like:

- `name`, `description`, `image`
- a list of `services` / endpoints (examples include web, A2A AgentCard, MCP endpoint, ENS name, DID, email)
- optional declarations of supported trust mechanisms

This design makes agents **browsable** and **transferable** using existing NFT tooling, while still pointing to richer off-chain metadata.

## Reputation Registry (feedback signals)

The Reputation Registry is intended to standardize how clients post and fetch feedback about agents. The ERC-8004 draft describes feedback as including a signed numeric value (fixed-point), optional tags, and optional pointers to off-chain evidence (e.g., a JSON file plus hash).

In practice, this component aims to make reputation data **indexable** and **composable** (both on-chain and off-chain), enabling scoring services, auditor networks, or insurance mechanisms to build on a shared interface.

## Validation Registry (independent checks)

The Validation Registry is described as a generic interface for requesting and recording third-party validations of agent behavior. The draft explicitly frames validation as **tiered** and **pluggable**, with different security/cost tradeoffs depending on the value at risk.

Examples mentioned in the draft include:

- stake-secured re-execution by validators
- zero-knowledge proofs (e.g., zkML)
- trusted execution environment (TEE) attestations

## Status

As of its EIPs site entry, **ERC-8004 is marked Draft**.

## Sources

- Ethereum EIPs: **EIP-8004 / ERC-8004 — “Trustless Agents” (Draft)**: https://eips.ethereum.org/EIPS/eip-8004
- Discussion thread (Ethereum Magicians): https://ethereum-magicians.org/t/erc-8004-trustless-agents/25098
