# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF *Internet-Draft* that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios, especially where autonomous or semi-autonomous agents act on behalf of an operator/principal. It extends typical OAuth/JWT deployments with (1) **structured claims** and (2) **resource-server validation rules** so relying parties can make authorization decisions that are more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/ https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What AAP is trying to solve

Traditional OAuth deployments often rely on coarse **scopes** and a small set of standard JWT claims. For autonomous agents, that can be too ambiguous: risk depends on **task context**, agents may act at **high frequency**, and authority may be **delegated** across tools/sub-agents.

AAP’s goal is to make the semantics of an access token more explicit so that a **resource server** can enforce:

- **agent identity** (what is acting),
- **task binding** (what the token is for),
- **capabilities + constraints** (what actions are permitted, under what restrictions),
- **delegation chain** semantics (how authority was passed/reduced), and
- **human oversight intent** (what requires approval/supervision).

(Overview, goals, and terminology: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

## Relationship to OAuth 2.0, JWT, Token Exchange, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides the signed claims container commonly used as an access token format. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is commonly used for delegation and “act-as / on-behalf-of” patterns; it defines the `act` (actor) claim used to represent delegation chains. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP discusses both mutual-TLS certificate-bound access tokens and DPoP as PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define `authorization_details` for fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

(Overview and relationship to existing standards: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

## AAP claim namespaces (high-level)

AAP extends standard JWT claims (e.g., `iss`, `sub`, `aud`, `exp`) with structured sections under specific claim names so that resource servers can interpret agent-specific authorization context.

The draft’s normative claim names include:

- `aap_agent`
- `aap_task`
- `aap_capabilities`
- `aap_oversight`
- `aap_delegation` (and/or `act` per RFC 8693)
- `aap_context`
- `aap_audit`

(Claim name list and schema overview: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

### How to read these claims

Treat these as **namespaces** inside the JWT payload. A resource server still performs baseline JWT/OAuth validation (signature, `iss`, `aud`, `exp`, etc.), and then applies AAP-specific validation/enforcement over these structured sections.

(“Standard token validation” + AAP validation rules: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

## When you might want AAP

AAP is aimed at deployments where “plain” OAuth conventions (e.g., `scope`, `aud`) don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: what task/purpose the token is intended for (to reduce purpose drift). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Delegation clarity**: distinguishing impersonation vs. delegation; Token Exchange defines these semantics and the `act` claim. https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: time windows, network/domain restrictions, or rate limits. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Oversight signals**: expressing that some actions require approval or supervision (policy intent; enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth 2.0 Token Exchange explicitly calls out these semantics and provides a standardized protocol for requesting tokens that represent them, including the `act` (actor) claim used to represent a delegation chain. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Resource server validation (what changes operationally)

AAP includes **resource server validation rules** beyond baseline JWT/OAuth checks, such as:

- validating the **agent identity** claims,
- enforcing **task binding** (token use must match declared task context),
- enforcing **capabilities and constraints**,
- enforcing **oversight requirements**, and
- validating **delegation chain** semantics.

(Validation rules: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

### Baseline validation still applies

AAP does not relax baseline requirements. A resource server still needs to do “normal” access token/JWT validation (e.g., verify signature, check `iss`/`aud`, enforce `exp`/`nbf` as applicable) and then *add* AAP-specific enforcement on top. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Confused deputy** failures in multi-hop delegation chains. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)
- [OAuth.net spec index (draft status + dates)](https://oauth.net/specs/)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft text (example version v00, HTML). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
