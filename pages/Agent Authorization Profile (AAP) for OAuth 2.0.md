# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that profiles the use of **OAuth 2.0** and **JWT** access tokens for **autonomous / agent-to-API** scenarios. It standardizes a set of **structured JWT claims** plus **resource-server validation expectations** so authorization decisions can be more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

Traditional OAuth deployments often rely on coarse indicators like `scope` and `aud`. AAP targets agentic systems where additional semantics matter in security reviews and in runtime enforcement, such as:

- **Task/purpose binding**: make the intended purpose explicit to reduce “purpose drift”. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capability-style authorization**: express permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Delegation clarity**: represent multi-hop delegation (and privilege reduction) when agents call tools or sub-agents. AAP is designed to remain compatible with OAuth 2.0 Token Exchange and its `act` (actor) claim. https://www.rfc-editor.org/rfc/rfc8693 https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Operational/context constraints**: bind tokens to environment constraints (time windows, network zones, etc.). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Human oversight signals**: carry intent like “requires human approval for these actions” (enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** define a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides the signed claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is commonly used for delegation and “act-as / on-behalf-of” patterns; it standardizes the `act` (actor) claim and delegation vs. impersonation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP discusses both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## AAP claim sections (normative names)

AAP extends standard JWT claims (e.g., `iss`, `sub`, `aud`, `exp`, `iat`, `jti`) with a set of structured claim “sections”. The draft lists the **normative claim names** as:

- `aap_agent` — agent identity and execution context
- `aap_task` — task binding (identifier/purpose/topic/sensitivity)
- `aap_capabilities` — permitted actions plus constraints
- `aap_oversight` — oversight intent (e.g., which actions require approval)
- `aap_delegation` — delegation metadata (may be used alongside Token Exchange `act`)
- `aap_context` — operational constraints (network/time/etc.)
- `aap_audit` — identifiers for logging/trace correlation

(Claim name list and discussion: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

## Key concepts (quick definitions)

- **Agent**: an autonomous software entity acting as an OAuth client on behalf of an operator. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capability**: a permitted action together with its restrictions/constraints. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Task**: the unit of work the token is meant to be used for (purpose/topic/sensitivity, etc.). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Proof-of-possession (PoP)**: a mechanism where the client proves it holds a key when presenting the token (e.g., DPoP, mTLS). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly calls out these different semantics and provides a standardized protocol for requesting tokens that represent them, including the `act` (actor) claim used to represent a delegation chain. https://www.rfc-editor.org/rfc/rfc8693

AAP is designed to make the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Implementation notes (resource server side)

AAP is primarily useful when the **resource server (RS)** actually evaluates the structured claims (not just signature + expiry). At minimum, RS validation typically includes:

- Standard JWT checks (`iss`, `aud`, `exp`, signature, etc.). https://www.rfc-editor.org/rfc/rfc7519
- Enforcement of any declared constraints in `aap_task`, `aap_capabilities`, and `aap_context`. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- Delegation-chain interpretation when Token Exchange is used (e.g., `act`). https://www.rfc-editor.org/rfc/rfc8693

For JWT handling guidance (validation, algorithm choices, and common pitfalls), JWT Best Current Practices is a useful baseline. https://www.rfc-editor.org/rfc/rfc8725

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Confused deputy** failures in multi-hop delegation chains. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft HTML (example version). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
