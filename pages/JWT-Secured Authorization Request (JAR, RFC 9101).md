# JWT-Secured Authorization Request (JAR, RFC 9101)

**JWT-Secured Authorization Request (JAR)** is an extension to the OAuth 2.0 authorization framework that allows an authorization request’s parameters to be packaged into a **JSON Web Token (JWT)** (called a *Request Object*), which can be **signed (JWS)** and optionally **encrypted (JWE)**. The goal is to provide integrity protection, request source authentication, and (when encrypted) confidentiality for authorization request parameters that would otherwise be transmitted as URL query parameters through a user agent (e.g., a web browser). JAR is standardized as **IETF RFC 9101** (Standards Track, August 2021).

## Overview

In “classic” OAuth 2.0, authorization requests are commonly sent as URL query parameters via the user agent. RFC 9101 describes shortcomings of this approach, including lack of application-layer integrity protection and limited assurances about the request’s origin when parameters traverse the user agent.

JAR introduces two request parameters:

- `request`: carries the Request Object **by value** as a JWT.
- `request_uri`: carries the Request Object **by reference**, as a URI from which the authorization server retrieves the JWT.

The JWT’s claims set contains the OAuth 2.0 authorization request parameters (plus a small set of JWT claims such as `iss` and `aud`).

## Request Object

A **Request Object** in JAR is a JWT whose claims represent the authorization request parameters. It is intended to include all parameters needed to process the request (including extension parameters), except `request` and `request_uri` themselves.

Depending on deployment needs, a Request Object can be:

- **JWS-signed** to provide integrity protection and authenticate the request source.
- **JWE-encrypted** to provide confidentiality end-to-end, even if TLS is terminated at intermediaries.

## Passing the request by reference (`request_uri`)

RFC 9101 also defines how an authorization server fetches a referenced Request Object. It discusses security considerations specific to `request_uri`, including risks such as request URI rewriting and potential denial-of-service concerns if a server fetches attacker-controlled URIs.

## Relationship to OAuth and OpenID Connect

JAR is specified as an OAuth 2.0 extension (RFC 6749 ecosystem) and is also used in practice by **OpenID Connect**, which defines the concept of a Request Object as part of its core specifications.

## Security and privacy considerations

RFC 9101 includes security guidance on:

- Algorithm selection for signing/encryption.
- Request source authentication properties of signed Request Objects.
- Downgrade risks (e.g., falling back to unsigned/plain parameter transmission).
- Operational risks around `request_uri` (fetch behavior, rewriting, amplification).

It also discusses privacy topics such as limiting disclosure of request contents and potential tracking considerations when using referenced Request Objects.

## See also

- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [OAuth 2.0 Pushed Authorization Requests (PAR).md](OAuth%202.0%20Pushed%20Authorization%20Requests%20(PAR).md)
- [DPoP (OAuth 2.0 Demonstrating Proof of Possession)](DPoP%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession))

## References

- IETF. *RFC 9101: The OAuth 2.0 Authorization Framework: JWT-Secured Authorization Request (JAR).* (August 2021). https://datatracker.ietf.org/doc/rfc9101/
- RFC Editor. *RFC 9101 information page (canonical).* https://www.rfc-editor.org/rfc/rfc9101
- OpenID Foundation. *OpenID Connect Core 1.0 (Request Object).* https://openid.net/specs/openid-connect-core-1_0.html
