# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios, especially where autonomous or semi-autonomous agents act on behalf of an operator/principal.

AAP does not define a new protocol; it profiles existing OAuth/JWT deployments with **structured JWT claims** and **resource server validation rules** so relying parties can make authorization decisions that are more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## When you might want AAP

AAP is aimed at deployments where common OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding / purpose limitation**: expressing what task or purpose the token is intended for (to reduce “purpose drift”). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation clarity**: whether an agent is acting *as* someone (impersonation) vs *on behalf of* someone (delegation). OAuth 2.0 Token Exchange defines these semantics and the `act` (actor) claim used to represent them. https://www.rfc-editor.org/rfc/rfc8693.html
- **Operational / contextual constraints**: limits such as time windows, domain/network restrictions, or rate limits. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight signals**: expressing that some actions require approval or supervision (policy intent; enforcement is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** is a common fit for delegation and “act-as / on-behalf-of” patterns; it standardizes delegation vs. impersonation semantics and defines the `act` (actor) claim for representing actors and delegation chains. https://www.rfc-editor.org/rfc/rfc8693.html
- **Bearer token usage (RFC 6750)** is the common HTTP usage profile for OAuth access tokens; it highlights that bearer tokens can be used by any party that possesses them and therefore must be protected in transit and at rest. https://www.rfc-editor.org/rfc/rfc6750
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP references both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR) (RFC 9396)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages; this can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (policy signals about required approvals/supervision).
- **Audit / trace correlation** (identifiers intended for logging correlation).

(Overview: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/)

## AAP structured claim sections (high-level)

The draft defines a set of structured claim “sections” (namespaces) to carry agent-specific authorization context. The exact field names and processing rules are in the draft; at a high level, the claim section names include:

- `aap_agent`
- `aap_task`
- `aap_capabilities`
- `aap_oversight`
- `aap_delegation`
- `aap_context`
- `aap_audit`

(Claim section names: https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt)

### How these sections are typically used

- **`aap_agent`**: identifies/describes the agent (or agent instance) that will use the token, so the resource server can apply agent-specific policy. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **`aap_task`**: binds the token to a declared task/purpose so the resource server can reject use outside the intended task context. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **`aap_capabilities`**: expresses allowed actions plus constraints; the draft includes an action-name grammar and standard constraint types (e.g., rate limiting, domain/network constraints, time constraints). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **`aap_oversight`**: carries oversight intent signals (e.g., that certain actions require human approval), leaving enforcement details to the deployment. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **`aap_delegation`**: carries delegation metadata and constraints; it can be used alongside the Token Exchange `act` claim and delegation chain semantics. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ https://www.rfc-editor.org/rfc/rfc8693.html
- **`aap_context`**: expresses environmental restrictions such as network/domain/time windows. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **`aap_audit`**: provides trace/session identifiers intended for audit logging correlation. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, while retaining its own identity.

OAuth 2.0 Token Exchange explicitly discusses these different semantics and describes how composite tokens can represent both the primary subject and the actor, including via the `act` claim (and nested `act` claims) to represent a chain of delegation. https://www.rfc-editor.org/rfc/rfc8693.html

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Resource server validation (what changes in practice)

In addition to standard OAuth/JWT checks, AAP describes additional validation expectations for resource servers, such as:

- validating proof-of-possession / sender constraints when used (e.g., mTLS-bound tokens or DPoP), https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- enforcing task binding and capability constraints, https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- validating delegation chains and applying delegation constraints. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ https://www.rfc-editor.org/rfc/rfc8693.html

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Confused deputy** failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Replay risk** when bearer tokens are used in high-automation environments; sender-constrained / proof-of-possession mechanisms can reduce replay compared to bearer tokens. https://www.rfc-editor.org/rfc/rfc6750 https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft text (example version). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 6750. “The OAuth 2.0 Authorization Framework: Bearer Token Usage.” https://www.rfc-editor.org/rfc/rfc6750
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693.html
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
