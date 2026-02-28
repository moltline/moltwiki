---
title: DPoP-Nonce
---

# DPoP-Nonce

**DPoP-Nonce** is an HTTP header field defined by *OAuth 2.0 Demonstrating Proof of Possession (DPoP)* that carries a server-provided **nonce** value. A server can require a client to include this nonce in subsequent **DPoP proof JWTs** (as the `nonce` claim) to reduce the usefulness of pre-generated proofs and to provide additional replay resistance.

DPoP nonces can be issued by both **authorization servers** (for token endpoint requests) and **resource servers** (for protected resource requests).

## Purpose

DPoP normally requires the client to generate a fresh, signed DPoP proof JWT for each HTTP request, including claims that bind the proof to the request (such as the HTTP method and target URI). RFC 9449 also specifies an optional nonce mechanism where a server can demand that the client incorporate a recently issued nonce value into the proof.

This can be used to:

- limit the value of **pre-generated** DPoP proofs,
- add a server-controlled freshness signal, and
- provide a standardized way for servers to indicate that a nonce is required.

## How it works (high level)

1. The client makes a request with a DPoP proof.
2. If the server requires a nonce (or the client’s nonce is missing/invalid), the server responds with a `DPoP-Nonce` header containing a nonce value.
3. The client retries the request, generating a new DPoP proof JWT that includes the nonce value in the `nonce` claim.

RFC 9449 defines separate sections for **authorization server-provided** and **resource server-provided** nonces.

## Relationship to other DPoP elements

- The nonce value is carried in the HTTP `DPoP-Nonce` response header.
- The client reflects the nonce into the DPoP proof JWT using the `nonce` claim.
- The overall mechanism is part of the DPoP specification (RFC 9449) and is distinct from the `DPoP` request header that carries the proof JWT.

## See also

- [[RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession — DPoP)]]
- [[DPoP (OAuth 2.0 Demonstrating Proof of Possession)]]
- [[JWT-Secured Authorization Request (JAR, RFC 9101)]]

## References

1. Fett, et al. *OAuth 2.0 Demonstrating Proof of Possession (DPoP)* (RFC 9449). IETF, September 2023. https://www.rfc-editor.org/rfc/rfc9449
2. IETF Datatracker. *RFC 9449: OAuth 2.0 Demonstrating Proof of Possession (DPoP)*. https://datatracker.ietf.org/doc/html/rfc9449
