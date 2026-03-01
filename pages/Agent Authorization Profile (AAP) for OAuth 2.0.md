# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that profiles how to use **OAuth 2.0** and **JSON Web Tokens (JWTs)** for **agent-to-API** (machine-to-machine) scenarios, where an autonomous or semi-autonomous agent acts under an operator's authority. It introduces **structured JWT claims** and **resource-server validation rules** so systems can make authorization decisions that are more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as work in progress. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

OAuth deployments often rely on coarse signals like `scope` and `aud`. AAP targets cases where that is not expressive enough for agentic systems that:

- operate at high frequency,
- may act without a human present at execution time,
- need their authority to be explainable and enforceable at the API.

The draft frames this as a need for **explicit identity**, **task binding**, **capability constraints**, **delegation traceability**, and **oversight intent**. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## When you might want AAP

Typical needs include:

- **Task binding**: make the intended task/purpose explicit to reduce purpose drift. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Capability-style authorization**: express permitted actions with structured constraints (beyond coarse scopes). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation clarity**: represent multi-hop on behalf of flows and privilege reduction across tools/sub-agents. AAP references OAuth Token Exchange for delegation/impersonation semantics and the `act` (actor) claim. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ https://www.rfc-editor.org/rfc/rfc8693
- **Contextual constraints**: encode restrictions like time windows, network/domain limits, or rate limits in a machine-checkable way. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight signals**: carry policy intent that some actions require human approval/supervision (enforcement is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container commonly used as an access token format. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** provides a standardized way to exchange tokens, including for **delegation** and **impersonation** scenarios, and defines the `act` (actor) claim to represent an actor chain. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP references both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR, RFC 9396)** define the `authorization_details` parameter for carrying fine-grained, structured authorization data in OAuth messages; AAP positions this as complementary to capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds: a structured claim profile

AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting)
- **Task context** (what the token is for)
- **Capabilities and constraints** (what actions are permitted, under what conditions)
- **Delegation chain semantics** (how authority was passed or reduced across hops)
- **Oversight requirements** (policy signals about required approvals/supervision)
- **Contextual restrictions** (environment/network/time)
- **Audit correlation** (trace/session identifiers)

## AAP claim sections (draft claim names)

The draft defines named structured sections (schemas) for agent-specific authorization context. The normative claim names include: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

- `aap_agent`  agent identity and execution context
- `aap_task`  task identifier/purpose/topic/sensitivity
- `aap_capabilities`  actions plus constraints
- `aap_oversight`  oversight/approval intent
- `aap_delegation`  delegation metadata (may be used alongside the Token Exchange `act` claim)
- `aap_context`  environment/network/time restrictions
- `aap_audit`  trace/session identifiers for logging correlation

## Delegation vs. impersonation (why it matters)

Token Exchange distinguishes:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity (often with additional constraints).

RFC 8693 defines the `act` (actor) claim to represent the current actor and (optionally) a nested actor chain. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making agent/task/capability semantics explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Security notes (high-level)

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift**: using a token beyond its declared task/purpose. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Confused deputy** and other multi-hop delegation failures. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Replay risk** in high-automation environments when bearer tokens leak; PoP mechanisms like mTLS-bound access tokens or DPoP reduce replay by sender-constraining the token. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. Agent Authorization Profile (AAP) for OAuth 2.0 (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- RFC 6749. The OAuth 2.0 Authorization Framework. https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. JSON Web Token (JWT). https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. OAuth 2.0 Token Exchange. https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens. https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. JSON Web Token Best Current Practices. https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. OAuth 2.0 Rich Authorization Requests. https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. OAuth 2.0 Demonstrating Proof of Possession (DPoP). https://www.rfc-editor.org/rfc/rfc9449
