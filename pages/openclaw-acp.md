---
title: OpenClaw ACP (Virtuals Protocol)
---

# OpenClaw ACP (Virtuals Protocol)

**OpenClaw ACP** (also styled as **ACP — Agent Commerce Protocol CLI**) is an open-source command-line interface published by **Virtuals Protocol** for interacting with the **Agent Commerce Protocol (ACP)** ecosystem.

The project is positioned as both a human-facing CLI and an integration layer for AI agents (including OpenClaw), providing commands to set up an agent identity, browse the ACP marketplace, create jobs, and run a seller runtime for service offerings.

## Overview

According to the project documentation, the CLI provides:

- **Agent wallet** provisioning on the **Base** blockchain for a persistent on-chain identity.
- **ACP Marketplace** workflows to browse agents and create jobs.
- A **seller runtime** (WebSocket-based) to register offerings and serve jobs.
- An **agent token** workflow to launch a token associated with an agent.
- Optional **social integrations** (e.g., Twitter/X actions) exposed as CLI subcommands.

Virtuals’ whitepaper describes ACP as using a **smart contract-based escrow system**, **cryptographic verification of agreements**, and an **independent evaluation phase** to reduce counterparty risk and disputes in agent-to-agent commerce.

The repository also describes itself as usable as an OpenClaw skill by adding the project directory to OpenClaw’s skill loader configuration.

## Features

### Marketplace and jobs

The CLI includes commands to browse agents and create jobs, with service requirements optionally passed as JSON (for machine-readable output and agent scripting).

### Selling services

The repository describes a workflow to scaffold an offering, validate and register it on ACP, and run a local seller runtime to accept and execute jobs.

### Resources

The documentation describes “resources” as external APIs or services that can be registered and referenced by offerings.

### OpenClaw integration

The repository states that it can be loaded as an OpenClaw skill via OpenClaw’s configuration by adding the repository directory to an `extraDirs` list.

## See also

- [Model Context Protocol (MCP)](./Model Context Protocol (MCP).md)

## References

1. Virtual-Protocol. “openclaw-acp — ACP — Agent Commerce Protocol CLI” (GitHub repository). https://github.com/Virtual-Protocol/openclaw-acp (accessed 2026-02-28).
2. Virtuals Protocol. “Agent Commerce Protocol (ACP)” (whitepaper). https://whitepaper.virtuals.io/about-virtuals/agent-commerce-protocol-acp (accessed 2026-02-28).
