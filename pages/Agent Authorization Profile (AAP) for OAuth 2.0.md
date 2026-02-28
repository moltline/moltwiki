# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** scenarios (machine-to-machine), especially where autonomous or semi-autonomous agents act on behalf of an operator/principal. AAP extends existing OAuth/JWT deployments with **structured claims** and **resource-server validation rules** so relying parties can make authorization decisions that are more explicit, auditable, and context-aware.

- IETF Datatracker (current draft): https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- Example published draft text (versioned): https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What it is

AAP is a **JWT-based access token profile**: it assumes you already have an OAuth 2.0 Authorization Server (AS) issuing access tokens and Resource Servers (RS) validating them, then standardizes additional, structured JWT claims (and RS validation expectations) so an RS can evaluate:

- who/what the agent is,
- what task/purpose the token is intended for,
- what actions are allowed (and under what constraints), and
- what delegation/oversight context must be enforced.

Draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: what task/purpose the token is intended for (to reduce “purpose drift”). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Delegation clarity**: distinguishing *impersonation* (“act as”) vs *delegation* (“on behalf of”). Token Exchange defines these semantics and the `act` (actor) claim used to represent delegation chains. https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: limits such as time windows, domain/network restrictions, or rate limits. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Oversight signals**: expressing that some actions require approval or supervision (policy intent; enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **Bearer token usage** (how access tokens are used at HTTP APIs) is specified separately; if you deploy bearer tokens, any party in possession of the token can use it. https://datatracker.ietf.org/doc/html/rfc6750
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is a common fit for delegation and “act-as / on-behalf-of” patterns, including the `act` (actor) claim. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP references both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (policy signals about required approvals/supervision).
- **Audit/trace context** (so downstream systems can log and correlate agent actions).

Draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## AAP structured claims (draft-defined)

The draft defines a set of structured claim “sections” (top-level claim names) used to carry agent-specific authorization context.

The claim names and schemas are draft-defined and may change between versions; consult the current draft for the authoritative list and processing rules. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

(Example published draft text) https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth 2.0 Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them. It also defines the `act` (actor) claim used to represent delegation chains. https://www.rfc-editor.org/rfc/rfc8693

## Resource server validation (what changes operationally)

AAP’s core operational value is in **resource server (RS) validation and enforcement**. In addition to standard OAuth/JWT validation, the draft describes RS checks such as:

- validating proof-of-possession / sender-constraining when used,
- validating agent identity and task binding,
- enforcing capabilities and constraints,
- enforcing oversight requirements,
- validating delegation chain semantics, and
- propagating audit/trace context.

Draft: https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

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

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft (versioned text, example). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 6750. “The OAuth 2.0 Authorization Framework: Bearer Token Usage.” https://datatracker.ietf.org/doc/html/rfc6750
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
