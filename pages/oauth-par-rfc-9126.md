---
title: "OAuth 2.0 Pushed Authorization Requests (RFC 9126)"
description: "IETF standard that lets OAuth clients push authorization request parameters to the authorization server via a back-channel endpoint, receiving a short-lived request_uri reference used in the front-channel authorization request."
---

**OAuth 2.0 Pushed Authorization Requests (PAR)** is an extension to OAuth 2.0 that adds a **PAR endpoint** at the authorization server. Instead of sending all authorization request parameters through the user agent as query parameters, the client **POSTs** the parameters directly to the authorization server and receives a **`request_uri`** reference. The client then initiates the normal front-channel authorization request by redirecting the user agent to the authorization endpoint with that `request_uri`.  
https://www.rfc-editor.org/rfc/rfc9126

PAR is specified in **[RFC 9126](https://www.rfc-editor.org/rfc/rfc9126)** (Standards Track, September 2021).

## Motivation

In “classic” OAuth 2.0 flows, the authorization request is commonly sent via a browser redirect with parameters in the URL. RFC 9126 highlights several challenges with that pattern:

- **Lack of integrity protection** for request parameters when they traverse the user agent (e.g., tampering with `scope` or transaction context).  
  https://www.rfc-editor.org/rfc/rfc9126
- **Potential confidentiality leaks** of request parameters (e.g., via browser history, logs, or referrers), even when the authorization endpoint uses HTTPS.  
  https://www.rfc-editor.org/rfc/rfc9126
- **Practical URL size limits** for large or fine-grained authorization requests.  
  https://www.rfc-editor.org/rfc/rfc9126

PAR is designed to mitigate these issues by moving the full request payload to a **back-channel** call from the client to the authorization server.

## How PAR works

At a high level, PAR splits the authorization request into two steps:

1. **Back-channel push**: the client sends an HTTP POST to the authorization server’s PAR endpoint with the authorization request parameters.
2. **Reference returned**: the authorization server responds with a **`request_uri`** (and an **`expires_in`** lifetime).
3. **Front-channel redirect**: the client redirects the user agent to the authorization endpoint with (at least) `client_id` and `request_uri`.

RFC 9126 includes an introductory example showing the POST to the PAR endpoint and the subsequent authorization request that uses `request_uri`.  
https://www.rfc-editor.org/rfc/rfc9126

### Relationship to JAR (RFC 9101)

RFC 9126 is designed to complement **JWT-Secured Authorization Request (JAR)**, which packages authorization request parameters into a signed (and optionally encrypted) JWT “Request Object”. PAR provides an interoperable way to obtain a `request_uri` reference by pushing the request data directly to the authorization server.  
https://www.rfc-editor.org/rfc/rfc9126

In practice, deployments may use:

- **PAR without JAR** (pushing standard OAuth parameters),
- **JAR without PAR** (sending a signed request object directly), or
- **JAR + PAR** (pushing a signed/encrypted request object and then using `request_uri` in the front-channel).

## Security properties

PAR can improve the security of OAuth authorization requests by:

- Allowing the authorization server to **authenticate the client before user interaction**, enabling earlier rejection of illegitimate requests.  
  https://www.rfc-editor.org/rfc/rfc9126
- Reducing exposure of sensitive request parameters to the browser and intermediaries, since the full request payload is sent over the back-channel.  
  https://www.rfc-editor.org/rfc/rfc9126
- Providing a standardized mechanism for using a short-lived `request_uri` reference, which can help address large request sizes and reduce accidental leakage of long query strings.  
  https://www.rfc-editor.org/rfc/rfc9126

RFC 9126 also discusses specific threats and considerations such as **request URI guessing**, **open redirection**, **request object replay**, and **request URI swapping**.  
https://www.rfc-editor.org/rfc/rfc9126

## Protocol details (selected)

- The PAR endpoint returns JSON containing `request_uri` and `expires_in`.  
  https://www.rfc-editor.org/rfc/rfc9126
- The subsequent authorization request uses the `request_uri` parameter to refer to the previously pushed request data.  
  https://www.rfc-editor.org/rfc/rfc9126

## References

- RFC 9126: OAuth 2.0 Pushed Authorization Requests — https://www.rfc-editor.org/rfc/rfc9126
- RFC 6749: The OAuth 2.0 Authorization Framework — https://www.rfc-editor.org/rfc/rfc6749
- RFC 9101: The OAuth 2.0 Authorization Framework: JWT-Secured Authorization Request (JAR) — https://www.rfc-editor.org/rfc/rfc9101
- RFC 8252: OAuth 2.0 for Native Apps — https://www.rfc-editor.org/rfc/rfc8252
