# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that profiles the use of **OAuth 2.0** and **JSON Web Tokens (JWTs)** for **autonomous agent (machine) to API** scenarios, with an emphasis on making authorization decisions more **explicit**, **auditable**, and **context-aware** via structured claims and resource-server validation rules. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

OAuth deployments often rely on coarse signals like `scope` and audience (`aud`). AAP’s motivation is that autonomous agents can be high-frequency, delegated across tools, and risk-sensitive to *task context*; the draft argues that traditional scope-based models are not expressive enough to represent these needs safely and transparently. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00

## When you might want AAP

Typical needs called out by the draft include:

- **Task binding**: bind access to a specific task/purpose to reduce “purpose drift”. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Capability-based authorization**: represent permitted actions together with constraints (more structured than coarse scopes). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Delegation clarity**: support auditable delegation across agents/tools (often via token exchange). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Operational/context constraints**: express restrictions such as time windows, network zones, or allowed domains. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Oversight signals**: express that certain actions require human approval/oversight (the draft treats enforcement as deployment-specific). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** define a new authorization protocol; it composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** is commonly used for delegation/impersonation semantics and defines the `act` (actor) claim used to represent an actor chain. https://datatracker.ietf.org/doc/html/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens; common mechanisms include mutual-TLS certificate-bound access tokens (RFC 8705) and DPoP (RFC 9449). https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR, RFC 9396)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://datatracker.ietf.org/doc/html/rfc9396

## What AAP adds (conceptually)

At a high level, AAP standardizes a set of structured JWT claims and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (signals about required approvals/supervision).

## AAP structured claim sections

The draft defines a set of structured claim sections (normative claim names), including:

- `aap_agent` (agent identity and execution context)
- `aap_task` (task identifier, purpose, topic, sensitivity, etc.)
- `aap_capabilities` (authorized actions plus constraints)
- `aap_oversight` (oversight intent, e.g., actions requiring approval)
- `aap_delegation` (delegation metadata; may be used alongside the Token Exchange `act` claim)
- `aap_context` (environment/network/time restrictions)
- `aap_audit` (trace/session identifiers for logging correlation)

(Claim names list: https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00)

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly distinguishes delegation and impersonation semantics and standardizes how to request and obtain tokens representing them. https://datatracker.ietf.org/doc/html/rfc8693

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including “purpose drift” and “confused deputy” style failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00

For JWT handling in general (validation pitfalls, algorithm choices, etc.), JWT Best Current Practices (RFC 8725) is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725.html

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft text (example version). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://datatracker.ietf.org/doc/html/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725.html
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://datatracker.ietf.org/doc/html/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
