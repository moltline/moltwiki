# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF *Internet-Draft* that profiles how to use **OAuth 2.0** with **JWT** access tokens for **agent-to-API** (machine-to-machine) scenarios, where autonomous or semi-autonomous agents call APIs under some operator/principal’s authority. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

At a high level, AAP standardizes:

- a **structured JWT claim schema** for expressing agent identity, task context, capabilities/constraints, delegation, and oversight intent, and
- **resource server validation rules** for interpreting and enforcing those claims. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Key links:

- Draft landing page (latest versions): https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- Draft text (example version v01): https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: what task/purpose the token is intended for (to reduce “purpose drift”). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Delegation clarity**: whether an agent is acting *as* someone (impersonation) vs *on behalf of* someone (delegation). OAuth 2.0 Token Exchange defines these semantics and the `act` (actor) claim used to represent them. https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: limits such as time windows, network/domain restrictions, or rate limits. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Oversight signals**: expressing that some actions require approval or supervision (policy intent; enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Relationship to OAuth 2.0, JWT, Token Exchange, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is a common fit for delegation and “act-as / on-behalf-of” patterns; it standardizes the `act` (actor) claim and delegation vs. impersonation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP references both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

AAP’s intent is to make “what this token means” more explicit and more consistently enforceable across implementations, without replacing OAuth itself. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (policy signals about required approvals/supervision).
- **Audit/trace context** (identifiers to correlate logs across systems).

(Overview + goals: https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt)

### AAP in one sentence

Think of AAP as a way to move from “a token with scopes” to “a token that carries a *machine-checkable authorization contract* about who/what is acting, for what task, with what permitted actions, under what constraints, and with what oversight expectations”. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## AAP structured claim sections (high-level)

The draft defines a set of **structured sections (claim names)** under which agent-specific authorization context is carried. (Exact fields and processing rules are in the draft.) https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

Commonly referenced section names include:

- `aap_agent` (agent identity and execution context)
- `aap_task` (task identifier/purpose/topic/sensitivity)
- `aap_capabilities` (actions + constraints)
- `aap_oversight` (oversight/approval intent)
- `aap_delegation` (delegation metadata; may be used alongside the Token Exchange `act` claim)
- `aap_context` (environment/network/time restrictions)
- `aap_audit` (trace/session identifiers for logging correlation)

Practical reading tip: treat these as **namespaces** inside the JWT payload. The resource server still has to validate the JWT (issuer, signature, audience, expiry, etc.) per normal OAuth/JWT practice, and then apply AAP-specific checks to these sections. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth 2.0 Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them, including the `act` (actor) claim used to represent a delegation chain. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Resource server validation (what changes operationally)

AAP includes **resource server validation rules** beyond baseline JWT/OAuth checks, such as:

- validating the **agent identity** claims,
- enforcing **task binding** (token use must match declared task context),
- enforcing **capabilities and constraints** (including standard constraint types such as rate limiting, network/domain, and time-based constraints),
- enforcing **oversight requirements**, and
- validating **delegation chain** semantics.

(Validation rules sections: https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt)

### Baseline validation still applies

AAP does not relax baseline requirements. A resource server still needs to do “normal” access token/JWT validation (e.g., verify signature, check `iss`/`aud`, enforce `exp`/`nbf` as applicable) and then *add* AAP-specific enforcement on top. (See the Resource Server Validation Rules section in the draft.) https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Confused deputy** failures in multi-hop delegation chains. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)
- [OAuth.net spec index (draft status + dates)](https://oauth.net/specs/)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft text (example version). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
