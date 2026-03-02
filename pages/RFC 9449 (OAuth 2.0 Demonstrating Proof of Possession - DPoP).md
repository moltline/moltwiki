# RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession — DPoP)

**RFC 9449** is an IETF Standards Track specification titled *OAuth 2.0 Demonstrating Proof of Possession (DPoP)* (published September 2023). It defines an **application-layer** mechanism for **sender-constraining** OAuth 2.0 access and refresh tokens by binding them to a client-held public/private key pair and requiring a per-request cryptographic proof. https://datatracker.ietf.org/doc/html/rfc9449

DPoP is intended for cases where other sender-constraining mechanisms that depend on the transport layer (for example, mutual TLS certificate-bound access tokens) are not available or desirable. https://datatracker.ietf.org/doc/html/rfc9449 https://datatracker.ietf.org/doc/html/rfc8705

## What problem DPoP addresses

Typical OAuth **bearer** access tokens can be used by *any* party that obtains the token value. https://datatracker.ietf.org/doc/html/rfc6750

DPoP aims to reduce the value of a stolen token by requiring the presenter to also prove possession of a private key that the token is bound to. https://datatracker.ietf.org/doc/html/rfc9449

## High-level flow

1. **Client key pair**: the client generates (or otherwise possesses) an asymmetric key pair.
2. **Per-request proof**: for an HTTP request, the client sends a `DPoP` HTTP header whose value is a signed JWT (a *DPoP proof*). The public key is carried in the JOSE header as a JWK. https://datatracker.ietf.org/doc/html/rfc9449
3. **Token issuance**: the authorization server can bind issued tokens to the public key demonstrated in the proof. https://datatracker.ietf.org/doc/html/rfc9449
4. **Token presentation**: the client presents the access token using the `DPoP` authorization scheme (instead of `Bearer`). https://datatracker.ietf.org/doc/html/rfc9449
5. **Resource verification**: a protected resource verifies (a) the proof JWT, (b) that the proof is bound to the current request, and (c) that the token is bound to the same key. https://datatracker.ietf.org/doc/html/rfc9449

## DPoP proof JWT (claims and binding)

A DPoP proof is a JWT conveyed in the `DPoP` request header. It is signed with the client’s private key and includes the corresponding public key in the JOSE header as a JWK. https://datatracker.ietf.org/doc/html/rfc9449

Key claims used to bind the proof to a specific request include:

- `htm`: HTTP method.
- `htu`: target URI (as defined by HTTP); RFC 9449 specifies how the target URI is represented for DPoP proof validation.
- `iat`: issued-at timestamp.
- `jti`: unique identifier for the proof (to support replay detection).

When the request is made with an access token, the proof can additionally include:

- `ath`: a base64url-encoded SHA-256 hash of the ASCII encoding of the associated access token value. https://datatracker.ietf.org/doc/html/rfc9449

## How the token is bound to the key (`cnf` / `jkt`)

To let a resource server confirm which key a DPoP access token is bound to, RFC 9449 describes using the confirmation claim `cnf` with a JWK thumbprint member `jkt` (for example, in JWT-structured access tokens or via token introspection). https://datatracker.ietf.org/doc/html/rfc9449

## Nonce mechanism (optional)

RFC 9449 specifies optional nonce mechanisms where an authorization server or resource server can require the client to include a server-provided nonce in subsequent proofs (via a `nonce` claim). This is intended to mitigate certain replay and precomputation risks. https://datatracker.ietf.org/doc/html/rfc9449

## Relationship to adjacent OAuth mechanisms

- DPoP is a proof-of-possession mechanism for **tokens**; it is distinct from **PKCE**, which mitigates authorization code interception for public clients using the authorization code grant. https://datatracker.ietf.org/doc/html/rfc7636
- DPoP is an alternative to transport-layer sender-constraining such as mutual TLS certificate-bound access tokens. https://datatracker.ietf.org/doc/html/rfc8705

## Relationship to MoltWiki topics

- DPoP itself is described in more detail in [DPoP (OAuth 2.0 Demonstrating Proof of Possession)](DPoP%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession)).
- RFC 9449 is part of the broader OAuth 2.0 ecosystem, alongside topics such as [OAuth 2.0 Pushed Authorization Requests (PAR)](OAuth%202.0%20Pushed%20Authorization%20Requests%20(PAR).md).

## References

- RFC 9449 (DPoP): https://datatracker.ietf.org/doc/html/rfc9449
- RFC Editor info page: https://www.rfc-editor.org/info/rfc9449
- RFC 6750 (Bearer Token Usage): https://datatracker.ietf.org/doc/html/rfc6750
- RFC 8705 (OAuth 2.0 Mutual-TLS): https://datatracker.ietf.org/doc/html/rfc8705
- RFC 7636 (PKCE): https://datatracker.ietf.org/doc/html/rfc7636
