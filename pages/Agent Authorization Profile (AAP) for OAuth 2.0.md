# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that defines an authorization *profile* for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios, where autonomous or semi-autonomous agents act on behalf of an operator/principal. It extends typical OAuth/JWT deployments with **structured claims** and **resource-server validation rules** so relying parties can make authorization decisions that are more explicit, auditable, and context-aware. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an **Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and should be treated as “work in progress”. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## What problem AAP is trying to solve

OAuth deployments commonly rely on relatively coarse signals such as `scope` and audience (`aud`). In highly automated agent systems, those signals can be too ambiguous for safe, auditable authorization decisions (e.g., “what task is this token for?”, “what constraints apply?”, “is human approval required?”, “how did delegation happen?”). AAP’s goal is to make these semantics explicit and consistently verifiable by resource servers. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## When you might want AAP

AAP targets deployments where “plain” OAuth conventions don’t capture enough semantics for agentic systems.

Typical needs include:

- **Task binding**: binding an access token to a specific task/purpose to reduce “purpose drift”. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capability-style authorization**: expressing permitted actions with structured constraints (beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Delegation clarity**: representing delegation vs. impersonation in multi-hop systems (often via OAuth Token Exchange). https://www.rfc-editor.org/rfc/rfc8693
- **Operational / contextual constraints**: limits such as time windows, network/domain restrictions, and rate limits. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Oversight signals**: expressing that some actions require approval/supervision (policy intent; enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Relationship to OAuth 2.0, JWT, and proof-of-possession

AAP does **not** introduce a new authorization protocol. It profiles and composes existing standards:

- **OAuth 2.0** provides the authorization framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides a signed (and optionally encrypted) claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange** is a common fit for delegation and “act-as / on-behalf-of” patterns, including delegation vs. impersonation semantics. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession (PoP) tokens** reduce replay risk compared to bearer tokens; AAP is designed to remain compatible with mechanisms such as mutual-TLS certificate-bound access tokens and DPoP. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449
- **Rich Authorization Requests (RAR)** define the `authorization_details` parameter for carrying fine-grained authorization data in OAuth messages, which can complement capability-style authorization. https://www.rfc-editor.org/rfc/rfc9396

## What AAP adds (conceptually)

At a high level, AAP standardizes a JWT claim schema and validation expectations so resource servers can reason about:

- **Agent identity / metadata** (who/what is acting).
- **Task context** (what the token is for).
- **Capabilities and constraints** (what actions are permitted, under what conditions).
- **Delegation chain semantics** (how authority was passed or restricted across hops).
- **Oversight requirements** (policy signals about required approvals/supervision).
- **Audit correlation** (trace/session identifiers that can be carried with the token).

## AAP claim sections (high-level)

AAP tokens extend standard JWT claims (e.g., `iss`, `sub`, `aud`, `exp`, `iat`, `jti`) with structured sections. The draft’s normative claim names are:

- `aap_agent`
- `aap_task`
- `aap_capabilities`
- `aap_oversight`
- `aap_delegation`
- `aap_context`
- `aap_audit`

(Claim names list: https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html)

### Minimal intuition for each section

- `aap_agent`: identifies the agent and (optionally) execution context (the draft notes this may include a workload identifier such as a SPIFFE ID in SPIFFE/SPIRE-based environments). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html https://spiffe.io/docs/latest/spiffe-about/overview/
- `aap_task`: binds the token to a task (identifier/purpose/topic/sensitivity), so downstream services can enforce “this token is only for *that* work”. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_capabilities`: expresses permitted actions together with constraints (a capability-style model rather than only coarse `scope`). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_oversight`: expresses human oversight requirements as policy metadata (intent), leaving enforcement to the resource server/orchestrator. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_delegation`: carries delegation metadata; the draft also points to using the standard `act` (actor) claim from OAuth Token Exchange for delegation chains. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html https://www.rfc-editor.org/rfc/rfc8693
- `aap_context`: carries operational constraints such as network/time/geo restrictions (deployment-specific semantics). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- `aap_audit`: carries trace/session identifiers intended to correlate authorization decisions with logs/traces (the draft mentions compatibility with existing trace context approaches such as W3C Trace Context and OpenTelemetry). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html https://www.w3.org/TR/trace-context/ https://opentelemetry.io/docs/what-is-opentelemetry/

## Delegation vs. impersonation (why it matters for agents)

Many agent systems need to distinguish:

- **Impersonation**: the caller is treated *as* another identity.
- **Delegation**: the caller is acting *on behalf of* another identity, often with additional constraints.

OAuth Token Exchange explicitly discusses delegation vs. impersonation semantics and defines a protocol for requesting and obtaining security tokens with those semantics. https://www.rfc-editor.org/rfc/rfc8693

AAP builds on these patterns by making the resulting token’s semantics more explicit and consistently verifiable by resource servers. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Security notes

AAP is motivated by threats that are especially salient in autonomous systems, including:

- **Agent impersonation** (tokens representing a different agent than intended). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capability escalation** (obtaining broader permissions than intended). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Purpose drift** (using a token beyond its declared task/purpose). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Replay risk** when bearer tokens are used in high-automation environments; proof-of-possession mechanisms can reduce replay. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

For JWT handling in general (validation, algorithm choices, and deployment pitfalls), JWT Best Current Practices is a useful baseline reference. https://www.rfc-editor.org/rfc/rfc8725

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)](OAuth%202.0%20Mutual-TLS%20Client%20Authentication%20and%20Certificate-Bound%20Access%20Tokens%20(RFC%208705).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- IETF Internet-Draft HTML. “Agent Authorization Profile (AAP) for OAuth 2.0” (draft-aap-oauth-profile-00). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://www.rfc-editor.org/rfc/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://www.rfc-editor.org/rfc/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://www.rfc-editor.org/rfc/rfc8693
- RFC 8705. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens.” https://www.rfc-editor.org/rfc/rfc8705
- RFC 8725. “JSON Web Token Best Current Practices.” https://www.rfc-editor.org/rfc/rfc8725
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://www.rfc-editor.org/rfc/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
- W3C Recommendation. “Trace Context.” https://www.w3.org/TR/trace-context/
- OpenTelemetry. “What is OpenTelemetry?” https://opentelemetry.io/docs/what-is-opentelemetry/
- SPIFFE. “Overview.” https://spiffe.io/docs/latest/spiffe-about/overview/
