# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an Internet-Draft that proposes an authorization profile for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in scenarios where **autonomous AI agents** access APIs on behalf of a principal or system. The draft describes structured JWT claims and validation rules intended to make agent-to-API authorization more **context-aware**, **auditable**, and amenable to **policy enforcement** (for example, by binding tokens to tasks, constraining permitted actions, and recording delegation chains).[1]

Because AAP is published as an **IETF Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and are not intended to be cited as stable references.[1]

## Overview

The AAP draft frames agent authorization as an application of existing building blocks—OAuth 2.0, JWTs, OAuth Token Exchange, and proof-of-possession mechanisms—rather than a new protocol. It specifies additional token content and processing expectations so that authorization systems can reason about:

- **Agent identity** and related metadata
- **Task context** (what the agent is trying to do)
- **Operational constraints** (limits that narrow how the token may be used)
- **Delegation chains** (how authority is derived or passed along)
- **Human oversight requirements** (conditions under which a human must approve or supervise actions)[1]

## Relationship to OAuth and JWT

In OAuth deployments, access tokens are often treated as bearer tokens with limited built-in semantics beyond scope and audience. The AAP draft proposes a more structured approach using JWT claims so that resource servers can apply **validation rules** and enforce **capabilities and constraints** consistently across services.[1]

The draft explicitly positions AAP as a profile layered on top of existing standards, aiming to improve interoperability for agentic use cases without changing the underlying OAuth flows.[1]

## Delegation and constraints

A recurring theme in the draft is reducing the risk of overbroad or drifting agent permissions. It describes mechanisms for expressing and validating:

- **Delegation constraints**, such as limiting the depth or breadth of delegation
- **Time- and environment-based restrictions**
- **Data and security constraints**
- **Audit and trace propagation** to support accountability and incident response[1]

## Threat model and security considerations

The draft includes a threat model summary that discusses risks relevant to autonomous agents, including agent impersonation, capability escalation, excessive delegation, and prompt/data injection. It also describes resource server validation expectations and broader security considerations for authorization servers and token handling.[1]

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)

## References

1. A. Cruz. "Agent Authorization Profile (AAP) for OAuth 2.0" (Internet-Draft), draft-aap-oauth-profile-01, 7 February 2026. IETF Datatracker. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ (accessed 2026-02-27).
