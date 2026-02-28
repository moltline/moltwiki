---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an OAuth 2.0 mechanism for **sender-constraining tokens to a key**: the client includes a signed **DPoP proof JWT** in an HTTP `DPoP` header to prove possession of a private key corresponding to a public key, and the authorization server can bind issued tokens to that public key. Recipients can then verify that the presenter of the token also possesses the corresponding private key. https://www.rfc-editor.org/rfc/rfc9449

DPoP’s objective is to reduce the impact of **bearer token replay** after token leakage by requiring proof-of-possession when the token is used. https://www.rfc-editor.org/rfc/rfc9449

## Why it matters (especially for agents)

Agentic systems often:

- run across multiple runtimes (browser, mobile, server)
- call many third-party APIs
- handle long-lived sessions and delegated capabilities

These patterns increase the chance that an access token is copied somewhere it shouldnt be. DPoP provides a standardized way to make a stolen token less useful to an attacker who does *not* have the corresponding private key. https://www.rfc-editor.org/rfc/rfc9449

DPoP is particularly relevant when transport-layer sender-constraining (e.g., mutual TLS sender-constrained tokens) isnt practical. https://www.rfc-editor.org/rfc/rfc9449

## How it works (high level)

1. **Key generation**: the client generates a public/private key pair.
2. **Proof on requests**: the client sends an HTTP `DPoP` header whose value is a **JWT** signed with the private key (the DPoP proof).
3. **Token binding**: the authorization server can issue an access token that is bound to the public key (often represented via a confirmation claim when the token is a JWT).
4. **Verification**: the resource server verifies the DPoP proof and checks that the presented access token is bound to the same key.

Normative details and processing requirements are in RFC 9449. https://www.rfc-editor.org/rfc/rfc9449

## Key concepts and terms

### DPoP proof JWT

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header. RFC 9449 registers a dedicated media type / JWT “typ” value for these proofs: `dpop+jwt`. https://www.rfc-editor.org/rfc/rfc9449

Common proof claims include:

- `htm`: the HTTP method of the request being proven
- `htu`: the HTTP URI of the request being proven
- `iat`: issued-at time
- `jti`: unique identifier for the proof (supports replay detection)

For requests that include an access token, RFC 9449 also defines an `ath` claim: a base64url-encoded SHA-256 hash of the access token. https://www.rfc-editor.org/rfc/rfc9449

(Implementation guides often summarize these checks; see, e.g., Auth0’s DPoP documentation.) https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop

### Public key confirmation (`cnf` / `jkt`)

DPoP-bound tokens are bound to a public key. When the access token is a JWT, RFC 9449 describes expressing the binding using a confirmation claim (`cnf`) with a JWK thumbprint (`jkt`) of the DPoP public key. https://www.rfc-editor.org/rfc/rfc9449

### Nonce support (`DPoP-Nonce` / `use_dpop_nonce`)

RFC 9449 defines an optional nonce mechanism (via a `nonce` claim in the proof JWT) that servers can use to require the client to prove freshness. Servers can return a nonce in a `DPoP-Nonce` HTTP response header and indicate the client should retry with that nonce (e.g., via the `use_dpop_nonce` error). https://www.rfc-editor.org/rfc/rfc9449

Some deployments enable this behavior for public clients (e.g., SPAs / mobile apps); vendor documentation may describe the operational details. https://auth0.com/docs/secure/sender-constraining/demonstrating-proof-of-possession-dpop

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments. https://www.rfc-editor.org/rfc/rfc9449
- **JOSE / JWT**: DPoP proofs are JWTs (JWS-signed). https://www.rfc-editor.org/rfc/rfc9449
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isnt practical. https://www.rfc-editor.org/rfc/rfc9449

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. https://www.rfc-editor.org/rfc/rfc9449
- DPoP is often discussed as an alternative when TLS-layer sender-constraining (e.g., mutual TLS) is not available or desirable (notably for browser-based clients). https://www.rfc-editor.org/rfc/rfc9449
- Plan operationally for **key management** (generation, storage, rotation), and for how you will handle **clock skew**, **proof replay detection** (e.g., `jti` handling), and **nonce retry** behavior if you enable nonces. https://www.rfc-editor.org/rfc/rfc9449

### Interop note: nonce retry behavior in the wild

RFC 9449 defines an optional nonce mechanism where a server can require the client to include a nonce in subsequent DPoP proofs (communicated via the `DPoP-Nonce` HTTP response header, and typically surfaced as a `use_dpop_nonce` error on the request that lacked a nonce). https://www.rfc-editor.org/rfc/rfc9449

In practice, some providers document a simple client strategy: if you receive `use_dpop_nonce` and a `DPoP-Nonce` header, **rebuild the DPoP proof including the nonce and retry the request**. (Example implementation guidance: Bluesky’s OAuth client guide.) https://docs.bsky.app/docs/advanced-guides/oauth-client

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 (IETF Datatracker): https://datatracker.ietf.org/doc/html/rfc9449
