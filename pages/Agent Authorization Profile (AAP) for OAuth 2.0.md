# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF *Internet-Draft* that defines an authorization profile for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** in **agent-to-API** (machine-to-machine) scenarios, where autonomous or semi-autonomous agents act on behalf of an operator/principal. It profiles how to represent **agent identity**, **task binding**, **capabilities/constraints**, **delegation**, **context restrictions**, and **oversight signals** in tokens so that resource servers can make more explicit and auditable authorization decisions. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

Because AAP is an Internet-Draft, it is a work in progress and may change; Internet-Drafts are not standards and should be treated as “work in progress”. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

## Motivation and goals

The draft’s motivation is that traditional OAuth deployments (often centered on coarse `scope` strings) can be insufficiently expressive for autonomous agent systems, where risk and permissions depend on *task context*, delegation chains, and operational constraints. The draft lists goals including explicit/verifiable agent identity, task/purpose binding, capability-based authorization with constraints, auditable delegation, and the ability to express human oversight requirements. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Relationship to OAuth 2.0, JWT, Token Exchange, and PoP mechanisms

AAP does **not** introduce a new authorization protocol; it profiles existing standards:

- **OAuth 2.0** provides the framework and token issuance model. https://www.rfc-editor.org/rfc/rfc6749
- **JWT** provides the signed claims container used as a token format in many deployments. https://www.rfc-editor.org/rfc/rfc7519
- **OAuth 2.0 Token Exchange (RFC 8693)** is commonly used for delegation and “act-as / on-behalf-of” patterns; it defines the `act` (actor) claim used to represent an actor/delegation chain. https://www.rfc-editor.org/rfc/rfc8693
- **Sender-constrained / proof-of-possession tokens** (e.g., mTLS-bound access tokens and DPoP) are referenced as mechanisms to reduce bearer-token replay risk. https://www.rfc-editor.org/rfc/rfc8705 https://www.rfc-editor.org/rfc/rfc9449

## AAP claim sections (JWT schema)

AAP profiles a JWT claim schema by adding structured claim “sections” to standard JWT claims (e.g., `iss`, `sub`, `aud`, `exp`). The draft’s normative AAP claim names include:

- `aap_agent`
- `aap_task`
- `aap_capabilities`
- `aap_oversight`
- `aap_delegation`
- `aap_context`
- `aap_audit`

https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

At a high level, these sections are intended to carry:

- **Agent identity/execution context** (e.g., identifiers and relevant runtime metadata). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Task binding** (e.g., a task identifier and purpose/topic/sensitivity metadata). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Capabilities with constraints** (structured authorization beyond coarse scopes). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Oversight requirements** (policy intent signals about actions requiring approval; enforcement is deployment-specific). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Delegation metadata** (optionally in addition to the Token Exchange `act` claim). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html https://www.rfc-editor.org/rfc/rfc8693
- **Contextual restrictions** (e.g., network/time/other operational constraints). https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html
- **Audit/trace correlation identifiers** to support logging and traceability. https://www.ietf.org/archive/id/draft-aap-oauth-profile-00.html

## Validation and enforcement (resource server perspective)

The draft describes that resource servers should validate both standard JWT properties and the additional AAP semantics, including proof-of-possession validation (when used), agent identity validation, task binding validation, capability enforcement, delegation chain validation, contextual restriction enforcement, and audit/trace propagation. https://datatracker.ietf.org/doc/draft-aap-oauth-profile/

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
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449
