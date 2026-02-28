---
title: "OAuth DPoP (RFC 9449)"
description: "IETF standard for sender-constraining OAuth 2.0 tokens using application-layer proof-of-possession (DPoP), reducing replay risk for leaked bearer tokens."
---

## What it is

**DPoP (Demonstrating Proof-of-Possession)** is an application-layer mechanism for **sender-constraining OAuth 2.0 access and refresh tokens**. A client proves possession of a public/private key pair by including a `DPoP` HTTP header in requests; the header value is a signed JWT (a **DPoP proof**) that allows an authorization server to bind issued tokens to the client’s public key. Resource servers can then verify that the party presenting the token also possesses the corresponding private key. https://www.rfc-editor.org/rfc/rfc9449

DPoP’s objective is to reduce the impact of **bearer token replay** after token leakage by requiring proof-of-possession when the token is used, and by enabling detection of replay attacks involving access and refresh tokens. https://www.rfc-editor.org/rfc/rfc9449

## Why it matters (especially for agents)

Agentic systems often:

- run across multiple runtimes (browser, mobile, server)
- call many third-party APIs
- handle long-lived sessions and delegated capabilities

These patterns increase the chance that an access token is copied into logs, crash reports, browser storage, or intermediate services. DPoP provides a standardized way to make a stolen token less useful to an attacker who does *not* have the corresponding private key. https://www.rfc-editor.org/rfc/rfc9449

DPoP is commonly discussed as an alternative when transport-layer sender-constraining (e.g., mutual TLS sender-constrained tokens) is not available or desirable (notably for browser-based clients). https://www.rfc-editor.org/rfc/rfc9449

## How it works (high level)

1. **Key generation**: the client generates a public/private key pair.
2. **Proof on requests**: the client sends an HTTP `DPoP` header whose value is a JWT signed with the private key (the DPoP proof).
3. **Token binding**: the authorization server can issue an access token bound to the public key.
4. **Verification**: the resource server verifies the DPoP proof and checks that the presented access token is bound to the same key.

Normative details and processing requirements are specified in RFC 9449. https://www.rfc-editor.org/rfc/rfc9449

## Key concepts and terms

### DPoP proof JWT

A **DPoP proof** is a JWT carried in the `DPoP` HTTP header. RFC 9449 registers a media type for these proofs: `application/dpop+jwt` (and the corresponding JWT “typ” value `dpop+jwt`). https://www.rfc-editor.org/rfc/rfc9449

DPoP proofs are bound to a specific HTTP request using claims including:

- `htm`: the HTTP method of the request being proven
- `htu`: the HTTP URI of the request being proven
- `iat`: issued-at time
- `jti`: unique identifier for the proof (supports replay detection)

For requests that include an access token, RFC 9449 also defines an `ath` claim: a base64url-encoded SHA-256 hash of the access token. https://www.rfc-editor.org/rfc/rfc9449

### Public key confirmation (`cnf` / `jkt`)

DPoP-bound tokens are bound to a public key. RFC 9449 defines a confirmation method based on a JWK thumbprint (`jkt`). When an access token is a JWT, the binding can be expressed using a confirmation claim (`cnf`) containing the `jkt` value. https://www.rfc-editor.org/rfc/rfc9449

RFC 9449 also describes how the same confirmation method can be represented in OAuth token introspection responses. https://www.rfc-editor.org/rfc/rfc9449

### Nonce support (`DPoP-Nonce` and `use_dpop_nonce`)

RFC 9449 defines optional nonce mechanisms that can be used by authorization servers and resource servers to require proof freshness.

- Servers can supply a nonce in a `DPoP-Nonce` HTTP response header.
- The client retries using a `nonce` claim in the DPoP proof.
- The error code `use_dpop_nonce` is defined for indicating that a nonce is required. https://www.rfc-editor.org/rfc/rfc9449

## Relationship to adjacent standards

- **OAuth 2.0**: DPoP is an extension mechanism for OAuth deployments. https://www.rfc-editor.org/rfc/rfc9449
- **JOSE / JWT**: DPoP proofs are JWTs (JWS-signed). https://www.rfc-editor.org/rfc/rfc9449
- **mTLS sender-constrained tokens**: DPoP is an application-layer alternative when TLS-layer binding isn’t practical. https://www.rfc-editor.org/rfc/rfc9449

## Practical notes

- DPoP is not itself a client authentication method; it is used to **constrain tokens**. https://www.rfc-editor.org/rfc/rfc9449
- Replay protection depends on server-side checks (e.g., validating the DPoP proof, enforcing an acceptable `iat` window, and preventing reuse of `jti` values within that window). https://www.rfc-editor.org/rfc/rfc9449
- Operationally, implementations typically need plans for **key management** (generation, storage, rotation), and for handling **clock skew** and **nonce retry** behavior if nonces are enabled. https://www.rfc-editor.org/rfc/rfc9449

## Notes

### RFC errata

RFC 9449 has a verified editorial erratum (EID 7646) correcting “authentication server” to “authorization server” in Section 4.2 with respect to `DPoP-Nonce` handling. https://www.rfc-editor.org/errata/eid7646

## Sources

- RFC 9449 (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- RFC 9449 (IETF Datatracker): https://datatracker.ietf.org/doc/html/rfc9449
- OAuth.net overview: https://oauth.net/2/dpop/
- RFC 9449 errata (RFC Editor): https://www.rfc-editor.org/errata/rfc9449
