# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF *Internet-Draft* that defines an authorization **profile** for using **OAuth 2.0** with **JWT-based access tokens** in *agent-to-API* (machine-to-machine) scenarios.

The draft’s goal is to make agentic authorization more **explicit and auditable** by standardizing:

- a **structured JWT claim schema** for agent identity, task context, constraints, and oversight signals, and
- **resource-server validation expectations** for those claims.

Primary spec (work in progress): https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions like `scope` and `aud` don’t capture enough semantics for autonomous or semi-autonomous systems.

Common needs include:

- **Task binding**: expressing what task/purpose a token is intended for (to reduce “purpose drift”). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Capability-style authorization**: describing permitted actions with structured constraints (beyond coarse scopes). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation clarity**: distinguishing “act-as” vs “on-behalf-of” semantics across hops (often via OAuth Token Exchange). https://www.rfc-editor.org/rfc/rfc8693
- **Operational constraints**: expressing restrictions like time windows, network/domain limits, or rate limits. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight signals**: indicating that certain actions require approval or supervision (enforcement is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to OAuth 2.0, JWT, Token Exchange, and PoP tokens

AAP does **not** define a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container often used as an access-token format. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** defines a protocol for requesting and obtaining security tokens, including tokens representing **impersonation and delegation** semantics, and registers the `act` (actor) claim commonly used to represent delegation chains. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession (PoP) tokens** reduce replay risk compared to bearer tokens. AAP references common PoP mechanisms such as mutual-TLS certificate-bound access tokens (RFC 8705) and DPoP (RFC 9449). https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR, RFC 9396)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages; this can complement capability-style authorization approaches. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so resource servers can make authorization decisions using:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed/restricted across hops).
- **Oversight requirements** (signals about required approvals/supervision).

Spec: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## AAP claim “sections” (high-level)

The draft defines a set of structured claim namespaces/sections (and schemas). The exact field names and processing rules are in the draft, but the high-level buckets include:

- `aap_agent` (agent identity and execution context)
- `aap_task` (task identifier/purpose/topic/sensitivity)
- `aap_capabilities` (actions + constraints)
- `aap_oversight` (oversight/approval intent)
- `aap_delegation` (delegation metadata; may be used alongside the Token Exchange `act` claim)
- `aap_context` (environment/network/time restrictions)
- `aap_audit` (trace/session identifiers for logging correlation)

Draft section “Structured Sections (Claim Names)”: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly discusses these different semantics and provides a standardized protocol, including the `act` (actor) claim. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Resource server validation (what changes operationally)

AAP’s value is mostly on the **resource server** side: it defines additional checks beyond “standard JWT validation” (signature, issuer, audience, expiry).

Examples of validation categories called out by the draft include:

- **Proof-of-possession validation** (when PoP is used). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Agent identity validation** (how the server interprets agent identity claims). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Task binding validation** (ensuring use is consistent with the declared task/purpose). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Capability enforcement** (checking requested operations against structured capabilities/constraints). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight requirement enforcement** (how “approval required” signals are handled). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation chain validation** (ensuring delegation depth/constraints are respected). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Contextual restriction enforcement** (network/domain/time/rate constraints). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Confused deputy** failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens (RFC 8705) or DPoP (RFC 9449) can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
