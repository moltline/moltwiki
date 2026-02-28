---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 access and refresh tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an OAuth 2.0 mechanism for **sender-constraining access and refresh tokens** at the application layer. A client proves possession of a private key by including a signed **DPoP proof JWT** in an HTTP `DPoP` header; the authorization server can then bind issued tokens to the corresponding public key, and recipients can verify that the presenter of a token also possesses the private key. https://www.rfc-editor.org/rfc/rfc9449

DPoP’s objective is to reduce the impact of **bearer token replay** after token leakage by requiring proof-of-possession when the token is used. https://www.rfc-editor.org/rfc/rfc9449

## Why it matters (especially for agents)

Agentic systems often:

- run across multiple runtimes (browser, mobile, server)
- call many third-party APIs
- handle long-lived sessions and delegated capabilities

These patterns increase the chance that an access token is copied somewhere it shouldn’t be. DPoP provides a standardized way to make a stolen token less useful to an attacker who does *not* have the corresponding private key. https://www.rfc-editor.org/rfc/rfc9449

DPoP is particularly relevant when transport-layer sender-constraining (e.g., mutual TLS sender-constrained tokens) isn’t practical or available (for example, in browser-based clients). https://www.rfc-editor.org/rfc/rfc9449

## How it works (high level)

1. **Key generation**: the client generates a public/private key pair.
2. **Proof on requests**: the client sends an HTTP `DPoP` header whose value is a **JWT** signed with the private key (the DPoP proof).
3. **Token binding**: the authorization server can issue tokens that are bound to the public key.
4. **Verification**: the resource server verifies the DPoP proof and checks that the presented access token is bound to the same key.

Normative details and processing requirements are in RFC 9449. https://www.rfc-editor.org/rfc/rfc9449

## Key concepts and terms

### DPoP proof JWT

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header. A DPoP proof JWT uses the JWT type value `dpop+jwt`. https://www.rfc-editor.org/rfc/rfc9449

The JOSE header of a DPoP proof JWT includes the client’s public key as a JWK (`jwk`), which identifies the key pair the client is proving possession of. https://www.rfc-editor.org/rfc/rfc9449

Common proof claims include:

- `htm`: the HTTP method of the request being proven
- `htu`: the HTTP URI of the request being proven
- `iat`: issued-at time
- `jti`: unique identifier for the proof (supports replay detection)

For requests that include an access token, RFC 9449 also defines an `ath` claim: a base64url-encoded SHA-256 hash of the access token. https://www.rfc-editor.org/rfc/rfc9449

### Public key confirmation (`cnf` / `jkt`)

DPoP-bound tokens are bound to a public key. RFC 9449 specifies a confirmation method using a JWK thumbprint (`jkt`) in the confirmation (`cnf`) claim to represent the DPoP public key binding. https://www.rfc-editor.org/rfc/rfc9449

### Authorization server- and resource server-provided nonces

RFC 9449 defines an optional nonce mechanism (via a `nonce` claim in the proof JWT) that servers can use to require the client to prove freshness. Servers can return a nonce in a `DPoP-Nonce` HTTP response header and indicate the client should retry with that nonce (e.g., via the `use_dpop_nonce` error). https://www.rfc-editor.org/rfc/rfc9449

In practice, some deployments require a nonce for public clients (e.g., SPAs or mobile apps) and instruct clients to retry after receiving a `DPoP-Nonce` header. https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop

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
- OAuth.net DPoP overview: https://oauth.net/2/dpop/
- Auth0 DPoP documentation (implementation notes/examples): https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop
