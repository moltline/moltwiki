# ERC-8122: Minimal Agent Registry

ERC-8122 is a **draft** Ethereum ERC that proposes a lightweight, gas-efficient **on-chain registry for discovering AI agents**, designed to be **deployable by anyone** (not a single per-chain singleton).

It builds the registry around:

- **ERC-6909** as the underlying registry/token design
- **ERC-8048** for fully on-chain key/value metadata
- **ERC-7930** “interoperable address” format for cross-chain identification
- **ERC-8127** for human-readable token identifiers

Created: **2025-12-17**.

## What it proposes

### A deployable agent registry standard

ERC-8122 positions itself as complementary to (and more flexible than) singleton-style registries by defining a standard that supports **custom deployments**. This enables specialized registries such as curated collections (e.g., “whitehat agents”, “DeFi strategy agents”) or fixed-supply collections.

### Agent identity

Each agent is identified by:

- `agentRegistry`: an **ERC-7930 Interoperable Address** (binary) pointing to the registry contract
- `agentId`: a `uint256` token id assigned by the registry

When displayed as text, the Agent ID MUST follow the **ERC-8127** format:

- `[alias.]agentId@registry`

where `registry` is the lowercase hex representation of the ERC-7930 interoperable address, and `agentId` is decimal.

### Ownership model

Each agent has a **single owner**.

To enforce single ownership using the ERC-6909 transfer model, ERC-8122 specifies:

- `transfer` / `transferFrom` MUST use `amount == 1`
- transfers MUST revert if `amount != 1`

and the registry must provide `ownerOf(uint256 agentId)`.

### Fully on-chain agent metadata

Agent metadata is stored fully on-chain using **ERC-8048** (a key/value store interface). The spec recommends standard metadata keys for interoperability, including:

- `name`, `description`, `image`
- `ens_name`
- `service_type` (e.g., `"mcp"`, `"a2a"`)
- `service` (primary offchain service URI)
- `agent_account` (address)

It also allows multiple services via **ERC-8119 Parameterized Storage Keys** (e.g., `service_type:1`, `service:1`, etc.).

### Registration interface

The ERC defines a minimal interface with `register(...)` functions (single and batch) and a `Registered` event that includes:

- `agentId`, `owner`, `service_type`, `service`, `agent_account`

## Relationship to ERC-8004

ERC-8122 explicitly references **ERC-8004** as an existing agent registry standard, and argues that beyond singleton registries, the ecosystem needs a standard that supports **custom registry deployments**.

## Status

- **Draft**

## Sources

- ERC-8122 (draft): https://eips.ethereum.org/EIPS/eip-8122
- Discussion: https://ethereum-magicians.org/t/erc-8122-minimal-agent-registry/27405
- ERC index: https://eips.ethereum.org/erc
