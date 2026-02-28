# OAuth 2.1

**OAuth 2.1** is an in-progress revision of the OAuth 2.0 authorization framework being developed in the IETF OAuth Working Group. It aims to consolidate widely-deployed OAuth 2.0 best practices and security guidance into a single, updated core specification, and it is intended to **replace and obsolete** OAuth 2.0 as defined in [RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749) and bearer token usage in [RFC 6750](https://datatracker.ietf.org/doc/html/rfc6750). The work is published as an Internet-Draft titled *The OAuth 2.1 Authorization Framework* (e.g., `draft-ietf-oauth-v2-1`).

## Overview

OAuth is a delegated authorization protocol: a client obtains an access token from an authorization server and uses that token to access protected resources at a resource server. OAuth 2.1 keeps the same high-level roles and flows as OAuth 2.0, but updates the baseline requirements to reflect current security expectations.

Because OAuth 2.1 is an **Internet-Draft**, it can change until it is finalized as an RFC, and implementations should track the draft version they target.

## Goals

OAuth 2.1’s stated goals include:

- **Consolidation**: fold common extensions and deployment guidance into the core framework rather than leaving them as optional add-ons.
- **Security hardening**: require or strongly encourage practices that mitigate known attacks against OAuth 2.0 deployments.
- **Simplification**: remove legacy or problematic features that are no longer recommended.

## Notable changes from OAuth 2.0

The OAuth 2.1 draft includes a section describing differences from OAuth 2.0. Notable changes include:

- **Removal of the Implicit grant**: OAuth 2.1 removes the OAuth 2.0 Implicit grant from the core framework, reflecting long-standing guidance to avoid it in favor of Authorization Code with PKCE for browser-based apps.
- **Emphasis on modern client patterns**: the draft discusses current deployment considerations for native apps and browser-based apps, including redirect URI handling.

For security guidance that complements (and is referenced by) OAuth 2.1 work, see *OAuth 2.0 Security Best Current Practice* ([RFC 9700](https://datatracker.ietf.org/doc/html/rfc9700)).

## Relationship to other OAuth specifications

OAuth 2.1 is part of a broader ecosystem of OAuth and OpenID Connect specifications and extensions. For example:

- **PKCE** (*Proof Key for Code Exchange*) mitigates authorization code interception attacks and is widely used with the Authorization Code flow ([RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)).
- **Sender-constrained tokens** bind tokens to a client to reduce replay risk; one application-layer mechanism is DPoP (*Demonstrating Proof of Possession*) ([RFC 9449](https://www.rfc-editor.org/rfc/rfc9449.html)).

## References

- D. Hardt, D. Hellō, A. Parecki, T. Lodderstedt, *The OAuth 2.1 Authorization Framework* (Internet-Draft), `draft-ietf-oauth-v2-1` (work in progress): https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/
- D. Hardt, *The OAuth 2.0 Authorization Framework*, [RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749)
- M. Jones, D. Hardt, *The OAuth 2.0 Authorization Framework: Bearer Token Usage*, [RFC 6750](https://datatracker.ietf.org/doc/html/rfc6750)
- D. Lodderstedt et al., *Best Current Practice for OAuth 2.0 Security*, [RFC 9700](https://datatracker.ietf.org/doc/html/rfc9700)
- N. Sakimura et al., *Proof Key for Code Exchange by OAuth Public Clients*, [RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)
- J. Fett et al., *OAuth 2.0 Demonstrating Proof of Possession (DPoP)*, [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449.html)
