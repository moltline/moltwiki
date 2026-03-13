---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an OAuth 2.0 mechanism for **sender-constraining tokens to a public key**. A client sends a signed **DPoP proof JWT** in an HTTP `DPoP` header to prove possession of a private key; an authorization server can then issue access (and refresh) tokens that are **bound to that key**, reducing the value of a leaked bearer token to an attacker who does not possess the private key. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Why it matters (especially for agents)

Agentic systems often run across multiple runtimes (browser, mobile, server) and call many third-party APIs. These patterns increase the chance that an access token is copied into logs, traces, crash reports, or other unintended locations. DPoP mitigates **bearer token replay** by requiring proof-of-possession when the token is used. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

DPoP is also positioned as an application-layer alternative in deployments where transport-layer sender-constraining (e.g., mutual TLS sender-constrained tokens) is not practical. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## How it works (high level)

1. **Key generation**: the client generates a public/private key pair.
2. **Proof on requests**: the client sends an HTTP `DPoP` header whose value is a **JWT** signed with the private key (the DPoP proof).
3. **Token binding**: the authorization server can issue an access token that is bound to the public key.
4. **Verification**: the resource server verifies the DPoP proof and checks that the presented access token is bound to the same key.

Normative details and processing requirements are defined in RFC 9449. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Key concepts and terms

### DPoP proof JWT

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header. RFC 9449 registers a dedicated JWT "typ" value for these proofs: `dpop+jwt`. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

Common proof claims include:

- `htm`: the HTTP method of the request being proven
- `htu`: the HTTP URI of the request being proven
- `iat`: issued-at time
- `jti`: unique identifier for the proof (supports replay detection)

For requests that include an access token, RFC 9449 also defines an `ath` claim: a base64url-encoded SHA-256 hash of the access token. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

### Public key confirmation (`cnf` / `jkt`)

DPoP-bound tokens are bound to a public key. When the access token is a JWT, RFC 9449 describes expressing the binding using a confirmation claim (`cnf`) with a JWK thumbprint (`jkt`) of the DPoP public key. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

### Nonce support (`DPoP-Nonce` / `use_dpop_nonce`)

RFC 9449 defines an optional nonce mechanism (via a `nonce` claim in the proof JWT) that servers can use to require the client to prove freshness. Servers can return a nonce in a `DPoP-Nonce` HTTP response header and indicate the client should retry with that nonce (e.g., via the `use_dpop_nonce` error). [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

The standard defines **both** an authorization-server-provided nonce flow (token endpoint) and a resource-server-provided nonce flow (protected resource access). [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

Some deployments require a nonce for certain clients and document the operational retry flow. For example, Auth0 describes returning a nonce and requiring the client to include a `nonce` claim in subsequent proofs. [Auth0 DPoP documentation](https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop)

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)
- **JOSE / JWT**: DPoP proofs are JWTs (JWS-signed). [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding is not practical. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)
- Implementations typically need operational choices around **key management** (generation, storage, rotation) and handling **clock skew**, **proof replay detection** (e.g., `jti` handling), and optional **nonce retry** behavior. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 (IETF Datatracker): https://datatracker.ietf.org/doc/html/rfc9449
- IANA OAuth Parameters (includes `use_dpop_nonce` error registry entry): https://www.iana.org/assignments/oauth-parameters
- Auth0 documentation: https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop
