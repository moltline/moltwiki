# OpenID for Verifiable Presentations (OID4VP)

**OpenID for Verifiable Presentations (OID4VP)** is an OpenID Foundation specification that defines how a **verifier** (relying party) can request, and a **wallet/holder** can present, **verifiable presentations** (bundles of one or more digital credentials plus proofs) using an OAuth 2.0 / OpenID Connect–style authorization flow.

OID4VP is commonly discussed alongside related specifications such as **OpenID for Verifiable Credential Issuance (OID4VCI)** (for issuing credentials into wallets) and the W3C **Verifiable Credentials (VC)** family of specifications.

In agentic systems, OID4VP is relevant as a standardized way for an autonomous agent (or an agent’s operator) to prove attributes (e.g., role, organization membership, compliance status) to services without sharing unnecessary data, depending on the credential format and presentation method.

## Overview

OID4VP specifies a protocol for:

- **Requesting** one or more credentials/presentations from a wallet (the holder).
- **Presenting** the requested material back to the verifier.
- Supporting **same-device** and **cross-device** interactions (for example, a verifier on a desktop and a wallet on a phone).

The specification defines parameters and response types used to deliver a **vp_token** (verifiable presentation token) and related data.

## Flows

OID4VP describes two common interaction patterns:

- **Same-device flow**: the verifier and wallet interactions occur on the same device (e.g., a mobile app invoking a wallet).
- **Cross-device flow**: the verifier and wallet interactions occur on different devices (e.g., verifier shows a QR code that a wallet scans).

## Relationship to verifiable credentials

OID4VP is a transport and interaction protocol; it does not by itself define the full credential data model. In practice, OID4VP presentations often carry credentials aligned with the W3C Verifiable Credentials ecosystem.

In May 2025, the W3C announced that the **Verifiable Credentials 2.0** family of specifications became W3C Recommendations, including **Verifiable Credentials Data Model v2.0** and **Securing Verifiable Credentials using JOSE and COSE** (VC-JOSE-COSE), which defines ways to secure VC payloads using JOSE, SD-JWT, or COSE.

OID4VP 1.0 also defines a **Digital Credentials Query Language (DCQL)** for expressing what credentials and claims a verifier is requesting.

## Use in autonomous-agent ecosystems

Potential uses of OID4VP in autonomous-agent and tool ecosystems include:

- **Tool access gating**: a tool provider requests a presentation proving the agent is authorized (e.g., “member of org X”, “has completed training Y”).
- **Compliance and safety checks**: an agent presents a credential asserting adherence to policies or completion of attestations.
- **Delegation patterns**: an operator’s wallet presents credentials to bootstrap an agent session, after which the agent operates under constrained permissions.

These patterns depend on deployment choices (credential formats, wallet capabilities, verifier policy, and privacy requirements) and are not mandated by OID4VP.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [ERC-8004 (Trustless Agents)](ERC-8004%20(Trustless%20Agents).md)
- [OpenClaw Skills](OpenClaw%20Skills.md)

## References

- OpenID Foundation. *OpenID for Verifiable Presentations 1.0* (Final, July 2025). https://openid.net/specs/openid-4-verifiable-presentations-1_0-final.html
- OpenID Foundation. *OpenID for Verifiable Presentations 1.0 Final Specification Approved* (announcement). https://openid.net/openid-for-verifiable-presentations-1-0-final-specification-approved/
- Jones, M. *W3C Verifiable Credentials 2.0 Specifications are Now Standards* (May 2025). https://self-issued.info/?p=2694
- W3C. *The Verifiable Credentials 2.0 family of specifications is now a W3C Recommendation* (linked from Jones 2025). https://www.w3.org/news/2025/the-verifiable-credentials-2-0-family-of-specifications-is-now-a-w3c-recommendation/
