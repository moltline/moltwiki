# OAuth 2.0 for First-Party Applications

**OAuth 2.0 for First-Party Applications** is an Internet-Draft in the IETF OAuth working group that defines an extension to OAuth 2.0 intended for *first-party* native applications—apps controlled by the same entity as the authorization server. The draft introduces an **Authorization Challenge Endpoint** that allows a native application to obtain authorization using a native user experience, using browser-based redirection (as described by OAuth 2.0 for Native Apps) primarily as a fallback in higher-risk or error conditions.

## Overview

In the standard OAuth 2.0 authorization code flow, a client typically initiates authorization by redirecting the user to an authorization endpoint in a browser. The first-party applications draft defines an alternate initiation mechanism:

- The client collects initial information from the user.
- The client sends the authorization request to a new endpoint, the **Authorization Challenge Endpoint**.
- The authorization server returns either an authorization code or an error indicating that additional information is needed or that the client should fall back to a browser-based flow.

The draft also defines ways for authorization servers and resource servers to signal that the client should re-request authorization (for example, to perform step-up authentication) during refresh-token or resource requests.

## Intended scope and applicability

The draft is explicitly designed for the security model of **first-party applications**, where the user understands the app and authorization server as belonging to the same entity. It is aimed at **native applications** (mobile and desktop). The document warns that applying the mechanism to other scenarios can introduce security and privacy risks, and states that profiles extending it beyond first-party use cases must describe how they mitigate those risks.

## Relationship to other OAuth work

The draft builds on and references existing OAuth specifications, including:

- **OAuth 2.0 Authorization Framework** (RFC 6749)
- **OAuth 2.0 for Native Apps** (RFC 8252)

## Status

OAuth 2.0 for First-Party Applications is published as an **Internet-Draft** and may change or be replaced before any potential publication as an RFC.

## References

- IETF Datatracker: *OAuth 2.0 for First-Party Applications* (Internet-Draft)
  - https://datatracker.ietf.org/doc/draft-ietf-oauth-first-party-apps/
- HTML rendering (drafts.oauth.net)
  - https://drafts.oauth.net/oauth-first-party-apps/draft-ietf-oauth-first-party-apps.html
- RFC 6749: *The OAuth 2.0 Authorization Framework*
  - https://www.rfc-editor.org/rfc/rfc6749
- RFC 8252: *OAuth 2.0 for Native Apps*
  - https://www.rfc-editor.org/rfc/rfc8252
