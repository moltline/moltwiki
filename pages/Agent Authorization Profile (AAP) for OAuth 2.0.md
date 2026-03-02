# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that profiles how to use **OAuth 2.0** and **JSON Web Tokens (JWTs)** for **agent-to-API** (machine-to-machine) authorization, especially when autonomous or semi-autonomous agents act on behalf of an operator/principal. It defines **structured JWT claims** and **resource-server validation rules** so relying parties can make authorization decisions that are more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

In many deployments, OAuth access tokens are authorized using relatively coarse signals such as `scope` and `aud`. For agentic systems, that can be insufficient to express:

- **Task binding / purpose** (what the token is intended for, to reduce “purpose drift”). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Fine-grained capabilities + constraints** (beyond coarse scopes). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Delegation semantics** across hops (who is acting, and on whose behalf). OAuth 2.0 Token Exchange standardizes delegation vs. impersonation semantics and the `act` (actor) claim used to represent an actor chain. https://www.rfc-editor.org/rfc/rfc8693
- **Operational/contextual restrictions** (e.g., time windows, network/domain restrictions, rate limits). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Oversight requirements** (signals that some actions require approval/supervision; enforcement is deployment-specific). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

AAP’s goal is to make these semantics explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Relationship to existing specs

AAP does **not** introduce a new authorization protocol; it profiles and composes existing standards:

- **OAuth 2.0** (authorization framework and token issuance model). https://www.rfc-editor.org/rfc/rfc6749
- **JWT** (signed, and optionally encrypted, claims container often used as an access token format). https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** (common fit for delegation and “act-as / on-behalf-of” patterns; defines the `act` claim and semantics). https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession (PoP) tokens** (reduce replay risk compared to bearer tokens). Two commonly referenced mechanisms are:
  - **mTLS certificate-bound access tokens**. https://www.rfc-editor.org/rfc/rfc8705
  - **DPoP**. https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** (`authorization_details` for structured authorization data in OAuth messages; can complement capability-style authorization). https://www.rfc-editor.org/rfc/rfc9396

## AAP claim structure (high level)

AAP defines a JWT claim schema organized into a set of **structured sections**. The exact field names and processing rules are defined in the draft (and can evolve between versions), but the core sections include:

- `aap_agent` — agent identity and execution context
- `aap_task` — task identifier/purpose/topic/sensitivity
- `aap_capabilities` — permitted actions plus constraints
- `aap_oversight` — oversight/approval intent signals
- `aap_delegation` — delegation metadata (may be used alongside the Token Exchange `act` claim)
- `aap_context` — environment/network/time restrictions
- `aap_audit` — trace/session identifiers for logging correlation

Structured section list (example version): https://www.ietf.org/archive/id/draft-aap-oauth-profile-01.txt

### Capabilities and constraints

A key design point is shifting from broad scopes to **capabilities** that can be paired with **constraints** (e.g., rate limits, network/domain restrictions, time bounds). The draft defines standard constraint types and how resource servers should validate/enforce them. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

### Delegation vs. impersonation

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them, including the `act` (actor) claim used to represent a delegation chain. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s intended semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Resource server responsibilities (validation)

AAP is opinionated about what a **resource server** should validate beyond baseline JWT checks, including (at a high level):

- Standard token validation (issuer, audience, time bounds, signature/keys).
- Proof-of-possession validation when sender-constrained tokens are used (e.g., mTLS-bound or DPoP-bound tokens). https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- Agent identity validation, task binding validation, capability enforcement, oversight requirement enforcement, delegation chain validation, contextual restriction enforcement, and audit/trace propagation. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

For JWT handling in general (validation pitfalls, algorithm choices, etc.), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## Security notes (why agents are special)

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Confused deputy** failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

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
