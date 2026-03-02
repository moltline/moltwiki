# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that profiles **OAuth 2.0** and **JSON Web Tokens (JWTs)** for **agent-to-API** (machine-to-machine) authorization, especially when autonomous or semi-autonomous agents act on behalf of an operator/principal. It introduces **structured JWT claims** and **resource-server validation expectations** so authorization decisions can be more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## What problem AAP is trying to solve

Classic OAuth deployments often rely on coarse-grained primitives like `scope` and implicit assumptions about *why* a token was issued. AAP is motivated by agentic systems where:

- actions can be high-frequency and autonomous,
- risk depends strongly on **task context** (purpose, sensitivity),
- authority may be **delegated across tools/sub-agents**, and
- systems may need to express **human oversight requirements**.

The draft frames these as gaps in expressiveness and auditability for “scope-only” models. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## When you might want AAP

AAP targets deployments where conventional OAuth token semantics are not expressive enough for agentic systems.

Common needs include:

- **Task binding**: binding tokens to an explicit task/purpose. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Delegation clarity**: distinguishing “act as” (impersonation) vs. “act on behalf of” (delegation). OAuth 2.0 Token Exchange defines these semantics and the `act` (actor) claim used to represent them. https://www.rfc-editor.org/rfc/rfc8693.html
- **Operational / contextual constraints**: limits such as time windows, network/domain restrictions, or rate limits. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Oversight signals**: expressing that some actions require approval or supervision (policy intent; enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749.html
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519.html
- **OAuth 2.0 Token Exchange** is a common fit for delegation and privilege reduction on re-issuance; it standardizes actor/delegation semantics and registers the `act` claim for representing an actor chain. https://www.rfc-editor.org/rfc/rfc8693.html
- **Sender-constrained / proof-of-possession tokens** reduce replay risk compared to bearer tokens. AAP discusses both mutual-TLS certificate-bound access tokens and DPoP as PoP mechanisms. https://www.rfc-editor.org/rfc/rfc8705.html https://www.rfc-editor.org/rfc/rfc9449.html
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396.html

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (policy signals about required approvals/supervision).

## AAP claim sections (high level)

AAP tokens extend standard JWT claims with structured “sections” for agent-specific authorization context. The draft lists these **normative claim names**:

- `aap_agent` — agent identity and execution context. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_task` — task identifier/purpose/topic/sensitivity. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_capabilities` — actions plus constraints. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_oversight` — oversight/approval intent (policy metadata). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_delegation` — delegation metadata; may be used alongside Token Exchange `act`. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html https://www.rfc-editor.org/rfc/rfc8693.html
- `aap_context` — environment/network/time restrictions. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_audit` — trace/session identifiers for logging correlation. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

(For exact field names and processing rules, see the current draft text.) https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth 2.0 Token Exchange defines these semantics and registers the `act` (actor) claim for representing an actor/delegation chain in JWTs (nested `act` objects can represent prior actors). https://www.rfc-editor.org/rfc/rfc8693.html

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Resource server validation (what changes in practice)

AAP is largely about making validation decisions more explicit. In addition to normal JWT checks, a resource server validating an AAP token is expected to evaluate the AAP claim sections relevant to the operation (agent identity, task binding, capabilities/constraints, oversight intent, delegation/context/audit). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), follow **JWT Best Current Practices**. https://datatracker.ietf.org/doc/html/rfc8725

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Purpose drift / permission drift** (using a token beyond its declared task/purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Confused deputy** failures in multi-hop delegation chains. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Replay risk** when bearer tokens are used in high-automation environments; PoP mechanisms like mTLS-bound access tokens or DPoP can help reduce replay. https://www.rfc-editor.org/rfc/rfc8705.html https://www.rfc-editor.org/rfc/rfc9449.html

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF draft text (example version). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749.html
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519.html
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693.html
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705.html
- RFC 8725. “JSON Web Token Best Current Practices.” https://datatracker.ietf.org/doc/html/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396.html
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449.html
