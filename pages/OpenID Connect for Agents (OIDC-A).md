# OpenID Connect for Agents (OIDC-A)

**OpenID Connect for Agents (OIDC-A)** is a proposed extension to **OpenID Connect (OIDC)** intended to represent, authenticate, and authorize **LLM-based software agents** within the existing **OAuth 2.0 / OIDC** ecosystem. It introduces agent-specific identity claims and mechanisms for expressing **delegation chains**, **attestation evidence**, and **capability-oriented authorization**, while aiming to remain compatible with existing OIDC infrastructure.

## Overview

OIDC and OAuth 2.0 were originally designed around human end-users and conventional client applications. OIDC-A proposes additional protocol elements for agentic systems, where an agent may act on behalf of a user (or another agent), potentially across multiple delegation steps.

In the OIDC-A proposal, relying parties can use agent-specific claims to make authorization decisions based on attributes such as the agent’s provider, model, and declared capabilities, and can validate transitive authority using a structured delegation chain.

## Proposed mechanisms

The arXiv specification proposal describes several extensions to OpenID Connect, including:

- **Agent identity claims**: additional standard claims intended to identify an agent and its characteristics (for example, agent type, provider, model, version, and instance identifiers).
- **Delegation and authority representation**: claims and validation rules intended to represent a chain of delegated authority from an original delegator through intermediate agents.
- **Attestation support**: mechanisms intended to carry or reference attestation evidence so that relying parties can evaluate integrity and provenance claims.
- **Capability discovery and authorization**: a capability-oriented approach to expressing what an agent can do, and to enabling fine-grained authorization.

## Relationship to other agent interoperability work

OIDC-A has been discussed in the broader context of emerging agent interoperability and governance work, where identity, authorization, and auditability are treated as prerequisites for deploying autonomous agents at scale.

## References

- Subramanya Nagabhushanaradhya. *OpenID Connect for Agents (OIDC-A) 1.0: A Standard Extension for LLM-Based Agent Identity and Authorization*. arXiv:2509.25974 (2025). https://arxiv.org/abs/2509.25974
- OpenID Foundation. *New whitepaper tackles AI agent identity challenges* (announcing the whitepaper *Identity Management for Agentic AI*). https://openid.net/new-whitepaper-tackles-ai-agent-identity-challenges/
