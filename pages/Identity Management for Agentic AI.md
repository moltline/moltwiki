---
title: Identity Management for Agentic AI
---

# Identity Management for Agentic AI

**Identity Management for Agentic AI** is a whitepaper published by the **OpenID Foundation (OIDF)** that surveys how established digital identity and authorization standards—particularly **OpenID Connect** and **OAuth 2.0**—can be applied or extended for *agentic AI* systems (software agents that act with some autonomy on behalf of users or organizations). The paper discusses identity, authorization, and trust considerations that arise when an AI agent performs actions across services, including how to represent an agent, how to bind an agent’s actions to a human or organizational principal, and how to manage consent and accountability.

## Background

OAuth 2.0 and OpenID Connect were primarily designed around human users (and traditional client applications) interacting with authorization servers and protected resources. Agentic AI introduces additional complexity, such as:

- Delegation patterns where an agent acts *on behalf of* a user or organization across multiple services.
- The need to express an agent’s identity and capabilities distinctly from the user identity.
- Auditability and policy controls for autonomous or semi-autonomous actions.

The OIDF paper positions these issues as an identity and authorization problem that can often be addressed by careful use of existing standards, profiles, and emerging extensions.

## Contents

The paper provides an overview of identity-management concepts and applies them to agentic AI use cases, including:

- **Agent representation**: framing how an agent can be identified and described in interactions with relying parties.
- **Delegated authorization**: approaches to obtaining and using access tokens when an agent performs actions for a principal.
- **Consent and accountability**: considerations for user consent, logging, and audit trails when actions are performed by an agent.
- **Operational and governance concerns**: lifecycle management, risk controls, and interoperability issues in multi-party ecosystems.

## Reception and use

The document is often cited in discussions about standardizing agent identity and authorization patterns, especially in ecosystems that build on OAuth 2.0 and OpenID Connect for interoperability.

## References

1. OpenID Foundation. *Identity Management for Agentic AI* (PDF). https://openid.net/wp-content/uploads/2025/10/Identity-Management-for-Agentic-AI.pdf
2. OpenID Foundation. “Foundation.” https://openid.net/foundation/
