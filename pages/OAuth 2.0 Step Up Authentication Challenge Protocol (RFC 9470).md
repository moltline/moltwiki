# OAuth 2.0 Step Up Authentication Challenge Protocol (RFC 9470)

The **OAuth 2.0 Step Up Authentication Challenge Protocol** is an IETF standards-track extension that allows an OAuth 2.0 **resource server** to tell a **client** that the user authentication associated with the presented access token is insufficient for the requested operation, and to indicate what stronger or more recent authentication is required.

It is standardized as **RFC 9470** (September 2023).

## Motivation

In many deployments, an authorization server can decide what user authentication is required for an access token based on static policy (for example, the client, requested scopes, or resource indicators). However, resource servers may need to enforce requirements that depend on request-specific context (for example, transaction value, risk scoring, or operation type) that the authorization server cannot evaluate ahead of time.

RFC 9470 defines an interoperable way for the resource server to:

- reject a request when the token’s associated authentication is not strong enough or not recent enough, and
- provide machine-readable parameters that the client can use in a new authorization request to obtain a token meeting those requirements.

## Protocol overview

A typical “step up” sequence is:

1. The client calls a protected resource using an existing access token.
2. The resource server determines the token’s associated user authentication does not meet its requirements and responds with a Bearer challenge indicating the needed authentication.
3. The client initiates a new OAuth authorization request that includes the required authentication parameters.
4. The authorization server performs authentication consistent with those requirements and issues a new access token.
5. The client retries the resource request with the new token.

This mechanism is intended to work with standard OAuth 2.0 roles and message flows; it does not define a new grant type.

## Bearer error and challenge parameters

RFC 9470 extends the error codes used with the Bearer authentication scheme (RFC 6750) so that a resource server can indicate that the token is valid in general but is associated with insufficient authentication for the current request.

### `insufficient_user_authentication`

When returning `401 Unauthorized`, the resource server can use the `error` value:

- `insufficient_user_authentication`

to signal that stronger or more recent user authentication is required.

### `acr_values` and `max_age`

The resource server can include the following parameters in the `WWW-Authenticate: Bearer ...` challenge:

- `acr_values`: one or more requested **Authentication Context Class Reference (ACR)** values, as defined by OpenID Connect.
- `max_age`: a requirement on the maximum elapsed time (in seconds) since the user last authenticated, as defined by OpenID Connect.

A client that understands these parameters can use them when constructing a new authorization request to the authorization server.

## Conveying authentication information to the resource server

For the resource server to decide whether a token satisfies its authentication requirements, it needs a way to learn information about the authentication event used when the token was obtained.

RFC 9470 describes approaches including:

- **JWT access tokens** (for example, following the JWT access token profile in RFC 9068), where authentication-related claims can be evaluated by the resource server.
- **Token introspection** (RFC 7662), where the resource server can obtain token metadata (including authentication-related information) from the authorization server.

## Relationship to OpenID Connect

RFC 9470 reuses the OpenID Connect request parameters `acr_values` and `max_age` to express authentication strength and recentness requirements in a way that can be consumed by clients and authorization servers that already support OpenID Connect semantics.

## Security considerations (high level)

The protocol is designed to make step-up authentication interoperable while keeping policy decisions with the resource server. Implementations typically need to consider:

- how authentication information is represented in tokens or introspection responses,
- replay and token substitution risks (mitigated by existing OAuth best practices), and
- ensuring the resource server’s requirements are enforced consistently across endpoints.

## References

- IETF. *RFC 9470: OAuth 2.0 Step Up Authentication Challenge Protocol.* September 2023. https://www.rfc-editor.org/rfc/rfc9470.html
- RFC Editor. *Information page for RFC 9470.* https://www.rfc-editor.org/info/rfc9470
- IETF OAuth Working Group (archived). *oauth-step-up-authn-challenge (draft history).* https://github.com/oauth-wg/oauth-step-up-authn-challenge
- IETF. *RFC 6750: The OAuth 2.0 Authorization Framework: Bearer Token Usage.* October 2012. https://www.rfc-editor.org/rfc/rfc6750
- OpenID Foundation. *OpenID Connect Core 1.0.* (for `acr_values` and `max_age`). https://openid.net/specs/openid-connect-core-1_0.html
- IETF. *RFC 7662: OAuth 2.0 Token Introspection.* October 2015. https://www.rfc-editor.org/rfc/rfc7662
- IETF. *RFC 9068: JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens.* October 2021. https://www.rfc-editor.org/rfc/rfc9068
