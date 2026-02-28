---
title: "RFC 9700 (Best Current Practice for OAuth 2.0 Security)"
description: "An IETF Best Current Practice (BCP 240) that updates OAuth 2.0’s threat model and recommends mitigations such as PKCE, exact redirect URI matching, and sender-constrained tokens."
---

# RFC 9700 (Best Current Practice for OAuth 2.0 Security)

**RFC 9700** is an Internet Engineering Task Force (IETF) **Best Current Practice** document (BCP 240) that collects and updates security guidance for **OAuth 2.0** deployments.

It updates and extends earlier OAuth security analysis and recommendations, incorporating practical lessons from real-world attacks and modern deployment patterns. It also **deprecates** some modes of operation that are considered insecure.

Primary specification:

- https://datatracker.ietf.org/doc/rfc9700/

## Scope

RFC 9700 focuses on security for the OAuth 2.0 ecosystem, including:

- **Authorization servers**, **clients**, and **resource servers**
- Redirect-based authorization flows
- Token replay and token theft
- Common implementation weaknesses observed in practice

It is intended as a consolidated set of best practices rather than a new OAuth “version”. The ongoing **OAuth 2.1** effort is expected to incorporate security recommendations from RFC 9700.

## Selected recommendations (high level)

RFC 9700 contains detailed attacks and mitigations; common themes include:

- **Protect redirect-based flows**
  - Authorization servers should use **exact string matching** for redirect URIs (with a narrow exception for localhost ports for native apps).
  - Avoid **open redirectors** that can be abused to exfiltrate authorization codes or tokens.
  - Clients must implement **CSRF protections** for redirect endpoints; when supported, **PKCE** can provide CSRF protection for authorization code flows.

- **Token replay and theft mitigations**
  - Use mechanisms that reduce the value of stolen tokens, such as **sender-constrained access tokens** (e.g., proof-of-possession style techniques) and **audience restriction**.

- **Client authentication and credential handling**
  - Guidance on robust client authentication and avoiding insecure patterns that lead to credential leakage.

## Relationship to other OAuth specifications

RFC 9700 complements core OAuth specifications and related security extensions:

- OAuth 2.0 Authorization Framework (RFC 6749): https://datatracker.ietf.org/doc/html/rfc6749
- The OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750): https://datatracker.ietf.org/doc/html/rfc6750
- Proof Key for Code Exchange (PKCE, RFC 7636): https://datatracker.ietf.org/doc/html/rfc7636
- Demonstrating Proof of Possession (DPoP, RFC 9449): https://datatracker.ietf.org/doc/html/rfc9449

## References

- RFC 9700: Best Current Practice for OAuth 2.0 Security — https://datatracker.ietf.org/doc/rfc9700/
- RFC Editor entry for RFC 9700 — https://www.rfc-editor.org/info/rfc9700
