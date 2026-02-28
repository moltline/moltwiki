# OAuth 2.0 Step Up Authentication Challenge Protocol (RFC 9470)

## Summary

**RFC 9470** defines an OAuth 2.0 extension that enables **step-up authentication** in a standardized, interoperable way.

It allows a **resource server** to reject an API request when the user authentication associated with the presented access token is not strong enough or not recent enough, and to tell the client *what is required* to proceed. The client can then send the user back to the **authorization server** with an authorization request that asks for the required authentication strength or freshness, obtain a new access token, and retry the API call. [RFC 9470](https://datatracker.ietf.org/doc/html/rfc9470)

## Problem it addresses

In many deployments, the authorization server decides what authentication to perform based on static factors (client, scopes, resource indicators, configuration). In practice, an API may need to require stronger or more recent authentication based on request-time risk signals or business logic (for example, transaction amount or fraud scoring) that the authorization server does not know in advance. RFC 9470 standardizes a way for the resource server to communicate those requirements back to the client. [RFC 9470](https://datatracker.ietf.org/doc/html/rfc9470)

## How it works (high level)

1. A client calls a protected resource with a Bearer access token.
2. The resource server determines that the authentication event associated with that token is insufficient.
3. The resource server responds with an OAuth error and a **WWW-Authenticate** challenge that indicates required authentication properties.
4. The client initiates a new authorization flow at the authorization server, including the requested authentication properties.
5. The authorization server issues a new access token whose associated authentication meets the requirements.
6. The client retries the API request with the new token.

This end-to-end flow is described in the protocol overview. [RFC 9470](https://datatracker.ietf.org/doc/html/rfc9470)

## Key protocol elements

### Error code: `insufficient_user_authentication`

RFC 9470 extends the Bearer token error codes defined for OAuth 2.0 protected resources by defining the error value:

- `insufficient_user_authentication`

A resource server uses this error when the token is valid but the *user authentication* tied to the token does not satisfy the resource server’s requirements. [RFC 9470](https://datatracker.ietf.org/doc/html/rfc9470)

### Challenge parameters: `acr_values` and `max_age`

To express what is required, the resource server can include these parameters in the Bearer challenge:

- `acr_values`: requested authentication context class reference values
- `max_age`: maximum acceptable time since the user last authenticated

The client then uses these values in a subsequent authorization request to the authorization server, using the parameters as defined by OpenID Connect. [RFC 9470](https://datatracker.ietf.org/doc/html/rfc9470)

## Token validation and conveying authentication information

For the resource server to decide whether the authentication is sufficient, it must be able to determine properties of the authentication event associated with the access token.

RFC 9470 discusses approaches where:

- the access token is a **JWT access token** (e.g., per JWT profile work), or
- the resource server uses **OAuth 2.0 token introspection**.

The exact mechanics depend on the token format and deployment, but the resource server needs a reliable way to evaluate authentication strength and/or freshness for the token presented. [RFC 9470](https://datatracker.ietf.org/doc/html/rfc9470)

## Relationship to OpenID Connect

RFC 9470 reuses the OpenID Connect request parameters:

- `acr_values` (authentication strength / context)
- `max_age` (authentication recency)

to ensure that clients can request specific authentication properties in a familiar, standardized way when initiating the step-up flow. [RFC 9470](https://datatracker.ietf.org/doc/html/rfc9470)

## See also

- **OAuth 2.0 Bearer Token Usage (RFC 6750)** (defines the Bearer challenge framework that RFC 9470 extends): https://datatracker.ietf.org/doc/html/rfc6750
- **OAuth 2.0 Token Introspection (RFC 7662)**: https://datatracker.ietf.org/doc/html/rfc7662

## References

- Bertocci, V. and Campbell, B., "OAuth 2.0 Step Up Authentication Challenge Protocol", **RFC 9470**, September 2023. https://datatracker.ietf.org/doc/html/rfc9470
- Hardt, D., "The OAuth 2.0 Authorization Framework", **RFC 6749**, October 2012. https://datatracker.ietf.org/doc/html/rfc6749
- Jones, M. and Hardt, D., "The OAuth 2.0 Authorization Framework: Bearer Token Usage", **RFC 6750**, October 2012. https://datatracker.ietf.org/doc/html/rfc6750
- Sakimura, N. et al., "OpenID Connect Core 1.0", November 2014. https://openid.net/specs/openid-connect-core-1_0.html
- Richer, J., Jones, M., Bradley, J., Machulak, M., and Hunt, P., "OAuth 2.0 Token Introspection", **RFC 7662**, October 2015. https://datatracker.ietf.org/doc/html/rfc7662
