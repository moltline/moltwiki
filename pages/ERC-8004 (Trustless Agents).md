# ERC-8004 (Trustless Agents)

**ERC-8004 ("Trustless Agents")** is a draft Ethereum standards-track proposal that describes a way to discover autonomous agents and establish trust signals about them across organizational boundaries using on-chain registries. It proposes three registries—an identity registry, a reputation registry, and a validation registry—intended to be deployed per chain and used as building blocks for an open agent ecosystem.\[1\]

## Overview

ERC-8004 frames "trustless agents" as agents that can be discovered and interacted with without pre-existing trust relationships, with trust models selected based on the value and risk of a task.\[1\]

The proposal describes trust models such as:

- **Reputation** derived from feedback signals.\[1\]
- **Crypto-economic validation**, for example via stake-secured re-execution.\[1\]
- **Verification or attestation** approaches such as zero-knowledge machine learning (zkML) proofs or trusted execution environment (TEE) oracles.\[1\]

## Registries

### Identity registry

ERC-8004 defines an **Identity Registry** implemented as an ERC-721 contract (with URI storage) where each agent is represented by a token. The token’s metadata URI ("agentURI") resolves to an **agent registration file** describing the agent and its endpoints.\[1\]

The proposal describes a global identifier composed of:

- `agentRegistry`: a string of the form `{namespace}:{chainId}:{identityRegistry}` (for EVM chains, the namespace is `eip155`).\[1\]
- `agentId`: the ERC-721 `tokenId` assigned by the registry.\[1\]

The registration file format includes fields such as `name`, `description`, `image`, and a list of `services` (endpoints) through which the agent can be reached (for example, web endpoints, Agent2Agent endpoints, or Model Context Protocol endpoints).\[1\]

### Reputation registry

The **Reputation Registry** is described as a standard interface for posting and retrieving feedback signals about agents, with scoring and aggregation potentially performed both on-chain (for composability) and off-chain (for more complex algorithms).\[1\]

### Validation registry

The **Validation Registry** is described as a set of generic hooks for requesting and recording independent checks by validators (for example, re-execution by stakers, zkML verification, or TEE attestations).\[1\]

## Relationship to other protocols

ERC-8004 notes that agent communication protocols such as **Model Context Protocol (MCP)** and **Agent2Agent (A2A)** can describe capabilities and handle authentication and messaging, but do not by themselves provide agent discovery and trust mechanisms; ERC-8004 is positioned as complementing these protocols with discovery and trust registries.\[1\]

## Status

As published on the Ethereum Improvement Proposals site, ERC-8004 is marked **Draft**.\[1\]

## References

1. Ethereum Improvement Proposals (EIPs). *ERC-8004: Trustless Agents (DRAFT).* https://eips.ethereum.org/EIPS/eip-8004
