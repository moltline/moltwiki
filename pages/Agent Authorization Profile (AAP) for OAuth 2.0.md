# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that profiles the use of **OAuth 2.0** [[RFC 6749](https://www.rfc-editor.org/rfc/rfc6749)] and **JWT** [[RFC 7519](https://www.rfc-editor.org/rfc/rfc7519)] access tokens for **autonomous / agent-to-API** scenarios. It standardizes a set of **structured JWT claims** plus **resource-server validation expectations** so authorization decisions can be more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

Traditional OAuth deployments often rely on coarse indicators like `scope` and `aud`. AAP targets agentic systems where additional semantics matter in security reviews and in runtime enforcement, such as:

- **Task/purpose binding**: make the intended purpose explicit to reduce “purpose drift”. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Capability-style authorization**: express permitted actions with structured constraints (beyond coarse scopes). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Delegation clarity**: represent multi-hop delegation (and privilege reduction) when agents call tools or sub-agents. AAP is designed to remain compatible with OAuth 2.0 Token Exchange and its `act` (actor) claim. https://www.rfc-editor.org/rfc/rfc8693 https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Operational/context constraints**: bind tokens to environment constraints (time windows, network zones, etc.). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Human oversight signals**: carry intent like “requires human approval for these actions” (enforcement is deployment-specific). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00

## How AAP fits into OAuth (AS/RS) deployments

AAP does **not** define a new authorization protocol. It is a profile that operates within the standard OAuth architecture (Authorization Server issues tokens; Resource Server validates them) and adds a layer of structured claims and validation rules. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00

In many agent-to-API deployments, token issuance still uses standard OAuth grants (e.g., Client Credentials). https://www.rfc-editor.org/rfc/rfc6749

## Relationship to JWT, Token Exchange, and proof-of-possession

AAP profiles and composes existing standards:

- **JWT** provides the signed claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is commonly used for delegation and “act-as / on-behalf-of” patterns; it standardizes the `act` (actor) claim and delegation vs. impersonation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP discusses both mutual-TLS certificate-bound access tokens and DPoP as common PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

## AAP claim sections (normative names)

AAP extends standard JWT claims (e.g., `iss`, `sub`, `aud`, `exp`, `iat`, `jti`) with a set of structured claim “sections”. The draft’s normative claim names are:

- `aap_agent` — agent identity and execution context
- `aap_task` — task binding (identifier/purpose/topic/sensitivity)
- `aap_capabilities` — permitted actions plus constraints
- `aap_oversight` — oversight intent (e.g., which actions require approval)
- `aap_delegation` — delegation metadata (and/or use of Token Exchange `act`)
- `aap_context` — operational constraints (network/time/etc.)
- `aap_audit` — identifiers for logging/trace correlation

(Claim name list: https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00)

## Key concepts (quick definitions)

The draft defines (among others):

- **Agent**: autonomous software entity that acts as an OAuth client and performs actions on behalf of an operator. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Authorization Server (AS)**: issues access tokens and applies AAP policies. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Resource Server (RS)**: protects resources and validates AAP tokens before allowing access. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Capability**: permitted action together with its restrictions (constraints). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Task**: unit of work to which the token is bound (identifier, purpose, sensitivity, etc.). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Proof-of-possession (PoP)**: mechanism where the client demonstrates possession of a key (e.g., DPoP, mTLS) when using the token. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange provides a standardized protocol for requesting tokens that represent these semantics, including the `act` (actor) claim used to represent a delegation chain. https://www.rfc-editor.org/rfc/rfc8693

AAP is designed to make the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00

## Implementation notes (resource server side)

AAP is primarily useful when the **resource server (RS)** actually evaluates the structured claims (not just signature + expiry). At minimum, RS validation typically includes:

- Standard JWT checks (`iss`, `aud`, `exp`, signature, etc.). https://www.rfc-editor.org/rfc/rfc7519
- Enforcement of declared constraints in `aap_task`, `aap_capabilities`, and `aap_context`. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- Delegation-chain interpretation when Token Exchange is used (e.g., `act`). https://www.rfc-editor.org/rfc/rfc8693

For JWT handling guidance (validation, algorithm choices, and common pitfalls), JWT Best Current Practices is a useful baseline. https://www.rfc-editor.org/rfc/rfc8725

## Conformance language

When reading the draft, note that normative keywords like **MUST**, **SHOULD**, and **MAY** are used with the meaning defined by BCP 14. https://www.rfc-editor.org/rfc/rfc2119

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Confused deputy** failures in multi-hop delegation chains. https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft HTML (example version). https://datatracker.ietf.org/doc/html/draft-aap-oauth-profile-00
- RFC 2119. “Key words for use in RFCs to Indicate Requirement Levels.” https://www.rfc-editor.org/rfc/rfc2119
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
