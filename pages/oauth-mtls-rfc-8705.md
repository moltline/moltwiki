# OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705)

OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens is an OAuth 2.0 extension standardized as **RFC 8705** (published February 2020).

RFC 8705 defines (1) ways for an OAuth client to authenticate to an authorization server using **mutual TLS (mTLS)** with X.509 certificates, and (2) a way to **bind (“sender-constrain”) access tokens** to the client certificate so that a stolen token cannot be used without also possessing the corresponding private key.\[1\]

**Type:** OAuth 2.0 extension (IETF Standards Track)  
**RFC:** [RFC 8705](https://www.rfc-editor.org/rfc/rfc8705.html)  
**Published:** February 2020  

## Background

In “bearer token” schemes, any party that obtains a valid access token can typically use it until it expires. Sender-constrained tokens aim to reduce the impact of token theft by requiring the presenter to prove possession of a key bound to the token.

RFC 8705 provides sender-constraining for OAuth using the TLS client certificate used in mutual TLS.

## Mutual TLS for OAuth client authentication

RFC 8705 specifies mutual-TLS-based client authentication for requests from a client to an authorization server (for example, at the token endpoint), using X.509 certificates.\[1\]

It defines two approaches:\[1\]

- **PKI mutual-TLS method**: the client certificate chains to a trusted CA (public or private PKI), and the authorization server validates it.
- **Self-signed certificate mutual-TLS method**: the authorization server pins or otherwise associates a specific self-signed certificate with the client.

## Certificate-bound access tokens

RFC 8705 also defines how an authorization server can issue access tokens that are **bound to the client’s certificate**, and how a protected resource can verify that binding.\[1\]

A common representation for the binding is the use of the **`cnf` (confirmation) claim** in a JWT access token, containing a confirmation method that identifies the certificate (for example, by thumbprint).\[1\]

## Implementation considerations

RFC 8705 discusses operational considerations such as TLS termination and certificate lifecycle issues (e.g., expiration) when using certificate-bound tokens.\[1\]

## Relationship to other sender-constraining mechanisms

OAuth has multiple mechanisms for sender-constraining tokens. The OAuth community also documents RFC 8705 as one option alongside other approaches such as DPoP (RFC 9449).\[2\]

## See also

- [OAuth 2.0 Demonstrating Proof of Possession (DPoP) (RFC 9449)](./oauth-dpop-rfc-9449.md)

## References

1. IETF / RFC Editor. “OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens (RFC 8705).” https://www.rfc-editor.org/rfc/rfc8705.html
2. OAuth.net. “RFC 8705: Mutual TLS Client Authentication and Certificate-Bound Access Tokens (MTLS).” https://oauth.net/2/mtls/
