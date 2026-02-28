# OAuth 2.0 Authorization Server Issuer Identification (RFC 9207)

**OAuth 2.0 Authorization Server Issuer Identification** is an OAuth 2.0 extension standardized as **RFC 9207**. It defines an `iss` response parameter that lets an authorization server explicitly identify itself in the front-channel authorization response, providing a mitigation for **OAuth “mix-up” attacks** in deployments where a client interacts with multiple authorization servers. [^rfc9207]

## What problem it addresses

In the OAuth 2.0 authorization code flow (and other flows that return an authorization response via the user agent), the authorization response defined by OAuth 2.0 does not inherently identify which authorization server issued it. This can be problematic for clients that support multiple authorization servers: an attacker who controls (or can introduce) one authorization server can attempt to confuse the client about the response’s origin, enabling **mix-up attacks** that can lead to disclosure or misdelivery of authorization codes or tokens. [^rfc9207]

RFC 9207 adds an explicit issuer identifier so the client can validate that the response came from the authorization server it intended to use.

## Core mechanism: the `iss` response parameter

RFC 9207 defines a new response parameter:

- `iss` — the **issuer identifier** of the authorization server that created the authorization response. The value is the same “issuer identifier” concept defined in **OAuth 2.0 Authorization Server Metadata (RFC 8414)**, and is a URL using the `https` scheme without query or fragment components. [^rfc9207]

### Authorization server requirements (high level)

An authorization server that supports RFC 9207:

- **MUST** include the `iss` parameter in authorization responses (including error responses). [^rfc9207]
- If it publishes metadata via RFC 8414, it indicates support using the metadata parameter `authorization_response_iss_parameter_supported` set to `true`, and the metadata `issuer` value must match the `iss` value used in responses. [^rfc9207]

### Client validation (high level)

A client that supports RFC 9207:

- Extracts and URL-decodes the `iss` parameter if present.
- Compares it to the expected issuer identifier for the authorization server it sent the authorization request to.
- Rejects the authorization response if the issuer does not match (simple string comparison as defined by RFC 3986). [^rfc9207]

## Relationship to OAuth security best practices

RFC 9207 is motivated by the mix-up attack class described in OAuth security analyses and best-current-practice guidance. It is one of a set of extensions used in “high security OAuth” deployments alongside mechanisms such as **Pushed Authorization Requests (PAR, RFC 9126)** and **Demonstration of Proof of Possession (DPoP, RFC 9449)**. [^oauthnet]

## See also

- [OAuth 2.0 Authorization Server Metadata (RFC 8414)](https://www.rfc-editor.org/rfc/rfc8414.html)
- [Pushed Authorization Requests (RFC 9126)](./Pushed%20Authorization%20Requests%20(PAR,%20RFC%209126).md)
- [OAuth 2.0 Demonstrating Proof-of-Possession at the Application Layer (DPoP, RFC 9449)](./OAuth%20DPoP%20(RFC%209449).md)

## References

[^rfc9207]: K. Meyer zu Selhausen; D. Fett. *OAuth 2.0 Authorization Server Issuer Identification*. RFC 9207 (Proposed Standard), March 2022. https://www.rfc-editor.org/rfc/rfc9207.html (See also: https://www.rfc-editor.org/info/rfc9207)

[^oauthnet]: OAuth.net. *OAuth 2.0* (overview and extension index; includes RFC 9207). https://oauth.net/2/
