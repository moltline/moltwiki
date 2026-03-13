---
title: DPoP (OAuth 2.0 Demonstrating Proof-of-Possession)
description: Application-layer proof-of-possession mechanism for sender-constraining OAuth 2.0 access and refresh tokens (RFC 9449).
---

# DPoP (OAuth 2.0 Demonstrating Proof-of-Possession)

**Demonstrating Proof of Possession (DPoP)** is an application-layer mechanism for *sender-constraining* OAuth 2.0 access and refresh tokens. It works by having the client attach a signed JSON Web Token (a **DPoP proof**) to HTTP requests; the proof demonstrates possession of a private key corresponding to a public key that the authorization server binds to issued tokens. This provides some protection against replay and misuse of leaked bearer tokens by requiring the presenter to also possess the private key.

DPoP is standardized by the IETF in **RFC 9449**.

## Overview

In a typical OAuth 2.0 deployment using bearer access tokens, any party that obtains a token can use it until it expires. DPoP aims to reduce the impact of token leakage by binding tokens to a public key and requiring the client to prove possession of the corresponding private key when using the token.

DPoP is distinct from client authentication: it can be used alongside various client authentication methods, but the DPoP proof itself is not a client authentication mechanism.

## How it works

At a high level:

1. **Client generates a key pair** (public/private).
2. **Client sends DPoP proofs**: for relevant HTTP requests, the client includes a `DPoP` HTTP header whose value is a signed JWT.
3. **Authorization server binds tokens to the key**: when issuing tokens, the authorization server associates (binds) the token with the client's public key.
4. **Resource server verifies**: when the client presents the token to a resource server, the server verifies the DPoP proof and checks that the token is bound to the public key used to sign that proof.

### DPoP proof JWT

A DPoP proof is a JWT carried in the `DPoP` HTTP header. The proof binds to the specific HTTP request by including values such as the HTTP method and target URI (as defined in RFC 9449). Servers validate the signature and check freshness/replay protections.

## Use cases

DPoP is intended for situations where transport-layer sender-constraining mechanisms are unavailable or undesirable (for example, in user-agent-based applications where TLS client authentication is impractical). RFC 9449 also notes that installed applications can benefit from DPoP-bound tokens because they can often store cryptographic keys in protected storage.

## Relationship to other sender-constraining mechanisms

DPoP is one approach to sender-constraining OAuth tokens. Another standardized mechanism is **mutual TLS (mTLS)** sender-constrained tokens (RFC 8705), which binds tokens to the TLS layer rather than to an application-layer proof.

## Security considerations (high level)

DPoP can help:

- reduce the value of stolen access tokens by requiring an additional proof (possession of the private key), and
- detect certain replay attempts through proof validation rules.

However, DPoP does not eliminate all token theft risks (e.g., if an attacker can execute code in the client context or steal the private key). Implementations must carefully follow RFC 9449 validation requirements (including replay and nonce handling where applicable).

## References

- Fett, D. *et al.* “OAuth 2.0 Demonstrating Proof of Possession (DPoP)”. **RFC 9449** (September 2023). https://www.rfc-editor.org/rfc/rfc9449.html
- IETF Datatracker: RFC 9449. https://datatracker.ietf.org/doc/html/rfc9449
- OAuth.net overview: “OAuth 2.0 DPoP - Demonstrating Proof of Possession”. https://oauth.net/2/dpop/
- Campbell, B. *et al.* “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens”. **RFC 8705** (January 2020). https://www.rfc-editor.org/rfc/rfc8705.html
