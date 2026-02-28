# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an **IETF Internet-Draft** that profiles how to use **OAuth 2.0** and **JWT** access tokens for **agent-to-API (M2M)** scenarios, where autonomous or semi-autonomous agents act for an operator/principal. It introduces a **structured JWT claim schema** plus **resource-server validation rules** so systems can make authorization decisions that are more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

In agentic systems, relying solely on conventional OAuth fields like `scope` and `aud` often leaves key questions implicit:

- What *task/purpose* is this token intended for?
- What *actions* are permitted, with what *constraints*?
- Is the caller acting *as* someone (impersonation) or *on behalf of* someone (delegation)?
- Are there environment/operational restrictions (time, network, domain)?
- Are there oversight requirements (e.g., approval needed)?

AAP standardizes how to express and validate these semantics in tokens. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to existing standards

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (STS)** is a common fit for delegation and “act-as / on-behalf-of” patterns; it defines both delegation and impersonation semantics and standardizes the `act` (actor) claim used to represent an actor/delegation chain. https://www.rfc-editor.org/rfc/rfc8693.html
- **Sender-constrained / proof-of-possession (PoP) tokens** reduce replay risk compared to bearer tokens. AAP references both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449.html
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages; AAP can complement this capability-style approach on the token/validation side. https://www.rfc-editor.org/rfc/rfc9396

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: what task/purpose the token is intended for (to reduce “purpose drift”). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation clarity**: distinguishing impersonation vs delegation; Token Exchange defines these semantics and the `act` claim. https://www.rfc-editor.org/rfc/rfc8693.html
- **Operational / contextual constraints**: limits such as time windows, network/domain restrictions, or rate limits. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight signals**: expressing that some actions require approval or supervision (policy intent; enforcement is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (policy signals about required approvals/supervision).

These are paired with **resource server validation rules** (e.g., task binding validation, capability enforcement, delegation chain validation, PoP validation, and audit/trace propagation). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## AAP structured claim sections (high-level)

The draft defines a set of structured claim “sections” (namespaces) to carry agent-specific authorization context. The exact fields and processing rules are in the draft; at a high level the sections include:

- `aap_agent` (agent identity and execution context)
- `aap_task` (task identifier/purpose/topic/sensitivity)
- `aap_capabilities` (actions + constraints)
- `aap_oversight` (oversight/approval intent)
- `aap_delegation` (delegation metadata; may be used alongside Token Exchange’s `act` claim)
- `aap_context` (environment/network/time restrictions)
- `aap_audit` (trace/session identifiers for logging correlation)

(Example section list and schemas appear in the draft text.) https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them, including the `act` (actor) claim used to represent an actor/delegation chain. https://www.rfc-editor.org/rfc/rfc8693.html

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Confused deputy** failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449.html

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 8693 (OAuth 2.0 Token Exchange)](RFC%208693%20(OAuth%202.0%20Token%20Exchange).md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft text (example version). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693.html
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449.html
