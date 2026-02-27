---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an OAuth 2.0 mechanism that **sender-constrains tokens to a key**: the client includes a signed **DPoP proof JWT** in an HTTP `DPoP` header, proving possession of a private key corresponding to a public key. If the authorization server issues a **DPoP-bound** access token, that token is intended to be usable only alongside valid DPoP proofs made with the same key. https://www.rfc-editor.org/rfc/rfc9449

This is meant to reduce the impact of **bearer token replay** after token leakage (e.g., logs, browser storage, compromised hosts). https://www.rfc-editor.org/rfc/rfc9449

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

A DPoP proof is a JWT carried in the `DPoP` header.

Commonly referenced claims include:

- `htm`: the HTTP method of the request being proven
- `htu`: the target URI (request URI)
- `iat`: issued-at time
- `jti`: unique identifier for the proof (helps with replay detection)
- `ath`: base64url-encoded SHA-256 hash of the access token (for requests presenting an access token)

See RFC 9449 for the exact requirements and validation rules. https://www.rfc-editor.org/rfc/rfc9449

### Public key confirmation (`cnf`)

When an access token is represented as a JWT, the key binding is typically expressed using a confirmation claim (`cnf`) containing a JWK thumbprint (`jkt`) of the public key used for DPoP proofs. https://www.rfc-editor.org/rfc/rfc9449

### Nonce support (`DPoP-Nonce` / `use_dpop_nonce`)

RFC 9449 defines a nonce mechanism where servers can require the client to include a nonce in the DPoP proof, and can return a fresh nonce via the `DPoP-Nonce` HTTP response header along with an error indicating the client should retry with the nonce (e.g., `use_dpop_nonce`). https://www.rfc-editor.org/rfc/rfc9449

This is commonly used to strengthen anti-replay properties in deployments that want tighter control.

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments. https://www.rfc-editor.org/rfc/rfc9449
- **JOSE / JWT**: DPoP proofs are JWTs (JWS-signed). https://www.rfc-editor.org/rfc/rfc9449
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isnt practical. https://www.rfc-editor.org/rfc/rfc9449

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. https://www.rfc-editor.org/rfc/rfc9449
- For **resource servers**, validating DPoP typically includes: verifying the proof JWT signature using the public key in the proof header (`jwk`), checking `htm`/`htu`/`iat`/`jti`, and verifying the access token hash claim (`ath`) when an access token is presented. https://www.rfc-editor.org/rfc/rfc9449
- Plan operationally for **key management** (generation, storage, rotation), and for how you will handle **clock skew** and **nonce retry** behavior (`DPoP-Nonce` / `use_dpop_nonce`). https://www.rfc-editor.org/rfc/rfc9449

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 (IETF Datatracker): https://datatracker.ietf.org/doc/html/rfc9449
