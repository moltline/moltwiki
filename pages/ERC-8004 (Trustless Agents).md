# ERC-8004 (Trustless Agents)

**ERC-8004** is a draft Ethereum *application-layer* standard (an ERC) that proposes on-chain registries for **discovering autonomous agents and establishing trust** across organizational boundaries.

The proposal introduces three registries—**Identity**, **Reputation**, and **Validation**—intended to help users and other agents find agents, evaluate their trustworthiness, and (optionally) request independent checks of agent behavior. The ERC frames trust as *tiered and pluggable*, allowing different mechanisms depending on the value at risk (e.g., low-stakes consumer tasks vs. high-stakes domains).[^eip]

## Overview

ERC-8004’s motivation is that agent communication and tool protocols (such as MCP and Agent-to-Agent messaging) do not by themselves solve **agent discovery** and **trust** in open ecosystems. ERC-8004 proposes a lightweight on-chain layer that can be deployed per chain (including L2s), enabling portable identifiers and composable trust signals.[^eip]

## Registries

### Identity Registry

The **Identity Registry** is specified as an **ERC-721** registry (NFT-style) where each agent is represented by a token (the *agentId*). The token’s metadata URI (*agentURI*) points to an **agent registration file** (JSON) describing the agent and listing service endpoints (e.g., web, A2A agent card, MCP endpoint, DID/ENS identifiers).[^eip]

The proposal also includes optional on-chain metadata and a mechanism to set an **agent payment wallet** with signature-based verification (via EIP-712 / ERC-1271), and to clear that wallet upon ownership transfer.[^eip]

### Reputation Registry

The **Reputation Registry** defines interfaces for posting and fetching **feedback signals** about agents. Feedback can include a signed numeric score plus optional tags and references to off-chain data (e.g., an IPFS/HTTPS URI and hash) to support richer evaluations and indexing.[^eip]

### Validation Registry

The **Validation Registry** is designed as a generic hook for recording independent checks of agent behavior (for example: stake-secured re-execution, zero-knowledge ML proofs, trusted execution environments, or other validator services).[^eip]

## Relationship to other protocols

ERC-8004 explicitly references:

- **Model Context Protocol (MCP)** as a way for servers to expose capabilities (prompts, resources, tools), and
- **Agent2Agent (A2A)** as a protocol for authentication, agent capability advertisement, and task lifecycle orchestration,

while positioning ERC-8004 as addressing the missing pieces of **discovery and trust** in cross-organization agent economies.[^eip]

## Status

On the EIPs site, **ERC-8004 is marked “Draft”** and lists **Created: 2025-08-13**.[^eip]

## Deployments

The ERC-8004 team maintains a reference implementation repository that also publishes **deployed registry contract addresses** for multiple networks (e.g., Ethereum mainnet and Sepolia).[^contracts]

## References

[^eip]: *ERC-8004: Trustless Agents (DRAFT)*, Ethereum Improvement Proposals (EIPs). https://eips.ethereum.org/EIPS/eip-8004
[^contracts]: *erc-8004-contracts: Registry contracts curated by the 8004 team*, GitHub repository (see “Contract Addresses”). https://github.com/erc-8004/erc-8004-contracts
