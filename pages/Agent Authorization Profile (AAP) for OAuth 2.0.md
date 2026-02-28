# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios.

Primary spec (Internet-Draft): https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. See “Status of This Memo” on the Datatracker page: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

In many agentic deployments, a token needs to carry more than “who is calling” and a coarse `scope` string. Resource servers often need to enforce **purpose binding**, **structured capabilities**, **delegation semantics**, **operational constraints**, and **audit/trace context** in a way that is consistent across implementations.

AAP’s core move is to standardize:

- a **structured JWT claim schema** for agent/task/capability context, and
- **resource server validation rules** for interpreting and enforcing those claims.

(Draft overview and table of contents show the claim schema and validation rules sections: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/)

## Where AAP fits in the OAuth/JWT ecosystem

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** defines a protocol for exchanging tokens, including delegation and impersonation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens; common mechanisms include mutual-TLS certificate-bound access tokens and DPoP. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define `authorization_details` for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

Related JWT guidance worth reading alongside AAP:

- **JWT BCP** (validation pitfalls, algorithm choices, claim handling). https://www.rfc-editor.org/rfc/rfc8725

## What AAP adds (high level)

AAP extends standard JWT claims with **structured AAP claim sections** and pairs them with **validation expectations** so resource servers can reason about:

- **Agent identity / execution context** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (signals that some actions require approval/supervision).
- **Audit / trace propagation** (correlation identifiers for logging).

This framing (structured claims + resource server validation rules) is the core of AAP’s abstract and overview. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

### AAP is a profile, not an “agent identity” standard

AAP does **not** make claims “true”. AAP claims are **authorization inputs** issued by (or via) an authorization server, and must be validated and then mapped to local policy at the resource server.

This matches the general OAuth model: access tokens are security artifacts used for authorization decisions, not ground-truth identity documents. https://www.rfc-editor.org/rfc/rfc6749

## AAP structured claim sections (as defined in the draft)

The draft defines the following AAP claim section names (see “Structured Sections (Claim Names)” in the draft):

- `aap_agent`
- `aap_task`
- `aap_capabilities`
- `aap_oversight`
- `aap_delegation`
- `aap_context`
- `aap_audit`

Source: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

High-level intent of each section (conceptual):

- `aap_agent`: agent identity and execution context
- `aap_task`: task identifier/purpose/topic/sensitivity
- `aap_capabilities`: actions plus constraints
- `aap_oversight`: oversight / approval intent
- `aap_delegation`: delegation metadata
- `aap_context`: environment/network/time restrictions
- `aap_audit`: trace/session identifiers for logging correlation

If you need the exact field-level schema and examples, use the draft’s “JWT Claim Schema” and “Example Claim Structures” sections. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Capabilities and constraints (why structured claims matter)

AAP’s motivation is that flat scopes are often too coarse for agentic systems. The draft includes an explicit section on **standard constraint types and semantics** (including rate limiting, domain/network constraints, time-based constraints, delegation constraints, and data/security constraints). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Delegation vs. impersonation (and Token Exchange)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth 2.0 Token Exchange defines these semantics and is commonly used in multi-hop agent/tool chains. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Implementation notes (resource servers)

AAP is a profile, so most of the work is in **validation and enforcement** at the resource server:

- Perform standard JWT validation (signature, `iss`, `aud`, time-based claims, etc.). JWT BCP provides deployment guidance and common pitfalls. https://www.rfc-editor.org/rfc/rfc8725
- Enforce proof-of-possession / sender-constraining when used (e.g., mTLS-bound tokens or DPoP) to reduce replay risk. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- Treat AAP structured claims as **authorization inputs**: validate schema and apply local policy; reject unknown/invalid structures rather than “best effort” parsing.

The draft’s “Resource Server Validation Rules” section enumerates these categories of checks. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Implementation notes (authorization servers)

If you issue AAP-profiled tokens, the draft also sets expectations for the authorization server side (authentication, token binding / sender constraints, capability + constraint encoding, token lifetime, token exchange usage, revocation, and audit/trace propagation). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Threat model notes (what AAP is trying to mitigate)

The draft includes a threat model summary covering topics such as agent impersonation, capability escalation, purpose drift, malicious/excessive delegation, large-scale automated misuse, prompt/data injection, lack of traceability, and use outside intended environment. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)
- [RFC 8693 (OAuth 2.0 Token Exchange)](RFC%208693%20(OAuth%202.0%20Token%20Exchange).md)

## References

- IETF Internet-Draft. “Agent Authorization Profile (AAP) for OAuth 2.0”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
