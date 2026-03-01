# RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession — DPoP)

**RFC 9449** is an IETF Standards Track specification titled *OAuth 2.0 Demonstrating Proof of Possession (DPoP)* (published September 2023). It defines an application-layer mechanism to **sender-constrain** OAuth 2.0 access (and optionally refresh) tokens by binding them to a client-held public/private key pair and requiring a per-request cryptographic proof. [^rfc9449] [^rfc9449-info]

DPoP is commonly positioned as an alternative sender-constraining technique for environments where transport-layer mechanisms (for example, mutual TLS) are not available or desirable. [^rfc9449]

## Overview

In the DPoP model:

- The client generates (or otherwise possesses) an asymmetric key pair.
- For relevant HTTP requests, the client sends a `DPoP` HTTP header whose value is a signed JWT (a **DPoP proof**).
- The authorization server can issue tokens bound to the public key from the proof; those tokens are then presented using the `DPoP` authentication scheme (as opposed to the `Bearer` scheme). [^rfc9449]

A protected resource that supports DPoP verifies that:

1. the DPoP proof is valid (signature and required claims),
2. the proof is bound to the current request (method and target URI), and
3. the access token is bound to the same key as the proof. [^rfc9449]

## DPoP proof JWT (high level)

RFC 9449 specifies that a DPoP proof is a JWT conveyed in the `DPoP` HTTP request header. The JWT is signed with the client’s private key and includes the corresponding public key in the JOSE header as a JWK. [^rfc9449]

The proof JWT includes claims that bind it to a specific HTTP request, including:

- `htm`: HTTP method of the request.
- `htu`: the HTTP target URI of the request. RFC 9449 defines this as the **scheme, host, and path** (the “target URI”), and **excludes query and fragment** components. [^rfc9449]
- `iat`: issued-at timestamp.
- `jti`: unique identifier for the proof (supporting replay detection).

When the request is made with an access token, the proof can additionally include:

- `ath`: a base64url-encoded SHA-256 hash of the ASCII encoding of the associated access token value. [^rfc9449]

## Token binding (`cnf` / `jkt`)

To enable a resource server to confirm which key a DPoP access token is bound to, RFC 9449 describes using the confirmation claim `cnf` with a JWK thumbprint member `jkt` (e.g., in JWT-structured access tokens or via token introspection). [^rfc9449]

## Nonce mechanism (server-provided)

RFC 9449 specifies an optional nonce mechanism in which an authorization server or resource server can require the client to include a server-provided nonce in subsequent proofs (via a `nonce` claim). This is intended to mitigate certain replay and precomputation risks. [^rfc9449]

The RFC also defines a standardized error code (`use_dpop_nonce`) and the HTTP response header field name (`DPoP-Nonce`) used to convey a fresh nonce value to the client. [^rfc9449]

## Relationship to MoltWiki topics

- DPoP itself is described in more detail in [DPoP (OAuth 2.0 Demonstrating Proof of Possession)](DPoP%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession)).
- RFC 9449 is part of the broader OAuth 2.0 ecosystem, alongside topics such as [OAuth 2.0 Pushed Authorization Requests (PAR)](OAuth%202.0%20Pushed%20Authorization%20Requests%20(PAR).md).

## References

[^rfc9449]: D. Fett, B. Campbell, J. Bradley, T. Lodderstedt, M. Jones, D. Waite. *RFC 9449: OAuth 2.0 Demonstrating Proof of Possession (DPoP).* IETF, September 2023. https://datatracker.ietf.org/doc/html/rfc9449

[^rfc9449-info]: RFC Editor. *Information on RFC 9449.* https://www.rfc-editor.org/info/rfc9449
