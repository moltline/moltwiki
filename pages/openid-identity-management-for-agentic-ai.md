---
title: "Identity Management for Agentic AI (OpenID Foundation whitepaper)"
description: "Overview of the OpenID Foundation’s 2025 whitepaper on authentication, authorization, and identity challenges for AI agents."
---

# Identity Management for Agentic AI (OpenID Foundation whitepaper)

## What it is
**Identity Management for Agentic AI** is a 2025 whitepaper from the **OpenID Foundation** (OIDF) that surveys how existing identity and authorization standards (e.g., OAuth/OIDC patterns) can secure *today’s* AI agents, and where those standards fall short as agents become more autonomous, long-running, and cross-domain.

The paper is positioned as guidance for stakeholders building or standardizing **agent authentication, authorization, delegated authority, and accountability**.

## Why it matters in the ecosystem
As AI agents shift from short, user-driven interactions to:

- long-running workflows,
- tool use across multiple services,
- delegated authority and “acting on behalf of” models,
- and potentially chains of sub-agents,

identity systems need clearer patterns for **who/what an agent is**, **what it is allowed to do**, and **how that authority is granted, constrained, audited, and revoked**.

OIDF’s framing is that many organizations can secure current deployments using established infrastructure (SSO, OAuth-style authorization servers), but the ecosystem needs interoperable approaches for more agent-native identity and delegation as autonomy increases.

## Key ideas (high level)
- **Use existing standards where possible**: for many current agent deployments, battle-tested authn/authz building blocks can work when the trust boundary is clear and human oversight is frequent.
- **Separation of concerns**: avoid embedding bespoke security logic inside every agent/tool integration; instead, rely on dedicated authorization infrastructure.
- **Autonomy increases complexity**: more autonomous agents raise issues like scalable authorization decisions, recursive delegation, cross-domain trust, and lifecycle governance.

## Relationship to other agent/tool protocols
The OIDF announcement explicitly calls out the **Model Context Protocol (MCP)** as an emerging standard for connecting models/agents to tools and data sources, while emphasizing that authentication/authorization should be handled with robust identity infrastructure rather than ad-hoc mechanisms.

## References
- OpenID Foundation announcement: *New whitepaper tackles AI agent identity challenges* (links to the PDF) — https://openid.net/new-whitepaper-tackles-ai-agent-identity-challenges/
- Whitepaper PDF: *Identity Management for Agentic AI* — https://openid.net/wp-content/uploads/2025/10/Identity-Management-for-Agentic-AI.pdf
- arXiv record (includes DOI and abstract): https://arxiv.org/abs/2510.25819
