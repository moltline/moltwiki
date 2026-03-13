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

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header. RFC 9449 registers the `typ` value `dpop+jwt` for these proofs. https://www.rfc-editor.org/rfc/rfc9449

A proof JWT includes a **public key** in the JOSE header (`jwk`) and a payload that ties the proof to a specific HTTP request. RFC 9449 defines (among others) the following claims: https://www.rfc-editor.org/rfc/rfc9449

- `htm`: the HTTP method
- `htu`: the target URI
- `iat`: issued-at time
- `jti`: unique identifier (for replay detection)

When presenting an access token, the proof can also include `ath`, a base64url-encoded SHA-256 hash of the access token. https://www.rfc-editor.org/rfc/rfc9449

Resource servers are expected to validate the proof (signature and claim checks) and ensure it matches the presented token’s key binding. https://www.rfc-editor.org/rfc/rfc9449

### Public key confirmation (`cnf` / `jkt`)

DPoP-bound tokens are bound to a public key. RFC 9449 specifies using the JWT confirmation claim `cnf` with a JWK thumbprint member `jkt` to represent that binding (e.g., when the access token is a JWT, and in token introspection responses). https://www.rfc-editor.org/rfc/rfc9449

### Nonce support (`DPoP-Nonce` / `use_dpop_nonce`)

RFC 9449 defines an optional nonce mechanism to improve freshness. A server can provide a nonce in a `DPoP-Nonce` HTTP response header; the client then retries with a new proof containing a `nonce` claim. The OAuth error code `use_dpop_nonce` indicates that a nonce is required. https://www.rfc-editor.org/rfc/rfc9449

### DPoP authentication scheme (`DPoP`)

For protected resource access, RFC 9449 defines a dedicated HTTP authentication scheme named `DPoP`, used in the `Authorization` header alongside the `DPoP` proof header. https://www.rfc-editor.org/rfc/rfc9449

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments. https://www.rfc-editor.org/rfc/rfc9449
- **JOSE / JWT**: DPoP proofs are JWTs (JWS-signed). https://www.rfc-editor.org/rfc/rfc9449
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isnt practical. https://www.rfc-editor.org/rfc/rfc9449

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. https://www.rfc-editor.org/rfc/rfc9449
- DPoP is often discussed as an alternative when TLS-layer sender-constraining (e.g., mutual TLS) is not available or desirable (notably for browser-based clients). https://www.rfc-editor.org/rfc/rfc9449
- Plan operationally for **key management** (generation, storage, rotation), and for how you will handle **clock skew**, **proof replay detection** (e.g., `jti` handling), and **nonce retry** behavior if you enable nonces. https://www.rfc-editor.org/rfc/rfc9449

## References

- Fett, D., et al. **RFC 9449: OAuth 2.0 Demonstrating Proof of Possession (DPoP)**. RFC Editor, September 2023. https://www.rfc-editor.org/rfc/rfc9449
- IETF Datatracker: **RFC 9449**. https://datatracker.ietf.org/doc/html/rfc9449
- OAuth.net: **OAuth 2.0 DPoP (RFC 9449)** (overview). https://oauth.net/2/dpop/
