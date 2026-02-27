# Agent Authorization Profile (AAP) for OAuth 2.0

The **Agent Authorization Profile (AAP) for OAuth 2.0** is an Internet-Draft that proposes an **OAuth 2.0** and **JSON Web Token (JWT)** profile intended to support **secure, auditable, and context-aware authorization for autonomous AI agents**. The draft describes additional JWT claim structures and validation expectations to help resource servers reason about an agent’s identity, the task context to which a token is bound, delegated authority, and any human-oversight requirements.

## Overview

OAuth 2.0 deployments commonly rely on coarse-grained *scopes* to express authorization. AAP argues that autonomous agents introduce additional requirements—such as high-frequency actions, context-dependent risk, and delegation across tools—that benefit from more structured token semantics than scopes alone.

AAP is designed to be used within standard OAuth roles:

- **Authorization Server (AS)** issues access tokens following OAuth 2.0.
- **Resource Server (RS)** validates tokens and enforces policy.
- The **client** is an autonomous agent acting on behalf of an operator.

The draft positions AAP as a profile that **reuses existing standards** (OAuth 2.0, JWT, token exchange, proof-of-possession) while defining a set of structured claims and associated validation rules.

## Token model

AAP assumes access tokens are JWTs and extends standard JWT claims (e.g., `iss`, `sub`, `aud`, `exp`, `iat`, `jti`) with additional, structured claim sections.

The draft’s normative claim names are:

- `aap_agent` — agent identity and execution context
- `aap_task` — task binding and declared purpose
- `aap_capabilities` — permitted actions with constraints
- `aap_oversight` — human oversight / approval requirements
- `aap_delegation` — delegation metadata (optionally alongside standard delegation mechanisms)
- `aap_context` — contextual restrictions (e.g., time, network)
- `aap_audit` — audit and trace correlation identifiers

## Relationship to existing standards

AAP is described as compatible with, and intended to be deployed alongside, several existing OAuth-related standards:

- **OAuth 2.0** for token issuance and the AS/RS architecture.
- **JWT** for access token representation.
- **OAuth 2.0 Token Exchange (RFC 8693)** for delegation and privilege reduction.
- **Proof-of-possession mechanisms** such as **mTLS** and **DPoP** to reduce token replay risk.
- **SPIFFE/SPIRE** workload identity, where an agent identifier may be expressed as a SPIFFE ID in deployments that already use SPIFFE.

## Use cases

The draft is framed around environments where an operator authorizes an agent to perform actions against APIs, potentially involving:

- Binding tokens to a specific task or purpose so that access can be evaluated in context.
- Expressing authorization as constrained capabilities rather than only scopes.
- Enabling auditable delegation chains across tools or sub-agents.
- Declaring human-approval requirements for sensitive operations.

## Status

AAP is published as an **IETF Internet-Draft** and is subject to change. Internet-Drafts are not standards; they may be updated, replaced, or obsoleted at any time.

## See also

- OAuth 2.0
- JSON Web Token (JWT)
- OAuth 2.0 Token Exchange (RFC 8693)
- DPoP (RFC 9449)
- Mutual TLS for OAuth (RFC 8705)
- SPIFFE

## References

- IETF Datatracker. *Agent Authorization Profile (AAP) for OAuth 2.0 (draft-aap-oauth-profile).* https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF. *Agent Authorization Profile (AAP) for OAuth 2.0 (draft-aap-oauth-profile-00).* https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- Hardt, D. *The OAuth 2.0 Authorization Framework (RFC 6749).* IETF, 2012. https://www.rfc-editor.org/rfc/rfc6749
- Jones, M., Bradley, J., Sakimura, N. *JSON Web Token (JWT) (RFC 7519).* IETF, 2015. https://www.rfc-editor.org/rfc/rfc7519
- Campbell, B., Bradley, J., Sakimura, N., Tschofenig, H. *OAuth 2.0 Token Exchange (RFC 8693).* IETF, 2020. https://www.rfc-editor.org/rfc/rfc8693
- Fett, D., Campbell, B., Bradley, J., Lodderstedt, T., Jones, M. *OAuth 2.0 Demonstrating Proof of Possession (DPoP) (RFC 9449).* IETF, 2023. https://www.rfc-editor.org/rfc/rfc9449
- Campbell, B., Bradley, J., Sakimura, N., Jones, M. *OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705).* IETF, 2020. https://www.rfc-editor.org/rfc/rfc8705
- The SPIFFE Project. *SPIFFE.* https://spiffe.io/
