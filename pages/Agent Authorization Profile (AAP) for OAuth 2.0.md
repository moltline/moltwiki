# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft describing an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios. It defines structured JWT claims and validation rules so systems can reason about agent identity, task context, operational constraints, delegation chains, and (where applicable) human oversight requirements. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Seed terms

- Agent-to-API (M2M)
- OAuth 2.0 client credentials
- JWT structured claims
- Delegation vs impersonation
- OAuth 2.0 Token Exchange
- Proof-of-possession (sender-constrained tokens)
- DPoP
- Mutual-TLS certificate-bound access tokens
- Rich Authorization Requests (RAR)
- Resource server validation

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: expressing what task/purpose a token is intended for. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Fine-grained authorization**: representing permitted actions with structured constraints beyond coarse scopes. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation clarity**: distinguishing whether an agent is acting *as* someone (impersonation) vs *on behalf of* someone (delegation). OAuth 2.0 Token Exchange defines these semantics and the `act` (actor) claim used to represent delegation chains. https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: limiting use by time window, domain/network, or rate limiting. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt
- **Auditability / trace signals**: enabling trace propagation and auditing across hops (deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol; it profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** provides a standard protocol for requesting and obtaining security tokens, including delegation and impersonation semantics, and defines the `act` (actor) claim. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** can reduce replay risk compared to bearer tokens:
  - **mTLS certificate-bound access tokens (RFC 8705)** bind tokens to a client certificate presented via mutual TLS. https://www.rfc-editor.org/rfc/rfc8705
  - **DPoP (RFC 9449)** sender-constrains tokens using application-layer proof-of-possession to detect replay. https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR, RFC 9396)** define `authorization_details` for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

The draft notes AAP is typically used in OAuth **client credentials** (agent-to-API / M2M) deployments. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## AAP structured claims (normative claim names)

AAP defines a set of structured JWT claim “sections” with **normative claim names**:

- `agent`
- `task`
- `capabilities`
- `oversight`
- `delegation`
- `context`
- `audit`

(See Section 5 “JWT Claim Schema (AAP Profile)” and Section 5.2 “Structured Sections (Claim Names)” in draft-aap-oauth-profile-01.) https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth 2.0 Token Exchange explicitly discusses these different semantics and standardizes protocol parameters and claims (including the `act` (actor) claim) for representing delegation chains. https://www.rfc-editor.org/rfc/rfc8693

## Resource server validation (high level)

AAP includes guidance for **resource server validation rules** that go beyond standard token validation, including proof-of-possession validation, task binding checks, capability enforcement, contextual restrictions, and audit/trace propagation. https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices provides baseline guidance. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 8693 (OAuth 2.0 Token Exchange)](RFC%208693%20(OAuth%202.0%20Token%20Exchange).md)
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
