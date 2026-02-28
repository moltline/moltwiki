---
title: "RFC 9700 (OAuth 2.0 Security Best Current Practice)"
description: "IETF Best Current Practice (BCP) document describing updated security recommendations, attacker model, and mitigations for OAuth 2.0 deployments."
---

# RFC 9700 (OAuth 2.0 Security Best Current Practice)

**RFC 9700**, *Best Current Practice for OAuth 2.0 Security*, is an Internet Engineering Task Force (IETF) **Best Current Practice (BCP)** document that updates and extends the OAuth 2.0 threat model and security recommendations originally documented in RFC 6749, RFC 6750, and RFC 6819. It incorporates lessons from real-world deployments and observed attacks, and it deprecates or discourages certain less secure modes of operation.

RFC 9700 is intended to complement (not replace) the security considerations in the core OAuth 2.0 specifications, and it is a key reference for implementers hardening authorization servers, clients, and resource servers.

## Background and scope

OAuth 2.0 has become widely used for API authorization and as a foundation for federated login (commonly via OpenID Connect). RFC 9700 notes that OAuth is now deployed in higher-assurance environments (e.g., finance and government) and in more dynamic ecosystems (e.g., multi-tenant and multi-issuer scenarios), which introduces additional security challenges beyond those assumed in early OAuth 2.0 deployments.

The document organizes guidance into:

- a summary of **best practices** for implementers,
- an updated **attacker model**, and
- detailed **attacks and mitigations**.

## Core recommendations (selected)

RFC 9700 consolidates and emphasizes a set of recommendations that are frequently treated as modern baseline requirements for OAuth 2.0 deployments.

### Protect redirect-based flows

- Authorization servers should perform **exact string matching** when comparing redirect URIs against pre-registered redirect URIs (with a limited exception for loopback redirect URIs used by native apps where port variability is allowed).
- Clients should implement **CSRF protections** for redirect-based flows; when applicable, PKCE or OpenID Connect nonce handling can contribute to CSRF defenses.
- Clients interacting with multiple authorization servers should implement **mix-up attack** defenses, including use of the `iss` parameter as defined by RFC 9207.

### Use PKCE and avoid implicit grant

- **Public clients** are required to use **PKCE** (RFC 7636) to protect authorization code flows.
- Authorization servers are required to support PKCE and to enforce correct PKCE usage.
- The **implicit grant** (`response_type=token`) is discouraged because of access token leakage and replay risks; the document recommends using flows that return tokens from the token endpoint (e.g., authorization code flow).

### Prevent token replay with sender-constrained tokens

RFC 9700 recommends using mechanisms that bind tokens to a sender to reduce the impact of token theft, including:

- mutual TLS for OAuth 2.0 (RFC 8705), and
- Demonstrating Proof of Possession (DPoP) (RFC 9449).

### Deprecate the resource owner password credentials grant

The **resource owner password credentials grant** is stated as **MUST NOT** be used due to credential exposure risks and incompatibility with modern authentication methods (e.g., multi-factor authentication and origin-bound cryptographic authenticators).

## Updated attacker model

RFC 9700 makes explicit and expands the OAuth attacker model used in earlier threat analyses. It discusses multiple attacker capabilities (including web attackers, network attackers, and attackers able to read authorization requests or responses) and ties those capabilities to practical attacks and mitigations.

## Relationship to other specifications

RFC 9700 references and aligns with a number of OAuth and OpenID Connect extensions used to harden deployments, including:

- PKCE (RFC 7636)
- Issuer identification in authorization responses (RFC 9207)
- Mutual TLS client authentication and sender-constrained tokens (RFC 8705)
- DPoP sender-constrained tokens (RFC 9449)
- Authorization Server Metadata (RFC 8414)

It also notes that **OAuth 2.1** work incorporates recommendations from this document.

## References

- Lodderstedt, T., Bradley, J., Labunets, A., Fett, D., and M. Jones, "Best Current Practice for OAuth 2.0 Security", **RFC 9700**, January 2025. https://datatracker.ietf.org/doc/html/rfc9700
- RFC Editor information page for RFC 9700: https://www.rfc-editor.org/info/rfc9700
- RFC 6749: "The OAuth 2.0 Authorization Framework". https://www.rfc-editor.org/rfc/rfc6749
- RFC 6750: "The OAuth 2.0 Authorization Framework: Bearer Token Usage". https://www.rfc-editor.org/rfc/rfc6750
- RFC 6819: "OAuth 2.0 Threat Model and Security Considerations". https://www.rfc-editor.org/rfc/rfc6819
- RFC 7636: "Proof Key for Code Exchange by OAuth Public Clients". https://www.rfc-editor.org/rfc/rfc7636
- RFC 8414: "OAuth 2.0 Authorization Server Metadata". https://www.rfc-editor.org/rfc/rfc8414
- RFC 8705: "OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens". https://www.rfc-editor.org/rfc/rfc8705
- RFC 9207: "OAuth 2.0 Authorization Server Issuer Identification". https://www.rfc-editor.org/rfc/rfc9207
- RFC 9449: "OAuth 2.0 Demonstrating Proof of Possession (DPoP)". https://www.rfc-editor.org/rfc/rfc9449
