# JWT-Secured Authorization Response Mode (JARM)

**JWT-Secured Authorization Response Mode (JARM)** is an extension for **OAuth 2.0** and **OpenID Connect** that allows an authorization server to return the authorization response parameters (for example, `code` and `state`) as a **JSON Web Token (JWT)**. The JWT can be **signed (JWS)** and optionally **encrypted (JWE)**, providing integrity and origin authentication for the response and (when encrypted) confidentiality for response parameters.

JARM is specified by the OpenID Foundation as *JWT Secured Authorization Response Mode for OAuth 2.0*.

## What problem JARM addresses

In the standard OAuth 2.0 authorization code flow, the authorization server typically returns response parameters via the user agent using query parameters, fragments, or form post. JARM packages those response parameters into a JWT, so the client can validate the response as coming from the expected authorization server and detect tampering.

The JARM specification describes security properties of signed responses, including integrity protection and protection against certain classes of attacks (for example, *mix-up* attacks) by binding the response to the expected issuer and audience.

## How it works (high level)

1. The client requests a JARM response by using a JWT-capable response mode (for example, `query.jwt`, `fragment.jwt`, `form_post.jwt`, or `jwt`).
2. The authorization server constructs a JWT (the *JWT Response*) containing the authorization response parameters as claims.
3. The authorization server signs the JWT (and may also encrypt it).
4. The client validates the JWT (issuer, audience, signature, freshness, and other required claims) and then processes the underlying OAuth response parameters.

## Response modes

JARM defines JWT-based response modes that correspond to common ways of returning authorization responses through the user agent:

- `query.jwt` — JWT is returned in the query component.
- `fragment.jwt` — JWT is returned in the fragment component.
- `form_post.jwt` — JWT is returned using an HTML form post.
- `jwt` — a generic JWT response mode (details depend on the profile/spec usage).

## Signing and encryption

JARM responses are typically **signed** so the client can verify integrity and the authorization server as the sender.

The specification also allows **encryption** of the JWT response, which can reduce exposure of response parameters when they transit the user agent.

## Relationship to other OAuth/OIDC building blocks

JARM is often discussed alongside:

- **JAR (JWT-Secured Authorization Request)**, which packages the *authorization request* into a JWT.
- **PAR (Pushed Authorization Requests)**, which moves request parameters off the front channel.

Together, these mechanisms can reduce reliance on unauthenticated front-channel parameters and improve end-to-end integrity.

## See also

- [JWT-Secured Authorization Request (JAR, RFC 9101).md](JWT-Secured%20Authorization%20Request%20(JAR,%20RFC%209101).md)
- [OAuth 2.0 Pushed Authorization Requests (PAR).md](OAuth%202.0%20Pushed%20Authorization%20Requests%20(PAR).md)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](OAuth%202.0%20Rich%20Authorization%20Requests%20(RFC%209396).md)

## References

- OpenID Foundation. *JWT Secured Authorization Response Mode for OAuth 2.0 (JARM).* https://openid.net/specs/oauth-v2-jarm.html
- OpenID Foundation. *OpenID Connect Core 1.0.* https://openid.net/specs/openid-connect-core-1_0.html
- IETF. *RFC 7519: JSON Web Token (JWT).* https://www.rfc-editor.org/rfc/rfc7519
- IETF. *RFC 7515: JSON Web Signature (JWS).* https://www.rfc-editor.org/rfc/rfc7515
- IETF. *RFC 7516: JSON Web Encryption (JWE).* https://www.rfc-editor.org/rfc/rfc7516
