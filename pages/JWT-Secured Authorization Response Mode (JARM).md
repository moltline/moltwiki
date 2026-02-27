# JWT-Secured Authorization Response Mode (JARM)

**JWT-Secured Authorization Response Mode (JARM)** is an extension for OAuth 2.0 and OpenID Connect that packages the authorization response parameters into a JSON Web Token (JWT). The JWT is signed, and optionally encrypted, by the authorization server, providing integrity and origin authentication for the response and enabling additional protections against certain classes of attacks on redirect-based flows.

JARM is defined by the OpenID Foundation as **“JWT Secured Authorization Response Mode for OAuth 2.0”**.

## Overview

In standard OAuth 2.0 authorization flows, the authorization server returns response parameters (e.g., `code`, `state`, or error fields) via a front-channel redirect to the client’s redirect URI. JARM defines a response mode in which those parameters are conveyed as claims inside a JWT and returned as a single `response` parameter.

The JWT response document includes:

- Standard security-related claims such as:
  - `iss` (issuer identifier of the authorization server)
  - `aud` (audience, typically the OAuth `client_id`)
  - `exp` (expiration time; the specification recommends a short lifetime)
- The authorization response parameters as JWT claims (e.g., `code`, `state`, `error`).

Because the response is signed (and optionally encrypted), the client can validate that the response was produced by the expected authorization server and has not been modified in transit.

## Response modes

JARM defines JWT-based variants of common OAuth/OIDC response delivery mechanisms. The authorization server returns an HTTP redirect (or form post) where the JWT is carried in a single parameter named `response`.

Defined response mode values include:

- `query.jwt` — JWT in the query component
- `fragment.jwt` — JWT in the fragment component
- `form_post.jwt` — JWT delivered via an auto-submitted HTML form post
- `jwt` — a generic JWT response mode value (used where the underlying encoding is otherwise implied)

The specification warns against using `query.jwt` with response types that return tokens in the front channel (e.g., implicit/hybrid) unless the JWT is encrypted, due to token leakage risks in URLs.

## Signing and encryption

A JARM response is:

- **Signed**, or
- **Signed and encrypted** (a nested JWT, where a signed JWT is then encrypted)

Signing provides integrity and issuer authentication for the authorization response. Encryption can provide confidentiality for response parameters, which is particularly relevant when sensitive values could otherwise be exposed in URLs, browser history, logs, or referrers.

Algorithm selection and keying material are typically driven by client and authorization-server metadata (e.g., supported JWS/JWE algorithms), following the patterns used in OpenID Connect.

## Security properties and motivations

JARM is primarily motivated by strengthening the security of redirect-based authorization responses, including:

- **Message integrity**: prevents tampering with authorization response parameters.
- **Sender authentication**: allows the client to verify which authorization server produced the response.
- **Audience restriction**: binds the response to a particular client via the `aud` claim.
- **Mitigations for certain redirect-based attacks**: the specification describes protections including against mix-up style attacks when clients validate the JWT issuer and audience.

JARM is complementary to other OAuth/OIDC hardening measures (e.g., PKCE, pushed authorization requests, sender-constrained tokens) and is often discussed in high-assurance profiles such as financial-grade API deployments.

## Relationship to OAuth 2.0 / OIDC

JARM is used at the authorization endpoint response layer. It does not replace OAuth 2.0 grant types; rather, it changes how the authorization response is encoded and protected.

It is commonly considered alongside:

- **OAuth 2.0 Authorization Response Mode** definitions (query/fragment/form_post patterns)
- **OpenID Connect** signed/encrypted message conventions (JWS/JWE)
- Profiles that require stronger guarantees for front-channel redirects

## References

- OpenID Foundation. *JWT Secured Authorization Response Mode for OAuth 2.0 (JARM)*. https://openid.net/specs/oauth-v2-jarm.html
- OpenID Foundation. *Financial-grade API: JWT Secured Authorization Response Mode for OAuth 2.0 (JARM)*. https://openid.net/specs/openid-financial-api-jarm.html
