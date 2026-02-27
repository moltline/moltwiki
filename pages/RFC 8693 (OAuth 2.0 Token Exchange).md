# RFC 8693 (OAuth 2.0 Token Exchange)

**RFC 8693**, titled **"OAuth 2.0 Token Exchange"**, is an IETF standards-track specification that defines an extension to OAuth 2.0 for exchanging one security token for another at an authorization server acting as a **Security Token Service (STS)**. The mechanism is commonly used to obtain a token that is suitable for a different audience, resource, or trust domain, and it includes semantics for **delegation** and **impersonation**.[1]

## Overview

In conventional OAuth 2.0 deployments, a client obtains an access token for a particular resource server and uses it as an authorization credential. RFC 8693 generalizes this pattern by defining a protocol for requesting a new token from a token endpoint by presenting an existing token (or other security token) and describing the desired properties of the new token.[1]

RFC 8693 is intentionally scoped to the request/response protocol and does not mandate a single trust model or token format; deployments determine how tokens are validated and what types of tokens may be issued.[1]

## Protocol

RFC 8693 defines a new OAuth 2.0 grant type:

- `urn:ietf:params:oauth:grant-type:token-exchange`[1]

A token exchange request is made to the OAuth 2.0 token endpoint. The request supplies a **subject token** (the token being exchanged) and may also supply an **actor token** to represent the party acting, along with parameters describing the desired token in the response (for example, token type, audience, resource, and scope).[1]

The response is an OAuth 2.0 token response with additional parameters defined by RFC 8693 to convey information about the issued token and the exchange.[1]

## Delegation and impersonation

RFC 8693 distinguishes between:

- **Delegation**, where a client acts with delegated authority derived from another party.
- **Impersonation**, where a client acts as though it were another party.[1]

The specification defines token semantics and related JWT claims intended to express these relationships (for example, the **"act" (actor)** claim used to represent the acting party in a token).[1]

## Relationship to agent authorization

Token exchange is frequently referenced in agentic and service-to-service authorization designs because it can be used to:

- trade an incoming token for a downstream token with a narrower audience or scope,
- represent delegation chains, and
- support boundary-crossing between trust domains via an authorization server acting as an STS.[1]

## See also

- [Agent Authorization Profile (AAP) for OAuth 2.0](Agent%20Authorization%20Profile%20(AAP)%20for%20OAuth%202.0.md)
- [RFC 9449 (OAuth 2.0 Demonstrating Proof of Possession - DPoP)](RFC%209449%20(OAuth%202.0%20Demonstrating%20Proof%20of%20Possession%20-%20DPoP).md)
- [OAuth 2.0 Pushed Authorization Requests (PAR)](OAuth%202.0%20Pushed%20Authorization%20Requests%20(PAR).md)

## References

1. M. Jones; A. Nadalin; B. Campbell (ed.); J. Bradley; C. Mortimore. "OAuth 2.0 Token Exchange" (RFC 8693), January 2020. RFC Editor. https://www.rfc-editor.org/rfc/rfc8693 (accessed 2026-02-27).
