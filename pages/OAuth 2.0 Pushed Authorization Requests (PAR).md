# OAuth 2.0 Pushed Authorization Requests (PAR)

**OAuth 2.0 Pushed Authorization Requests** (**PAR**) is an OAuth 2.0 extension that adds a *back-channel* way for clients to submit the parameters of an authorization request to an authorization server. Instead of placing the full authorization request in the front-channel authorization endpoint URL, the client sends the request parameters to a dedicated **pushed authorization request endpoint** and receives a short-lived **request URI** that is then used at the authorization endpoint.

PAR is standardized by the IETF as **RFC 9126** (September 2021).

## Overview

In a conventional OAuth 2.0 authorization code flow, the client constructs an authorization request and redirects the user agent to the authorization endpoint with request parameters in the URL query (or, for some response modes, in the fragment or form post). PAR changes this by moving most request parameters to a server-to-server call.

A typical PAR-based sequence is:

1. The client sends the authorization request parameters to the authorization server’s **PAR endpoint**.
2. The authorization server validates the request and returns a `request_uri` value (and an expiration time).
3. The client redirects the user agent to the authorization endpoint, including the returned `request_uri` (and typically `client_id`).
4. The authorization server retrieves the pushed request parameters associated with that `request_uri` and continues processing the authorization request.

## Request URI

The `request_uri` returned from the PAR endpoint is a reference to the stored authorization request parameters on the authorization server.

RFC 9126 specifies that:

- The client uses the `request_uri` parameter at the authorization endpoint.
- The `request_uri` value is intended to be **single-use** and **short-lived**.
- The authorization server controls the format and meaning of the `request_uri` value.

PAR builds on the earlier concept of OAuth 2.0 **request objects** (JWT-encoded authorization requests) and can be used with request objects as well.

## Motivations and security considerations

PAR is commonly used to reduce exposure and manipulation of authorization request parameters in the front channel. Benefits discussed in RFC 9126 and related deployment guidance include:

- **Reduced URL size and leakage**: large request parameters (for example, rich authorization details or request objects) are not placed in the browser URL, which can be logged or leaked via referrers.
- **Server-side validation before redirect**: the authorization server can validate pushed parameters early and reject invalid or unauthorized requests before involving the user agent.
- **Stronger binding to the client**: when the PAR endpoint requires client authentication, the pushed request becomes tied to an authenticated client.

PAR does not remove the need for TLS; it is specified for use with HTTPS.

## Relationship to other specifications

PAR is often discussed alongside other OAuth and OpenID Connect extensions that harden the authorization request and response:

- **JWT Secured Authorization Response Mode (JARM)**, which encodes authorization responses as signed (and optionally encrypted) JWTs.
- **Demonstrating Proof of Possession (DPoP)**, which can sender-constrain access tokens.

## References

1. IETF. *RFC 9126: OAuth 2.0 Pushed Authorization Requests.* September 2021. https://datatracker.ietf.org/doc/html/rfc9126
2. OAuth.net. *Pushed Authorization Requests.* https://oauth.net/2/pushed-authorization-requests/
