# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** scenarios, especially where autonomous or semi-autonomous agents act on behalf of a principal. The draft’s goal is to make authorization more **explicit**, **auditable**, and **policy-enforceable** by standardizing additional structured token content (claims) and validation rules. (IETF Datatracker: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/)

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. (IETF Datatracker: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/)

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems. Typical needs include:

- **Task binding**: what task, objective, or workflow step the token is intended for.
- **Capability-style authorization**: what actions are allowed, possibly with structured constraints.
- **Delegation clarity**: whether an agent is acting *as* someone (impersonation) vs *on behalf of* someone (delegation), and how authority was derived.
- **Operational constraints**: limits such as time bounds, environment restrictions, or rate limits.
- **Oversight signals**: when human approval or supervision is required.

These are the kinds of questions that become operationally important when agents can plan multi-step actions and call multiple downstream APIs.

## Relationship to OAuth 2.0 and JWT building blocks

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. (RFC 6749: https://datatracker.ietf.org/doc/html/rfc6749)
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. (RFC 7519: https://www.rfc-editor.org/rfc/rfc7519)
- **OAuth 2.0 Token Exchange** is a common fit for delegation and “act-as / on-behalf-of” patterns that show up in agent architectures. (RFC 8693: https://www.rfc-editor.org/rfc/rfc8693)
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens; **DPoP** is one standardized mechanism. (RFC 9449: https://www.rfc-editor.org/rfc/rfc9449)
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages. (RFC 9396: https://datatracker.ietf.org/doc/html/rfc9396)

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so that resource servers can reason about:

- **Agent identity / metadata**: which software entity is acting.
- **Task context**: what the agent is trying to do.
- **Capabilities and constraints**: what is permitted, and under what conditions.
- **Delegation chain semantics**: how authority was passed or restricted across hops.
- **Oversight requirements**: signals that certain operations require approval or supervision.

The exact claim names, structures, and processing rules are defined in the draft itself. (IETF Datatracker: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/)

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them. (RFC 8693: https://www.rfc-editor.org/rfc/rfc8693)

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers.

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift**: tokens or delegated authority being reused beyond their intended task.
- **Confused deputy** failures in multi-hop delegation chains.
- **Replay risk** when bearer tokens are used in high-automation environments.

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. (RFC 8725: https://www.rfc-editor.org/rfc/rfc8725)

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://datatracker.ietf.org/doc/html/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://datatracker.ietf.org/doc/html/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
