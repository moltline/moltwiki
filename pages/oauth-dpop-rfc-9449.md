---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## Overview

**Demonstrating Proof of Possession (DPoP)** is an application-layer mechanism for **sender-constraining OAuth 2.0 access and refresh tokens** to a public/private key pair. A client proves possession of the private key by including a signed **DPoP proof JWT** in an HTTP `DPoP` header; the authorization server can then bind tokens it issues to the corresponding public key, enabling recipients to verify that the party presenting the token also possesses the associated private key. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

DPoP is intended to reduce the impact of **bearer token replay after token leakage** by making a stolen token insufficient on its own. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

DPoP can be used when transport-layer sender-constraining mechanisms (such as mutual TLS sender-constrained tokens) are not available or desirable, including in browser-based clients. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## How it works (high level)

1. **Key generation**: the client generates a public/private key pair.
2. **Proof on requests**: for token requests and protected resource requests, the client sends a `DPoP` HTTP header whose value is a JWT signed with the private key (the DPoP proof).
3. **Token binding**: the authorization server can issue an access token that is bound to the client’s public key.
4. **Verification**: the resource server verifies the DPoP proof and checks that the presented access token is bound to the same key.

Normative processing requirements and security considerations are specified in RFC 9449. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Key concepts

### DPoP proof JWT

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header. RFC 9449 registers the media type / `typ` value `dpop+jwt` for these proofs. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

The proof JWT commonly includes claims that bind the proof to a particular HTTP request, including:

- `htm`: the HTTP method
- `htu`: the HTTP URI
- `iat`: issued-at time
- `jti`: unique identifier (supports replay detection)

For requests that use an access token, RFC 9449 also defines an `ath` claim: a base64url-encoded SHA-256 hash of the access token. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

### Public key confirmation (`cnf` / `jkt`)

DPoP-bound tokens are bound to a public key. When the access token is a JWT, RFC 9449 describes expressing the binding using a confirmation claim (`cnf`) with a JWK thumbprint (`jkt`) of the DPoP public key. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

### Authorization server-provided nonce (`DPoP-Nonce` / `use_dpop_nonce`)

RFC 9449 defines an optional nonce mechanism (via a `nonce` claim in the proof JWT) that an authorization server can use to require proof freshness. The server can return a nonce in a `DPoP-Nonce` HTTP response header and indicate that the client should retry with that nonce (for example, using the `use_dpop_nonce` error). [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)
- **JOSE / JWT**: DPoP proofs are signed JWTs (JWS). [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isn’t practical. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Practical considerations

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)
- Deployments typically need operational policies for **key management** (generation, storage, rotation) and for handling **clock skew** and **proof replay detection** (for example, `jti` reuse). [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)
- If nonce support is enabled, clients must implement **retry** behavior when a server responds with a nonce requirement. [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449)

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 (IETF Datatracker): https://datatracker.ietf.org/doc/html/rfc9449
