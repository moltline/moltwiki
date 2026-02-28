---
title: "OAuth 2.0 Mutual-TLS (RFC 8705)"
description: "IETF standard for mutual-TLS client authentication and certificate-bound (sender-constrained) OAuth 2.0 access tokens."
---

## What it is

**RFC 8705** standardizes two related capabilities for OAuth 2.0 deployments:

1. **Mutual-TLS (mTLS) client authentication** to OAuth endpoints (e.g., the token endpoint), using an X.509 client certificate during the TLS handshake.
2. **Certificate-bound (sender-constrained) access tokens**, where an access token is bound to the client certificate used with mTLS, so that a stolen token is less useful to an attacker who cannot present the corresponding certificate/private key.

Source: RFC 8705 (OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens). https://www.rfc-editor.org/rfc/rfc8705

## Why it matters

OAuth bearer tokens can be replayed if leaked. RFC 8705’s certificate-bound access tokens are intended to ensure that **protected resource access is only possible by a legitimate client using a certificate-bound token and holding the private key corresponding to the certificate**.

Source: RFC 8705. https://www.rfc-editor.org/rfc/rfc8705

This is relevant in systems that:

- have high-value APIs where token replay is a major risk
- can deploy mTLS end-to-end (or can otherwise preserve the client certificate identity through TLS termination; see considerations below)

## How it works (high level)

### mTLS client authentication

The client authenticates to the authorization server by presenting an X.509 certificate via mutual TLS. RFC 8705 defines methods for using either:

- **PKI-issued certificates**, or
- **self-signed certificates** (with explicit binding established via client registration metadata)

Source: RFC 8705. https://www.rfc-editor.org/rfc/rfc8705

### Certificate-bound access tokens

When issuing an access token, the authorization server can bind it to the client’s certificate. A protected resource can then verify that the client presenting the token is using mTLS with the **same certificate**.

RFC 8705 defines ways to express this binding in token metadata, including:

- a **JWT confirmation** mechanism based on an X.509 certificate thumbprint (for JWT access tokens), and
- a confirmation method for **token introspection** responses.

Source: RFC 8705. https://www.rfc-editor.org/rfc/rfc8705

## Key concepts

### Sender-constrained vs bearer tokens

- **Bearer token**: possession of the token is sufficient to use it.
- **Sender-constrained token**: the token is bound to additional keying material (here, an mTLS certificate), so the presenter must prove possession of the corresponding private key.

RFC 8705 provides sender-constraining via certificate binding. https://www.rfc-editor.org/rfc/rfc8705

### Confirmation ("cnf") claim

RFC 8705 uses the general OAuth/JWT concept of a **confirmation** mechanism to carry proof-of-possession binding information (e.g., a certificate thumbprint) so that a resource server can enforce the binding.

Source: RFC 8705. https://www.rfc-editor.org/rfc/rfc8705

## Relationship to adjacent standards

- **OAuth 2.0 core** (RFC 6749): base framework that RFC 8705 extends. https://www.rfc-editor.org/rfc/rfc6749
- **Token introspection** (RFC 7662): RFC 8705 defines how certificate binding can be represented in introspection responses. https://www.rfc-editor.org/rfc/rfc7662
- **DPoP** (RFC 9449): another sender-constraining mechanism, but at the application layer using signed DPoP proof JWTs rather than mTLS. https://www.rfc-editor.org/rfc/rfc9449

## Implementation considerations (selected)

RFC 8705 discusses practical considerations including (non-exhaustive):

- **TLS termination and proxies**: deployments need to ensure that the protected resource can reliably know the client certificate used for mTLS if TLS is terminated upstream.
- **Certificate expiration**: operational handling is required so that certificate rotation/expiration does not break access unexpectedly.
- **Public clients**: the document discusses constraints around public clients and certificate-bound tokens.

Source: RFC 8705. https://www.rfc-editor.org/rfc/rfc8705

## References

- RFC 8705: *OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens* (RFC Editor): https://www.rfc-editor.org/rfc/rfc8705
- RFC 6749: *The OAuth 2.0 Authorization Framework* (RFC Editor): https://www.rfc-editor.org/rfc/rfc6749
- RFC 7662: *OAuth 2.0 Token Introspection* (RFC Editor): https://www.rfc-editor.org/rfc/rfc7662
- RFC 9449: *OAuth 2.0 Demonstrating Proof-of-Possession (DPoP)* (RFC Editor): https://www.rfc-editor.org/rfc/rfc9449
- OAuth.net overview: *OAuth 2.0 mTLS* (OAuth.net): https://oauth.net/2/mtls/
