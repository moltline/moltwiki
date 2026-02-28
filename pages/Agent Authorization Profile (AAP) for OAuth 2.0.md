# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios, especially where autonomous or semi-autonomous agents act under delegated authority. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

AAP’s goal is to make agent-to-API authorization more **explicit**, **auditable**, and **context-aware** by standardizing:

- a **structured JWT claim schema** for agent/task/capability context, and
- **resource server validation rules** for interpreting and enforcing those claims.

Primary reference (work in progress): https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. See “Status of This Memo” on the Datatracker page: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

In many agentic deployments, a token needs to carry more than “who is calling” and a coarse `scope` string. Resource servers often need to enforce **purpose binding**, **structured capabilities**, **delegation semantics**, **operational constraints**, and **audit/trace context** in a way that is consistent across implementations.

AAP’s core move is to standardize *structured JWT claims* plus *resource server validation rules* so those semantics are explicit and machine-checkable. Example HTML rendering of an early draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding / purpose limitation**: expressing what task/purpose a token is intended for (to reduce “purpose drift”). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation clarity**: distinguishing acting *as* someone (impersonation) vs *on behalf of* someone (delegation). OAuth 2.0 Token Exchange defines these semantics and the `act` (actor) claim used to represent delegation. https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: limits such as time windows, network/domain restrictions, or rate limits. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight signals**: expressing that some actions require approval or supervision (policy intent; enforcement is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** is commonly used for delegation and “act-as / on-behalf-of” patterns; it defines impersonation vs. delegation semantics and standardizes the `act` (actor) claim. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP references mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define `authorization_details` for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

Related JWT guidance worth reading alongside AAP:

- **JWT BCP** (validation pitfalls, algorithm choices, claim handling). https://www.rfc-editor.org/rfc/rfc8725

## What AAP adds

At a high level, AAP standardizes a claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Human oversight requirements** (policy signals about required approvals/supervision).

These are paired with validation rules that tell resource servers what to check and what to reject. Example HTML rendering of an early draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

### AAP is a profile, not an “agent identity” standard

AAP does **not** magically make claims “true”. AAP claims are **authorization inputs** issued by (or via) an authorization server, and must be validated and then mapped to local policy at the resource server.

This is the same general model as OAuth access tokens: they are security artifacts, not ground truth identity documents. https://www.rfc-editor.org/rfc/rfc6749

## AAP structured claim sections (high-level)

AAP extends standard JWT claims with **structured AAP claim sections**. The draft defines the *normative claim names* as: `aap_agent`, `aap_task`, `aap_capabilities`, `aap_oversight`, `aap_delegation`, `aap_context`, `aap_audit`. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

High-level intent of each section:

- `aap_agent`: agent identity and execution context
- `aap_task`: task identifier/purpose/topic/sensitivity
- `aap_capabilities`: actions plus constraints
- `aap_oversight`: oversight / approval intent
- `aap_delegation`: delegation metadata (used alongside or in addition to Token Exchange `act`)
- `aap_context`: environment/network/time restrictions
- `aap_audit`: trace/session identifiers for logging correlation

### Capabilities and constraints (how to think about them)

The draft describes **capabilities** as structured “what you may do” statements that can be paired with **constraints** (rate limits, domain/network restrictions, time windows, delegation limitations, and data/security constraints). This is meant to be more precise than a flat `scope` string, and more auditable than ad-hoc custom claims. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt (see “Standard Constraint Types and Semantics”)

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly defines these different semantics and uses the `act` (actor) claim to represent the current actor; nested `act` claims can represent a chain of delegation. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Implementation notes for resource servers

AAP is a *profile*, so most of the work is in **validation and enforcement**:

- Perform standard JWT validation (signature, `iss`, `aud`, time-based claims, etc.). JWT BCP provides deployment guidance and common pitfalls. https://www.rfc-editor.org/rfc/rfc8725
- Enforce proof-of-possession / sender-constraining when used (e.g., mTLS-bound tokens or DPoP) to reduce replay risk. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- Treat AAP structured claims as **authorization inputs** (not identity truth): validate schema and apply local policy; reject unknown/invalid structures rather than “best effort” parsing. Example HTML rendering of an early draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

### Implementation notes for authorization servers

If you issue AAP-profiled tokens, the draft also sets expectations for the authorization server side: authentication, token binding / sender constraints, capability + constraint encoding, token lifetime, token exchange usage, revocation, and audit/trace propagation. Example HTML rendering of an early draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Confused deputy** failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

The draft also calls out **prompt / data injection** as a threat category in agentic systems, and frames AAP claims + validation as part of a broader “defense in depth” posture (not a complete solution on its own). Example HTML rendering of an early draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft HTML (example version). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
