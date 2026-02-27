# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that profiles how to use **OAuth 2.0** and **JSON Web Tokens (JWTs)** for **agent-to-API** (machine-to-machine) authorization, where autonomous or semi-autonomous agents act for an operator/principal. It introduces **structured JWT claims** and **resource-server validation rules** so authorization decisions can be more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

As of **February 2026**, the IETF Datatracker lists **draft-aap-oauth-profile-01** (Intended status: Standards Track). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## When you might want AAP

AAP targets deployments where conventional OAuth token semantics (e.g., `scope`, `aud`) are too coarse for agentic systems.

Common needs include:

- **Task binding / purpose limitation**: encoding what task/purpose a token is intended for (to reduce “purpose drift”). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Fine-grained authorization**: expressing permitted actions with structured constraints, rather than only coarse scopes. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation clarity**: making it clearer whether an agent is acting *as* someone vs *on behalf of* someone; OAuth Token Exchange defines delegation and the `act` (actor) claim used to represent it. https://www.rfc-editor.org/rfc/rfc8693
- **Operational/context constraints**: time windows, domain/network restrictions, rate limits, and other environment constraints. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight signals**: expressing that some actions require approval/supervision (the enforcement model is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** define a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is a common fit for delegation and “act-as / on-behalf-of” patterns; it standardizes the `act` (actor) claim and delegation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP references both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds

At a high level, AAP standardizes a JWT claim schema and validation expectations so **resource servers** can reason about:

- **Agent identity and execution context**.
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed/restricted across hops).
- **Oversight requirements** (signals about required approvals/supervision).

This is paired with resource-server validation guidance (standard token validation, PoP validation, task binding validation, capability enforcement, delegation chain validation, and audit/trace propagation). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## AAP structured claim sections (high-level)

The draft defines a set of structured claim “sections” (claim names) to carry agent-specific authorization context. The exact field names and processing rules are defined in the draft’s claim schema section. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

The draft also includes a **complete example JWT payload** and specifies additional details such as **string length limits**, an **ABNF grammar for action names**, and a set of **standard constraint types** (including rate limiting, domain/network, time-based, delegation, and data/security constraints). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Commonly referenced sections include:

- `aap_agent` (agent identity and execution context)
- `aap_task` (task identifier/purpose/topic/sensitivity)
- `aap_capabilities` (actions + constraints)
- `aap_oversight` (oversight/approval intent)
- `aap_delegation` (delegation metadata; may be used alongside the Token Exchange `act` claim)
- `aap_context` (environment/network/time restrictions)
- `aap_audit` (trace/session identifiers for logging correlation)

## Delegation vs. impersonation (why it matters)

In agent systems, it’s often important to distinguish:

- **Impersonation**: the caller is treated *as* another identity (downstream systems cannot tell it was delegated).
- **Delegation**: the caller acts *on behalf of* another identity, often with additional constraints and an explicit delegation chain.

OAuth Token Exchange provides a standardized way to request tokens representing these patterns and defines the `act` (actor) claim for expressing delegation. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by aiming to make the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including purpose drift, confused-deputy failures in multi-hop delegation chains, replay risk for bearer tokens, and lack of traceability. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), **JWT Best Current Practices** is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

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
