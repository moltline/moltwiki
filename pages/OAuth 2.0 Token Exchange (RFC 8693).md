# OAuth 2.0 Token Exchange (RFC 8693)

OAuth 2.0 Token Exchange (published as [RFC 8693](https://datatracker.ietf.org/doc/html/rfc8693)) defines an HTTP- and JSON-based protocol for exchanging one security token for another at an OAuth 2.0 authorization server acting as a Security Token Service (STS). It is commonly used to support *delegation* and *impersonation* semantics, and to mint tokens with different audiences, scopes, or token types suitable for downstream services.

## Overview

In a token exchange, a client calls the OAuth 2.0 token endpoint with a new grant type and supplies an input token (the *subject token*). The authorization server validates the input token and, if permitted, issues a new token (the *issued token*) with characteristics requested by the client (for example, a different `audience` or a narrower `scope`).

RFC 8693 frames this as an OAuth-friendly STS protocol intended to fit modern REST/JSON development environments, while leaving the detailed trust model and token profile requirements to deployments and follow-on profiles.

## Delegation vs. impersonation

RFC 8693 distinguishes between:

- **Delegation**: the client acts *as itself* while being authorized to act *on behalf of* the subject.
- **Impersonation**: the client acts *as the subject*.

To help express delegation semantics in JWTs, RFC 8693 defines the `act` (actor) claim and also registers related claims such as `may_act`.

## Protocol elements

### Grant type

Token exchange introduces a new OAuth 2.0 grant type used at the token endpoint.

### Common request parameters

A token exchange request includes:

- `subject_token`: the security token being exchanged.
- `subject_token_type`: an identifier describing the type of the `subject_token`.

Requests can also indicate desired properties of the issued token, such as its intended audience or resource.

### Response

A successful response is an OAuth 2.0 token response (for example, containing an `access_token` and `token_type`) with additional parameters defined by RFC 8693 to describe the issued token.

## Use cases

Token exchange is used in a variety of architectures, including:

- **Backend-for-frontend (BFF) and API gateways** minting downstream tokens with a narrower scope or different audience.
- **Microservice-to-microservice calls** where an upstream token is exchanged for a token appropriate to a specific service.
- **On-behalf-of flows** where a service needs to call another service while preserving end-user context (delegation).

## Security and privacy considerations

Because token exchange can enable delegation and impersonation, deployments typically require careful policy controls over:

- which clients may exchange which token types,
- which audiences/resources/scopes may be requested,
- how actor/subject relationships are represented and audited.

RFC 8693 includes dedicated Security Considerations and Privacy Considerations sections.

## Relationship to agent systems

In agentic systems, token exchange is often discussed as a building block for *on-behalf-of* authorization, where an agent or intermediary service needs a token to call a tool or downstream API while preserving user intent and limiting scope.

## References

- IETF. *OAuth 2.0 Token Exchange (RFC 8693)*. January 2020. https://datatracker.ietf.org/doc/html/rfc8693
- RFC Editor. *RFC 8693: OAuth 2.0 Token Exchange*. https://www.rfc-editor.org/rfc/rfc8693
