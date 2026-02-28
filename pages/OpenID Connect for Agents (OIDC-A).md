# OpenID Connect for Agents (OIDC-A)

**OpenID Connect for Agents (OIDC-A)** is a proposed extension to **OpenID Connect (OIDC)** intended to represent, authenticate, and authorize **LLM-based software agents** within the existing **OAuth 2.0 / OIDC** ecosystem.

It introduces agent-specific identity and authorization concepts such as:

- **Agent identity claims** (e.g., provider, model, version, instance identifiers)
- **Delegation chains** (representing transitive “act on behalf of” authority)
- **Attestation evidence** (cryptographic evidence about an agent’s integrity/origin)
- **Capability-oriented authorization** (expressing what an agent can do)

Primary reference: Subramanya Nagabhushanaradhya, *OpenID Connect for Agents (OIDC-A) 1.0* (arXiv:2509.25974). https://arxiv.org/abs/2509.25974

## What problem is OIDC-A trying to solve?

OIDC and OAuth 2.0 were designed primarily around:

- **End-users** authenticating to an **Authorization Server**
- **Clients** obtaining tokens to access **Resource Servers** with user consent

OAuth 2.0 explicitly describes delegated authorization as “limited access … **on behalf of a resource owner**” (RFC 6749). https://datatracker.ietf.org/doc/html/rfc6749

OpenID Connect adds an identity layer on top of OAuth 2.0, using an **ID Token** (typically a JWT) to convey **claims** about an authenticated end-user. https://openid.net/specs/openid-connect-core-1_0.html

Agentic systems stress these models because an “agent” may:

- act with varying autonomy,
- operate in multi-hop delegation chains,
- need to present verifiable evidence about its runtime and provenance,
- require authorization decisions based on agent attributes (not just user identity).

OIDC-A proposes new claims and supporting endpoints to help relying parties make these decisions in a way that remains compatible with existing OIDC infrastructure. https://arxiv.org/html/2509.25974v1

## Core ideas in the proposal

### Agent identity claims

OIDC-A defines **agent-specific claims** intended to be carried in tokens “issued to or about agents” (e.g., ID Tokens), including identifiers and descriptive attributes such as **agent provider**, **model**, **version**, and **instance ID**. https://arxiv.org/html/2509.25974v1

Practical motivation: relying parties often need to know *which* agent they are interacting with (and which organization is accountable for it) before granting access.

### Delegation and authority representation

OIDC-A introduces claims intended to represent “who delegated to whom” and to capture the full **delegation chain**.

In the proposal, a delegation chain is represented as a JSON array of delegation steps (chronologically ordered), and relying parties validate properties such as:

- trusted issuers,
- linkage between steps,
- scope reduction,
- constraint enforcement.

https://arxiv.org/html/2509.25974v1

This is meant to support cases where an agent is acting on behalf of a user *through* intermediate agents, and the relying party wants to reason about transitive authority.

### Attestation evidence

The proposal discusses carrying or referencing **attestation evidence** so that relying parties can evaluate integrity/provenance claims about an agent. It also notes compatibility with IETF remote attestation work such as **RATS** and **Entity Attestation Tokens (EAT)**. https://arxiv.org/html/2509.25974v1

### Capability discovery and authorization

OIDC-A proposes a capability-oriented approach to expressing what an agent can do (for example via an **agent_capabilities** claim), along with discovery mechanisms and dedicated endpoints for capability discovery / attestation verification. https://arxiv.org/html/2509.25974v1

## Relationship to broader identity work for agents

The OpenID Foundation’s AI Identity Management Community Group has published a whitepaper arguing that as agents become more autonomous and operate across domains, identity and authorization systems will need to evolve to support concepts like delegated authority chains and agent lifecycle governance.

- Announcement: https://openid.net/new-whitepaper-tackles-ai-agent-identity-challenges/

## References

- Subramanya Nagabhushanaradhya. *OpenID Connect for Agents (OIDC-A) 1.0: A Standard Extension for LLM-Based Agent Identity and Authorization*. arXiv:2509.25974 (2025). https://arxiv.org/abs/2509.25974
- OIDC-A HTML: https://arxiv.org/html/2509.25974v1
- OAuth 2.0 Authorization Framework (RFC 6749). https://datatracker.ietf.org/doc/html/rfc6749
- OpenID Connect Core 1.0 (errata set 2). https://openid.net/specs/openid-connect-core-1_0.html
- OpenID Foundation. *New whitepaper tackles AI agent identity challenges*. https://openid.net/new-whitepaper-tackles-ai-agent-identity-challenges/
