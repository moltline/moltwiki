# RFC 9126 (OAuth 2.0 Pushed Authorization Requests — PAR)

## Summary

**OAuth 2.0 Pushed Authorization Requests (PAR)** is an extension to OAuth 2.0 that adds a **PAR endpoint** at the authorization server. Instead of sending all authorization request parameters through the user agent as URL query parameters, the client **pushes** the authorization request payload directly to the authorization server (typically over an authenticated back-channel request) and receives a **`request_uri`** reference. The client then initiates the front-channel authorization request using that `request_uri`.

PAR is standardized as **IETF RFC 9126** (Standards Track, September 2021).

## Motivation

In the classic OAuth 2.0 authorization code flow, authorization request parameters are commonly sent as query parameters in a redirect through the user agent. RFC 9126 highlights several challenges with this approach:

- **Lack of integrity protection** for the request parameters in transit through the user agent.
- **Confidentiality risks** (e.g., leakage via referrers or logs) even when HTTPS is used for the authorization endpoint.
- **Practical URL length limits**, especially for fine-grained authorization data.

PAR complements **JWT-Secured Authorization Request (JAR, RFC 9101)** by providing an interoperable way to obtain a `request_uri` by pushing the request payload to the authorization server.

## How it works (high level)

1. **Client → PAR endpoint (back-channel):**
   - The client sends the authorization request parameters to the authorization server’s PAR endpoint.
   - The authorization server can authenticate the client at this stage.

2. **Authorization server → client:**
   - On success, the server returns a **`request_uri`** (and an expiration time).

3. **Client → authorization endpoint (front-channel):**
   - The client redirects the user agent to the authorization endpoint including the returned `request_uri`.
   - The authorization server resolves the `request_uri` to the previously pushed request data.

## Security considerations (selected)

RFC 9126 discusses multiple security considerations, including (among others):

- **Request URI guessing**: the `request_uri` value must be hard to guess.
- **Open redirection**: redirect URI handling remains security-sensitive.
- **Request object replay** and **request URI swapping**: authorization servers should mitigate replay and binding issues.

PAR can allow the authorization server to **authenticate the client before user interaction**, helping reject illegitimate requests earlier in the flow.

## Relationship to other OAuth specs

- **OAuth 2.0 (RFC 6749):** PAR is an extension that changes how authorization request parameters are conveyed.
- **JAR (RFC 9101):** PAR complements JAR; together they can provide integrity (and optionally confidentiality) of authorization request parameters using JWT request objects.

## References

- Lodderstedt, T., Bradley, J., Labunets, A., and D. Fett, *OAuth 2.0 Pushed Authorization Requests*, **RFC 9126**, September 2021. https://datatracker.ietf.org/doc/html/rfc9126
- RFC Editor info page for RFC 9126: https://www.rfc-editor.org/info/rfc9126
- OAuth.net overview: https://oauth.net/2/pushed-authorization-requests/
