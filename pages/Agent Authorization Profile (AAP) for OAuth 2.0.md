# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** with **JWT-encoded access tokens** in **agent-to-API** (machine-to-machine) scenarios. It aims to make tokens more **context-rich** (agent identity, task/purpose, constraints, delegation, oversight) and to define **resource-server validation expectations** so authorization decisions are more explicit and auditable. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

In many deployments, OAuth access tokens that only carry coarse signals like `scope` and `aud` don’t capture enough semantics for autonomous systems. AAP’s goal is to make **intent and limits machine-checkable** so resource servers can evaluate:

- **Who/what is acting** (agent identity and execution context). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **What the token is for** (task binding / purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **What actions are allowed** and with what constraints (capability-style authorization). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **How authority was delegated** (delegation chain semantics). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Whether human oversight is required** (oversight requirements as policy signals). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: what task/purpose the token is intended for (to reduce “purpose drift”). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Delegation clarity**: distinguishing “act-as” (impersonation) vs “on-behalf-of” (delegation). OAuth Token Exchange defines these semantics and the `act` (actor) claim used to represent them. https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: limits such as time windows, network/domain restrictions, or rate limits. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Oversight signals**: expressing that some actions require approval or supervision (enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** is a common fit for delegation and “act-as / on-behalf-of” patterns; it standardizes the `act` (actor) claim and delegation vs. impersonation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP discusses both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds

At a high level, AAP standardizes:

1) A **structured JWT claim schema** (organized into “sections”) for agent authorization context. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

2) **Resource server validation rules** for interpreting and enforcing those sections (in addition to normal JWT/OAuth validation). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## AAP structured claim sections (high-level)

The draft groups AAP-specific claims into structured sections so the token can carry agent-relevant authorization context in a predictable shape. The exact fields and processing rules are defined in the draft. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

Commonly referenced sections include:

- `aap_agent` — agent identity and execution context. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- `aap_task` — task identifier/purpose/topic/sensitivity. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- `aap_capabilities` — permitted actions plus constraints. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- `aap_oversight` — oversight requirements / policy signals. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- `aap_delegation` — delegation metadata (often used alongside Token Exchange `act`). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- `aap_context` — environmental restrictions (e.g., network/domain/time). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- `aap_audit` — trace/session identifiers for logging correlation. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation (act-as)**: the caller is treated *as* another identity.
- **Delegation (on-behalf-of)**: the caller is acting *for* another identity, often with additional constraints.

OAuth Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them, including the `act` (actor) claim used to represent a delegation chain. https://www.rfc-editor.org/rfc/rfc8693

## Resource server validation (what to check)

AAP’s intent is that resource servers do normal JWT/OAuth validation *and then* validate the AAP-specific semantics.

Useful baselines to cross-reference:

- **JWT validation best practices** (algorithm selection, `typ`/`kid` handling, etc.). https://www.rfc-editor.org/rfc/rfc8725
- **DPoP validation** (proof-of-possession binding and replay protections). https://www.rfc-editor.org/rfc/rfc9449
- **mTLS-bound access token validation**. https://www.rfc-editor.org/rfc/rfc8705

(Full AAP validation rules are in the draft’s “Resource Server Validation Rules” section.) https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Confused deputy** failures in multi-hop delegation chains. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

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
