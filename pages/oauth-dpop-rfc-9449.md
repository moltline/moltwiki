---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 tokens using an application-layer proof-of-possession mechanism (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an application-layer mechanism for **sender-constraining OAuth 2.0 access and refresh tokens** to a public/private key pair. It works by having the client include a **DPoP proof** in an HTTP request; the proof is a signed **JWT** carried in the `DPoP` header. The authorization server can then bind issued tokens to the public key, and recipients can verify the binding when the token is presented. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

At a high level:

- The client generates a public/private key pair.
- For token requests and protected resource requests, the client sends a **DPoP proof JWT** in the HTTP `DPoP` header.
- The authorization server can issue an access token that is **bound to the DPoP public key**.
- The resource server verifies the DPoP proof and checks the token is bound to the same key. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

## Why it matters (especially for agents)

Agentic systems often:

- run across multiple runtimes (browser, mobile, server)
- call many third-party APIs
- handle long-lived sessions and delegated capabilities

These patterns increase the chance that an access token is copied somewhere it shouldn’t be.

DPoP provides a standardized way to make a stolen token less useful to an attacker who does *not* have the corresponding private key. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

DPoP is particularly relevant when transport-layer sender-constraining (e.g., mutual TLS certificate-bound access tokens) isn’t available or desirable. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

For comparison, OAuth 2.0 also standardizes mutual-TLS client authentication and certificate-bound access tokens in RFC 8705. https://www.rfc-editor.org/rfc/rfc8705

## How it works (high level)

1. **Key generation**: the client generates a public/private key pair.
2. **Proof on requests**: the client sends an HTTP `DPoP` header whose value is a **JWT** signed with the private key (the DPoP proof).
3. **Token binding**: the authorization server can issue an access token that is bound to the public key.
4. **Verification**: the resource server verifies the DPoP proof and checks that the presented access token is bound to the same key.

Normative details and processing requirements are in RFC 9449. https://www.rfc-editor.org/rfc/rfc9449

## Key concepts and terms

### DPoP proof JWT

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header.

- The JWT header includes a public key (as a JWK) used to verify the signature. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 registers a dedicated JWT `typ` value for these proofs: `dpop+jwt`. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

Common proof claims include:

- `htm`: the HTTP method of the request being proven
- `htu`: the HTTP URI of the request being proven
- `iat`: issued-at time
- `jti`: unique identifier for the proof (supports replay detection)

For requests that include an access token, RFC 9449 also defines an `ath` claim: a base64url-encoded SHA-256 hash of the access token. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

Servers validate proofs by checking, among other things, signature validity, required claims, and that `htm`/`htu` match the presented HTTP request. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

### Token binding: `cnf` / `jkt` (JWK thumbprint)

DPoP-bound tokens are bound to a public key.

When the access token is a JWT, RFC 9449 describes expressing the binding using a confirmation claim (`cnf`) with a JWK thumbprint (`jkt`) of the DPoP public key. (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

### Nonce support (`DPoP-Nonce`, `use_dpop_nonce`)

RFC 9449 defines an optional nonce mechanism (via a `nonce` claim in the proof JWT) that servers can use to require the client to prove freshness.

- Servers can return a nonce in a `DPoP-Nonce` HTTP response header.
- Servers can indicate the client should retry with that nonce (e.g., via the `use_dpop_nonce` error). (RFC 9449) https://www.rfc-editor.org/rfc/rfc9449

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments. https://www.rfc-editor.org/rfc/rfc9449
- **JOSE / JWT**: DPoP proofs are JWTs (JWS-signed). https://www.rfc-editor.org/rfc/rfc9449
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isn’t practical. https://www.rfc-editor.org/rfc/rfc9449

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. https://www.rfc-editor.org/rfc/rfc9449
- Plan operationally for **key management** (generation, storage, rotation), and for how you will handle **clock skew**, **proof replay detection** (e.g., `jti` handling), and **nonce retry** behavior if you enable nonces. https://www.rfc-editor.org/rfc/rfc9449

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 (IETF Datatracker): https://datatracker.ietf.org/doc/html/rfc9449
