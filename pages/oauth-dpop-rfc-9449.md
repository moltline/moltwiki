---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 access and refresh tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an OAuth 2.0 extension that **sender-constrains tokens** at the application layer by binding them to a public key. The client proves possession of the corresponding private key by attaching a signed **DPoP proof JWT** in the HTTP `DPoP` request header. https://www.rfc-editor.org/rfc/rfc9449

The goal is to reduce the impact of **bearer token replay** after token leakage: a stolen token is harder to use if the attacker can’t also produce valid proofs for the bound key. https://www.rfc-editor.org/rfc/rfc9449

## Why it matters (especially for agents)

Agentic systems often:

- run across multiple runtimes (browser, mobile, server)
- call many third-party APIs
- handle long-lived sessions and delegated capabilities

These patterns increase the chance that an access token is copied somewhere it shouldn’t be. DPoP provides a standardized way to make a stolen token less useful to an attacker who does *not* have the corresponding private key. https://www.rfc-editor.org/rfc/rfc9449

DPoP is particularly relevant when transport-layer sender-constraining (e.g., mutual TLS sender-constrained tokens) isn’t practical or available (for example, in browser-based clients). https://www.rfc-editor.org/rfc/rfc9449

## How it works (high level)

1. **Key generation**: the client generates (or otherwise obtains) a public/private key pair.
2. **Proof on requests**: the client sends a `DPoP` HTTP header whose value is a **JWS-signed JWT** (the DPoP proof) demonstrating possession of the private key. https://www.rfc-editor.org/rfc/rfc9449
3. **Token binding**: the authorization server can issue an access token whose confirmation (`cnf`) claim indicates the public key it is bound to (via a JWK thumbprint, `jkt`). https://www.rfc-editor.org/rfc/rfc9449  https://www.rfc-editor.org/rfc/rfc7800
4. **Verification**: the resource server verifies the DPoP proof and checks that the presented access token is bound to the same key. https://www.rfc-editor.org/rfc/rfc9449

## Key concepts and terms

### DPoP proof JWT

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header. A DPoP proof JWT uses the JWT type value `dpop+jwt`. https://www.rfc-editor.org/rfc/rfc9449

The JOSE header of a DPoP proof JWT conveys the public key being proven, typically by embedding it as a JWK in the `jwk` header parameter. https://www.rfc-editor.org/rfc/rfc9449

Common proof claims include:

- `htm`: the HTTP method of the request being proven
- `htu`: the HTTP URI of the request being proven
- `iat`: issued-at time
- `jti`: unique identifier for the proof (supports replay detection)

For requests that include an access token, RFC 9449 defines an `ath` claim: a base64url-encoded SHA-256 hash of the access token. https://www.rfc-editor.org/rfc/rfc9449

A resource server can use `ath` to ensure the proof is bound to the specific access token being presented (not just to the request URL/method). https://www.rfc-editor.org/rfc/rfc9449

### Public key confirmation (`cnf` / `jkt`)

DPoP-bound tokens are bound to a public key. RFC 9449 uses the standard JWT confirmation (`cnf`) claim (defined for proof-of-possession JWT semantics) and represents the DPoP key binding using a JWK thumbprint (`jkt`). https://www.rfc-editor.org/rfc/rfc9449  https://www.rfc-editor.org/rfc/rfc7800

### Authorization server- and resource server-provided nonces

RFC 9449 defines an optional nonce mechanism (via a `nonce` claim in the proof JWT) that servers can use to require freshness. When a nonce is required, the server supplies it in a `DPoP-Nonce` HTTP response header and indicates the client should retry with a fresh proof that includes the `nonce` value (for example, using the `use_dpop_nonce` error code). https://www.rfc-editor.org/rfc/rfc9449

In practice, some providers require a nonce and document “retry with `DPoP-Nonce`” client behavior. https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension for OAuth deployments. https://www.rfc-editor.org/rfc/rfc9449
- **JOSE / JWT**: DPoP proofs are JWS-signed JWTs. https://www.rfc-editor.org/rfc/rfc9449
- **JWT confirmation (`cnf`)**: the `cnf` claim is standardized proof-of-possession semantics for JWTs; DPoP uses it with a JWK thumbprint (`jkt`) to represent the binding key. https://www.rfc-editor.org/rfc/rfc7800  https://www.rfc-editor.org/rfc/rfc9449
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isn’t practical. https://www.rfc-editor.org/rfc/rfc9449

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. https://www.rfc-editor.org/rfc/rfc9449
- DPoP does **not** provide confidentiality for the token; it primarily adds sender-constraining so a leaked token is harder to replay without the private key. https://www.rfc-editor.org/rfc/rfc9449
- Plan operationally for **key management** (generation, storage, rotation), and for how you will handle **clock skew**, **proof replay detection** (e.g., `jti` handling), and **nonce retry** behavior if you enable nonces. https://www.rfc-editor.org/rfc/rfc9449

### When to consider DPoP

DPoP is most useful when bearer tokens might be copied out of the legitimate client context (logs, proxies, crash reports, XSS in a SPA, etc.) and you want the resource server to reject token replay from elsewhere. It is also a common choice when you can’t rely on mutual TLS sender-constrained tokens (RFC 8705) because the client is a browser-based app or otherwise can’t present a stable client certificate. https://www.rfc-editor.org/rfc/rfc9449  https://www.rfc-editor.org/rfc/rfc8705

### Common implementation pitfalls

- **Reusing `jti` across retries**: DPoP proofs are intended to be unique per request; retry logic that replays the same proof can trigger server-side replay detection. https://www.rfc-editor.org/rfc/rfc9449
- **`htu` mismatches**: servers compare the `htu` claim against the request URI; differences in URI normalization (scheme/host casing, default ports, trailing slashes, etc.) can cause verification failures. https://www.rfc-editor.org/rfc/rfc9449
- **Nonce-required deployments**: RFC 9449 defines optional server-provided nonce mechanisms (authorization server- and resource server-provided). Clients should be prepared to retry with a fresh proof JWT that includes the `nonce` claim when a server indicates nonce use. https://www.rfc-editor.org/rfc/rfc9449

## Related standards

- **RFC 8705 (OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens)**: a TLS-layer approach to sender-constraining access and refresh tokens by binding them to a client certificate. https://www.rfc-editor.org/rfc/rfc8705
- **RFC 7800 (Proof-of-Possession Key Semantics for JWTs)**: defines the `cnf` claim used by DPoP to express proof-of-possession key confirmation. https://www.rfc-editor.org/rfc/rfc7800

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 (IETF Datatracker): https://datatracker.ietf.org/doc/html/rfc9449
- RFC 7800 (JWT `cnf` claim / proof-of-possession semantics): https://www.rfc-editor.org/rfc/rfc7800
- RFC 8705 (OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens): https://www.rfc-editor.org/rfc/rfc8705
- OAuth.net DPoP overview: https://oauth.net/2/dpop/
- Auth0 DPoP documentation (implementation notes/examples): https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop
