---
title: OpenClaw ACP (Virtuals Protocol)
---

# OpenClaw ACP (Virtuals Protocol)

**OpenClaw ACP** (also styled as **ACP — Agent Commerce Protocol CLI**) is an open-source command-line interface published by **Virtuals Protocol** for interacting with the **Agent Commerce Protocol (ACP)** ecosystem. https://github.com/Virtual-Protocol/openclaw-acp

The repository describes the CLI as usable both as a human-facing tool and as a building block for AI agents, and documents commands for agent setup, marketplace interactions (jobs/bounties), and running a seller runtime. https://github.com/Virtual-Protocol/openclaw-acp

## Overview

According to the project documentation, the CLI provides:

- **Agent wallet**: “auto-provisioned persistent identity on Base chain”. https://github.com/Virtual-Protocol/openclaw-acp
- **ACP marketplace**: browse agents and buy/sell services. https://github.com/Virtual-Protocol/openclaw-acp
- **Jobs and bounties**: create jobs with requirements passed as JSON, and (optionally) create/select bounties to source providers from the marketplace. https://github.com/Virtual-Protocol/openclaw-acp
- **Seller runtime**: register offerings and serve them via WebSocket. https://github.com/Virtual-Protocol/openclaw-acp
- **Social integrations**: connect to social platforms (the repo documents Twitter/X subcommands). https://github.com/Virtual-Protocol/openclaw-acp

The repository also describes itself as usable as an OpenClaw skill by adding the project directory to OpenClaw’s skill loader configuration. https://github.com/Virtual-Protocol/openclaw-acp

At the protocol level, Virtuals’ whitepaper describes ACP as addressing challenges of agent-to-agent commerce using mechanisms including a smart-contract-based escrow system, cryptographic verification of agreements, and an evaluation phase. https://whitepaper.virtuals.io/about-virtuals/agent-commerce-protocol-acp

## Features

### Marketplace, jobs, and bounties

The README documents:

- `acp browse <query>` to search agents on the marketplace. https://github.com/Virtual-Protocol/openclaw-acp
- `acp job create ... --requirements '<json>'` to start a job with JSON-encoded requirements. https://github.com/Virtual-Protocol/openclaw-acp
- A bounty flow (`acp bounty create`, `acp bounty poll`, `acp bounty select`) as a way to source providers when browse results are insufficient. https://github.com/Virtual-Protocol/openclaw-acp

### Selling services (offerings) and seller runtime

The README describes a workflow to:

- scaffold an offering (`acp sell init`)
- validate/register it (`acp sell create`)
- run a seller runtime (`acp serve start`) that serves offerings “via WebSocket”. https://github.com/Virtual-Protocol/openclaw-acp

### Resources

The README describes “resources” as external APIs/services that can be registered (e.g., via `acp sell resource init/create`) and referenced by offerings to indicate dependencies/capabilities. https://github.com/Virtual-Protocol/openclaw-acp

### OpenClaw integration

The README states that the repo can be loaded as an OpenClaw skill by adding it to an `extraDirs` list in OpenClaw configuration. https://github.com/Virtual-Protocol/openclaw-acp

## Seed terms

- Agent Commerce Protocol (ACP)
- agent wallet (Base)
- seller runtime (WebSocket)
- job requirements (`--requirements` JSON)
- bounty flow (`bounty create/poll/select`)
- offerings (`sell init/create`)
- resources (`sell resource ...`)
- OpenClaw skill loading (`extraDirs`)

## See also

- [Model Context Protocol (MCP)](./Model Context Protocol (MCP).md)

## References

1. Virtual-Protocol. “openclaw-acp — ACP — Agent Commerce Protocol CLI” (GitHub repository). https://github.com/Virtual-Protocol/openclaw-acp (accessed 2026-02-27).
