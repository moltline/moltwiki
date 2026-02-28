# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF *Internet-Draft* that defines an authorization profile for using **OAuth 2.0** with **JWT-based** access tokens in **agent-to-API** (machine-to-machine) scenarios, with explicit support for **delegation chains**, **task binding**, **operational constraints**, and **oversight signals**. It does not introduce a new protocol; it profiles how to use OAuth 2.0, JWT, Token Exchange, and proof-of-possession mechanisms in a way that is more **auditable** and **context-aware** for autonomous / semi-autonomous agents. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: expressing what task/purpose the token is intended for (to reduce “purpose drift”). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Delegation clarity**: distinguishing *impersonation* (“act as”) vs *delegation* (“act on behalf of”). OAuth 2.0 Token Exchange defines these semantics and related token structures. https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: limits such as time windows, domain/network restrictions, or rate limits. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Oversight signals**: expressing that some actions require approval/supervision (policy intent; enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Relationship to OAuth 2.0, JWT, Token Exchange, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container commonly used as an access token format. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** is a common fit for delegation and “act-as / on-behalf-of” patterns; it defines a protocol for obtaining tokens representing impersonation and delegation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP discusses using mutual-TLS certificate-bound access tokens (RFC 8705) and DPoP (RFC 9449). https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds

At a high level, AAP standardizes:

- a **structured JWT claim schema** for agent-specific authorization context, and
- **resource-server validation rules** for interpreting and enforcing those claims.

The draft’s stated goal is to help systems reason about agent identity, task context, operational constraints, delegation chains, and oversight requirements in a consistent way. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## AAP structured claim sections (high-level)

AAP defines a set of structured claim “sections” (top-level claim names), including:

- `aap_agent` (agent identity and execution context)
- `aap_task` (task identifier/purpose/topic/sensitivity)
- `aap_capabilities` (actions + constraints)
- `aap_oversight` (oversight/approval intent)
- `aap_delegation` (delegation metadata)
- `aap_context` (environment/network/time restrictions)
- `aap_audit` (trace/session identifiers for logging correlation)

(See Section 5.2 “Structured Sections (Claim Names)”.) https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth 2.0 Token Exchange explicitly calls out these different semantics and defines a protocol for obtaining tokens representing them. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Validation and security notes (resource server)

AAP includes guidance for resource servers in addition to standard JWT/OAuth validation, including:

- **Standard token validation** (issuer, audience, lifetime, signature, etc.) as a baseline. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Proof-of-possession validation** when sender-constrained mechanisms are used (e.g., mTLS-bound tokens or DPoP). https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Task binding validation** (rejecting use outside the intended task/purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Capability enforcement** against structured actions/constraints (instead of relying solely on coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Delegation chain validation** for multi-hop scenarios. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Audit/trace propagation** to support correlation and accountability. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

For JWT handling pitfalls and hardening guidance more generally, JWT Best Current Practices (BCP 8725) is a useful baseline. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

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
