# OAuth 2.0 JWT-Secured Authorization Request (JAR)

**JWT-Secured Authorization Request (JAR)** is an IETF Standards Track extension to OAuth 2.0, published as **RFC 9101** (August 2021). It defines a way to convey OAuth 2.0 authorization request parameters inside a **JSON Web Token (JWT)** (a *request object*), rather than as plain query parameters, so that the request can be **signed (JWS)** and optionally **encrypted (JWE)**. This provides authorization-request **integrity**, **source authentication**, and (when encrypted) **confidentiality**, including across intermediaries or user agents where TLS may terminate. [^rfc9101]

## Overview

In the base OAuth 2.0 authorization code flow, request parameters such as `response_type`, `client_id`, `redirect_uri`, `scope`, and `state` are typically sent via URI query parameters to the authorization endpoint. RFC 9101 notes that this is easy to implement but exposes the request to risks including parameter tampering and observation in the user agent path. JAR mitigates these weaknesses by packaging request parameters into a JWT that can be signed and/or encrypted. [^rfc9101]

JAR introduces two additional authorization request parameters:

- `request`: carries the JWT *by value*.
- `request_uri`: references a URI from which the authorization server can fetch the JWT *by reference*.

The JWT claims set contains JSON-encoded OAuth authorization request parameters and may also use selected registered JWT claims (notably `iss` and `aud`) as described by RFC 9101. [^rfc9101]

## Request object

RFC 9101 uses the term **request object** for the JWT that encapsulates the authorization request. Depending on deployment requirements, the request object may be:

- **JWS-signed**, enabling integrity protection and authentication of the signer. [^rfc9101]
- **JWE-encrypted**, enabling confidentiality of request parameters end-to-end (even if TLS terminates at intermediaries). [^rfc9101]

Authorization servers validate request objects according to rules in RFC 9101, including signature/encryption processing and assembly/validation of request parameters. [^rfc9101]

## Passing by value vs. by reference

JAR supports two transmission styles:

- **By value (`request`)**: the complete JWT is sent as a parameter to the authorization endpoint.
- **By reference (`request_uri`)**: the client sends a URI; the authorization server retrieves the request object from that location.

RFC 9101 discusses security considerations for `request_uri`, including risks such as denial-of-service against the authorization server and URI rewrite concerns. [^rfc9101]

## Relationship to related OAuth specifications

JAR is part of a broader set of OAuth extensions that strengthen and structure authorization requests:

- **Pushed Authorization Requests (PAR)** (RFC 9126) provides a way to push request parameters directly to the authorization server and send only a reference in the front-channel.
- **Rich Authorization Requests (RAR)** (RFC 9396) defines a structured `authorization_details` parameter for fine-grained authorization.

JAR can be used alongside other extensions depending on system requirements and profiles.

## See also

- [OAuth 2.0 Pushed Authorization Requests (PAR)](OAuth%202.0%20Pushed%20Authorization%20Requests%20(PAR).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396).md](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession — DPoP).md](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)

## References

[^rfc9101]: N. Sakimura, J. Bradley, M. Jones, B. Campbell, and T. Lodderstedt. *RFC 9101: The OAuth 2.0 Authorization Framework: JWT-Secured Authorization Request (JAR).* IETF, August 2021. https://www.rfc-editor.org/rfc/rfc9101.html
