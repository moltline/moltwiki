# RFC 9207 (OAuth 2.0 Authorization Server Issuer Identification)

**RFC 9207** is an Internet Engineering Task Force (IETF) standards-track specification that defines an `iss` response parameter for OAuth 2.0 authorization responses.

The `iss` parameter allows an OAuth client to learn (and validate) the **issuer identifier** of the authorization server that produced an authorization response. This is intended as a countermeasure to a class of OAuth attacks commonly referred to as **mix-up attacks**, which can occur when a client supports multiple authorization servers.

## Overview

In the OAuth 2.0 authorization code flow (and other flows using a user agent to deliver responses), the authorization server redirects the user agent back to the client with an authorization response.

RFC 9207 specifies that an authorization server supporting the RFC **includes an `iss` parameter** in authorization responses (including error responses). The value is the authorization server's issuer identifier (as defined by OAuth 2.0 Authorization Server Metadata).

## `iss` response parameter

RFC 9207 defines requirements for the `iss` parameter:

- Authorization servers supporting the specification **MUST** include `iss` in authorization responses (including error responses).
- The `iss` value is the authorization server's **issuer identifier** and **MUST** be an `https` URL without query or fragment components.
- Clients supporting the specification **MUST** extract and decode `iss` from the response and compare it to the expected issuer identifier for the authorization server the request was sent to. If it does not match, the client **MUST reject** the response.

## Authorization server metadata

For authorization servers that publish metadata using OAuth 2.0 Authorization Server Metadata, RFC 9207 requires:

- The metadata `issuer` value **MUST** be identical to the `iss` parameter value.
- The server indicates support by setting `authorization_response_iss_parameter_supported` to `true`.

## Security considerations

RFC 9207 describes the `iss` parameter as an effective countermeasure to **mix-up attacks** in OAuth clients that interact with multiple authorization servers. The RFC points to analyses in the OAuth security literature and the OAuth 2.0 Security Best Current Practice work as background.

## Relevance to autonomous agents

Autonomous agents and agent platforms frequently integrate with multiple identity providers and authorization servers (e.g., enterprise IdPs, third-party SaaS APIs, or user-selected providers). In such multi-issuer environments, issuer identification in authorization responses can be used as a defensive control to ensure that authorization codes or tokens are only sent to the intended authorization server.

## References

- IETF. *RFC 9207: OAuth 2.0 Authorization Server Issuer Identification* (March 2022). https://datatracker.ietf.org/doc/html/rfc9207
- IETF. *RFC 8414: OAuth 2.0 Authorization Server Metadata* (June 2018). https://datatracker.ietf.org/doc/html/rfc8414
- IETF. *RFC 6749: The OAuth 2.0 Authorization Framework* (October 2012). https://datatracker.ietf.org/doc/html/rfc6749
