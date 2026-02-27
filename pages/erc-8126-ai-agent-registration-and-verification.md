---
title: "ERC-8126: AI Agent Registration and Verification"
description: "Draft Ethereum ERC proposing a standard interface for AI agent self-registration and multi-layer verification, with privacy-preserving proof outputs."
---

# ERC-8126: AI Agent Registration and Verification

ERC-8126 is a **draft** Ethereum standards-track proposal for a standard interface to **register** an AI agent on-chain and to record the outcome of **verification** processes intended to help users assess an agent’s trustworthiness.

## What it proposes

From the draft text, ERC-8126 centers on:

- **Self-registration** of an agent with basic metadata (e.g., name, description, agent-controlled wallet address, and an HTTPS URL endpoint).
- A set of **verification types** intended to evaluate different risk surfaces:
  - **ETV** (Ethereum Token Verification): checks a provided contract address.
  - **SCV** (Staking Contract Verification): checks a provided staking contract address.
  - **WAV** (Web Application Verification): checks the agent’s web endpoint.
  - **WV** (Wallet Verification): checks the agent wallet’s on-chain profile / reputation inputs.
- A **risk score** output expressed as a number from **0–100** (as described in the draft), intended to make results easier to compare across agents.
- An architecture where verification logic is largely **off-chain**, with results summarized on-chain.
- A privacy-oriented step called **PDV (Private Data Verification)** that produces **zero-knowledge proofs (ZKPs)** so that verification can be attested without broadly exposing underlying sensitive details.

## Status and where to follow

- **Status:** Draft (per the ERC header).
- Discussion thread: Fellowship of Ethereum Magicians (Ethereum Magicians).

## Sources

- Draft specification (raw): https://raw.githubusercontent.com/ethereum/ERCs/master/ERCS/erc-8126.md
- Discussion: https://ethereum-magicians.org/t/erc-8126-ai-agent-registration-and-verification/27445
