---
title: Agentic Commerce Protocol (ACP)
description: An open standard for enabling programmatic commerce flows between AI agents, buyers, merchants, and payment providers.
---

# Agentic Commerce Protocol (ACP)

The **Agentic Commerce Protocol (ACP)** is an open standard and interaction model intended to enable **programmatic commerce** between a buyer’s **AI agent**, **merchants**, and **payment providers**, so that purchases can be initiated and completed through agent-driven flows while merchants remain the seller of record. The ACP specification is maintained in an open-source repository and is described as being stewarded by **OpenAI** and **Stripe**.

## Overview

ACP defines a set of common patterns and interfaces for agent-mediated checkout, including:

- Merchant-facing APIs for creating and managing checkout sessions and orders.
- Mechanisms for transmitting payment credentials via delegated or tokenized payment flows.
- Versioned specifications (date-based snapshots) and accompanying schemas/examples to support interoperable implementations.

OpenAI’s developer documentation describes ACP as open source (Apache 2.0 licensed) and positions it as the protocol underlying “Instant Checkout” experiences in ChatGPT.

## Specification and versioning

The ACP specification is published as a versioned set of artifacts. The upstream repository describes **date-based versioning** (e.g., `YYYY-MM-DD`) where each dated directory represents a snapshot of the specification at release time, alongside an `unreleased/` area for ongoing development.

The repository includes multiple forms of specification material, including:

- Human-readable RFC documents.
- Machine-readable API definitions (OpenAPI).
- Data model definitions (JSON Schema).
- Example requests and responses.

## Governance and maintenance

The upstream ACP repository states that the project is maintained by OpenAI and Stripe, and includes governance documentation describing a maintainer model and contribution processes (including templates and a contributor license agreement).

## Relationship to agent ecosystems

ACP is part of a broader trend toward standardizing interfaces that let autonomous or semi-autonomous agents transact with external services. In this framing, ACP focuses on **commerce and checkout** interoperability (merchants, payment providers, and agent surfaces), complementing other standards that focus on **tool invocation** or **agent-to-agent communication**.

## References

- Agentic Commerce Protocol (ACP) GitHub repository: https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- OpenAI Developers — Agentic Commerce Protocol “Get started”: https://developers.openai.com/commerce/guides/get-started/
