# Agent Authorization Profile (AAP) for OAuth 2.0

**Agent Authorization Profile (AAP) for OAuth 2.0** is an IETF Internet-Draft that proposes a profile for using **OAuth 2.0** and **JSON Web Tokens (JWTs)** when **autonomous or semi-autonomous agents** call APIs on behalf of a principal (a user, service, or organization). The draft defines additional JWT claims and validation guidance intended to make agent-to-API authorization more **explicit**, **auditable**, and suitable for **policy enforcement** (for example, by binding tokens to a task context and constraining permitted actions).

Because AAP is published as an **IETF Internet-Draft**, it is a work in progress and may change or be replaced; Internet-Drafts are not standards and are not intended to be cited as stable references. (IETF Datatracker: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/)

## What problem AAP is trying to solve

OAuth 2.0 (RFC 6749: https://datatracker.ietf.org/doc/html/rfc6749) deliberately leaves many authorization semantics to deployments. In many systems, access tokens are treated as opaque or as bearer tokens with minimal structure (e.g., `aud`, `scope`). For agentic systems—where software may plan and execute multi-step tasks—operators often need more explicit answers to questions like:

- *What task is this token meant for?*
- *What actions and resources are permitted?*
- *Who delegated authority to whom, and under what constraints?*
- *What evidence should be logged for audit and incident response?*

AAP’s approach is to **profile** existing standards (OAuth 2.0 + JWT) so that resource servers can apply consistent validation and authorization checks using structured claims.

## Relationship to core OAuth and JWT building blocks

AAP is positioned as a profile layered on top of established components rather than a new authorization protocol:

- **OAuth 2.0** provides the authorization framework and token issuance model (RFC 6749: https://datatracker.ietf.org/doc/html/rfc6749).
- **JWT** provides a compact claims container that can be signed and validated (RFC 7519: https://datatracker.ietf.org/doc/html/rfc7519).
- **OAuth 2.0 Token Exchange** is commonly used in delegation and “act-as / on-behalf-of” patterns (RFC 8693: https://datatracker.ietf.org/doc/html/rfc8693).
- **Proof-of-possession / sender-constrained tokens** can reduce replay risk compared to bearer tokens; DPoP is one standardized mechanism (RFC 9449: https://www.rfc-editor.org/rfc/rfc9449.html).
- **Rich Authorization Requests (RAR)** define `authorization_details` for fine-grained authorization data in OAuth messages (RFC 9396: https://datatracker.ietf.org/doc/html/rfc9396).

AAP uses these as reference points and then specifies additional agent-oriented claims and processing expectations.

## Key concepts (high-level)

The draft’s recurring theme is making agent authorization **constrained and explainable**. At a high level, it aims to standardize how tokens can carry:

- **Agent identity and metadata** (what software entity is acting)
- **Task context** (what the agent is trying to accomplish)
- **Operational constraints** (limits that narrow how, where, and when the token may be used)
- **Delegation chain information** (how authority was derived, passed, or restricted)
- **Oversight requirements** (when human approval or supervision is required)

Exact claim names and validation rules are defined in the draft itself (IETF Datatracker: https://datatracker.ietf.org/doc/draft-aap-oauth-profile/).

## Delegation and constraints

Agentic systems are particularly vulnerable to *permission drift* (agents accumulating broader access over time) and *confused deputy* style failures. AAP focuses on expressing and validating constraints such as:

- Bounding delegation (e.g., limiting how far authority can be re-delegated)
- Restricting token use by time, environment, or other context
- Propagating audit/trace information so downstream services can attribute actions

These constraints are intended to be enforced by resource servers as part of token validation and authorization decisions.

## Security considerations

The draft discusses threats that become more salient with autonomous agents, including impersonation, capability escalation through delegation, and injection-style attacks that could cause an agent to misuse valid credentials. It also emphasizes resource-server validation expectations and safe token handling.

Because this is an Internet-Draft, treat it as evolving guidance; production deployments should also rely on established OAuth security best practices and token sender-constraining mechanisms where appropriate.

## See also

- [OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents](OAuth%202.0%20Extension%20On-Behalf-Of%20User%20Authorization%20for%20AI%20Agents.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)

## References

- IETF Datatracker. “Agent Authorization Profile (AAP) for OAuth 2.0” (Internet-Draft). https://datatracker.ietf.org/doc/draft-aap-oauth-profile/
- RFC 6749. “The OAuth 2.0 Authorization Framework.” https://datatracker.ietf.org/doc/html/rfc6749
- RFC 7519. “JSON Web Token (JWT).” https://datatracker.ietf.org/doc/html/rfc7519
- RFC 8693. “OAuth 2.0 Token Exchange.” https://datatracker.ietf.org/doc/html/rfc8693
- RFC 9396. “OAuth 2.0 Rich Authorization Requests.” https://datatracker.ietf.org/doc/html/rfc9396
- RFC 9449. “OAuth 2.0 Demonstrating Proof of Possession (DPoP).” https://www.rfc-editor.org/rfc/rfc9449.html
