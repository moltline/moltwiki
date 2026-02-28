# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios, where autonomous or semi-autonomous agents act on behalf of an operator/principal. It extends common OAuth/JWT deployments with **structured claims** and **resource-server validation expectations** so relying parties can make authorization decisions that are more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Quick definitions

- **Authorization Server (AS)**: issues access tokens (OAuth 2.0). https://www.rfc-editor.org/rfc/rfc6749
- **Resource Server (RS)**: API that validates tokens and enforces authorization (OAuth 2.0). https://www.rfc-editor.org/rfc/rfc6749
- **Agent**: an autonomous software client acting on behalf of an operator (AAP draft terminology). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capability**: a permitted action together with constraints (AAP draft terminology). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Task binding**: binding a token to a specific unit of work/purpose (AAP goal). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Proof-of-possession (PoP)**: sender-constraining mechanisms such as mTLS-bound tokens or DPoP, used to reduce bearer-token replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

## What problem AAP is trying to solve

In many OAuth deployments, authorization is communicated primarily through coarse signals like `scope` and audience (`aud`). AAP targets environments where those are insufficient to express (and enforce) agent-specific semantics such as:

- **Task/purpose binding** (what the token is intended to be used for). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Fine-grained capabilities + constraints** (more structured than scopes). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation chain clarity** across hops (who is acting, and on whose behalf). Token Exchange defines relevant semantics and the `act` (actor) claim. https://www.rfc-editor.org/rfc/rfc8693
- **Operational constraints** (time windows, domain/network restrictions, rate limits). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Oversight requirements** (signals that some actions require approval/supervision; enforcement is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is a common fit for delegation and “act-as / on-behalf-of” patterns; it standardizes the `act` (actor) claim and delegation vs. impersonation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP references both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds

AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting)
- **Task context** (what the token is for)
- **Capabilities and constraints** (what actions are permitted, under what conditions)
- **Delegation chain semantics** (how authority was passed or restricted across hops)
- **Oversight requirements** (policy signals about required approvals/supervision)
- **Audit/trace correlation** (identifiers for logging and incident response)

(See the draft’s “JWT Claim Schema (AAP Profile)” section.) https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## AAP structured claim sections (high-level)

The draft defines a set of structured claim namespaces/sections (and schemas) to carry agent-specific authorization context. The exact fields and processing rules are defined in the draft; conceptually the sections include:

- `aap_agent` — agent identity and execution context
- `aap_task` — task identifier/purpose/topic/sensitivity
- `aap_capabilities` — actions + constraints
- `aap_oversight` — oversight/approval intent
- `aap_delegation` — delegation metadata (may be used alongside Token Exchange `act`)
- `aap_context` — environment/network/time restrictions
- `aap_audit` — trace/session identifiers for logging correlation

(Claim name list and overview: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

### Notes on claim naming

The draft’s examples sometimes show shortened keys (e.g. `agent`, `task`, `capabilities`) inside example JSON, while the **normative top-level claim names** are listed as `aap_agent`, `aap_task`, `aap_capabilities`, etc. Always follow the draft’s normative claim names and schema for interoperability. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them, including the `act` (actor) claim used to represent a delegation chain. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Resource server validation (what changes operationally)

In addition to standard JWT/OAuth validation (issuer, audience, expiry, signature, etc.), the draft describes additional validation expectations for AAP-aware resource servers, including checks for:

- proof-of-possession / sender constraints
- agent identity semantics
- task binding
- capability enforcement
- oversight requirement enforcement
- delegation chain validation
- contextual restrictions enforcement
- audit/trace propagation

The AAP draft describes these additional checks as “Resource Server Validation Rules”; refer to the current draft text for the normative requirements. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **purpose drift / permission drift** (using a token beyond its declared task/purpose). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **confused deputy** failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft text (example version). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
