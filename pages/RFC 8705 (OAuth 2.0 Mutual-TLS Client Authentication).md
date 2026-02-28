---
title: "RFC 8705 (OAuth 2.0 Mutual-TLS Client Authentication)"
---

# RFC 8705 (OAuth 2.0 Mutual-TLS Client Authentication)

**RFC 8705** is an IETF Standards Track specification that defines how OAuth 2.0 clients can authenticate to an authorization server using **mutual TLS (mTLS)** with X.509 certificates, and how authorization servers can issue **certificate-bound (sender-constrained) access tokens** that are usable only by a client presenting the corresponding certificate.

It is commonly discussed alongside other sender-constraining mechanisms such as **DPoP** ([RFC 9449](https://datatracker.ietf.org/doc/html/rfc9449)).

## Overview

In the abstract OAuth 2.0 flow, a client obtains an access token from an authorization server and then presents that token to a protected resource (resource server). RFC 8705 adds two related capabilities:

1. **mTLS client authentication** to OAuth endpoints (e.g., the token endpoint), using either:
   - **PKI-based certificates** (certificate chain anchored in a CA trust model), or
   - **self-signed certificates** (where the authorization server is configured with the client’s certificate information).
2. **Certificate-bound access tokens**, where the access token is cryptographically bound to the client certificate used with mTLS, so a stolen token cannot be replayed by an attacker that lacks the private key.

## Mutual-TLS client authentication

RFC 8705 defines how a client uses an X.509 certificate during the TLS handshake to authenticate to the authorization server (“mutual TLS”). The authorization server validates the certificate according to the registered method (PKI or self-signed) and treats the authenticated certificate as the client credential at the OAuth layer.

This mechanism can be used for endpoints that require OAuth client authentication (not only the token endpoint).

## Certificate-bound (sender-constrained) access tokens

A key feature of RFC 8705 is **binding** an access token to the client certificate so that the protected resource can ensure the token was issued to the client presenting the certificate.

The binding is expressed using the JWT **`cnf` (confirmation)** claim when the access token is a JWT, typically via an X.509 certificate thumbprint confirmation method (see RFC 8705 for the specific confirmation method definition).

For deployments that use OAuth token introspection, RFC 8705 also defines how to communicate the certificate binding information in introspection responses.

## Relationship to OAuth security goals

Certificate-bound access tokens are intended to mitigate token replay in scenarios where bearer tokens might otherwise be stolen (e.g., via logs, proxies, or client-side compromise) and then reused by an attacker.

mTLS-based sender constraining has operational tradeoffs:

- It requires certificate provisioning and lifecycle management.
- It can interact with infrastructure patterns like TLS termination and reverse proxies.

## See also

- [RFC 8705: OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens](https://datatracker.ietf.org/doc/html/rfc8705)
- [RFC 9449: OAuth 2.0 Demonstrating Proof of Possession (DPoP)](https://datatracker.ietf.org/doc/html/rfc9449)
- [OAuth 2.0 (RFC 6749)](https://datatracker.ietf.org/doc/html/rfc6749)
- [OAuth 2.0 Token Introspection (RFC 7662)](https://datatracker.ietf.org/doc/html/rfc7662)

## References

- IETF. *OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705).* February 2020. https://datatracker.ietf.org/doc/html/rfc8705
- RFC Editor. *RFC 8705.* https://www.rfc-editor.org/rfc/rfc8705.html
