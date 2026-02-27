# OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents

**OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents** is an Internet-Draft that proposes an extension to the OAuth 2.0 Authorization Framework to support explicit, user-consented delegation to an AI agent (the “actor”) when accessing protected resources on a user’s behalf. The draft extends the OAuth 2.0 authorization code flow with parameters intended to identify the delegated agent at the authorization endpoint and authenticate the agent at the token endpoint.

## Overview

OAuth 2.0 is commonly used to authorize applications (“clients”) to access protected resources on behalf of a resource owner (the “user”). The draft argues that common OAuth 2.0 flows do not directly model an AI agent as a distinct party in the delegation chain, and proposes additional protocol elements to make the agent explicit and auditable in the resulting access token.

The draft describes a flow in which:

- A client initiates an OAuth 2.0 authorization request that includes a parameter identifying the requested agent (“actor”) for which the user is delegating authority.
- After user consent, the client exchanges the authorization code at the token endpoint and includes an “actor token” that authenticates the agent.
- The authorization server validates that the authenticated agent matches the agent for which the user granted consent, and issues an access token that documents the delegation chain.

The draft also describes a variant where the flow can be initiated by a resource server challenge, so that user consent is obtained dynamically when access is attempted.

## Proposed protocol elements

The draft introduces two main parameters:

- **`requested_actor`**: an authorization request parameter used to identify the specific agent for which delegation is being requested.
- **`actor_token`**: a token request parameter used to authenticate the agent during the authorization code exchange.

The draft further describes access token claims intended to record the delegation chain (user → client → actor) for transparency and auditability.

## Relationship to adjacent ecosystem concepts

The draft positions a “resource server” broadly, including examples such as a Model Context Protocol (MCP) server or another agent, and frames the extension as enabling dynamic, consent-driven delegation when an agent attempts to access protected resources.

## Status

As an Internet-Draft, the document is a work in progress published through the IETF datatracker and may be updated, replaced, or expired.

The HTML rendering of version -02 indicates it was published in August 2025 and (as of that version) was scheduled to expire on 27 February 2026.

## References

- Thilina Senarath; Ayesha Dissanayaka. *OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents* (Internet-Draft). IETF Datatracker. https://datatracker.ietf.org/doc/draft-oauth-ai-agents-on-behalf-of-user/
- Thilina Senarath; Ayesha Dissanayaka. *OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents* (draft-oauth-ai-agents-on-behalf-of-user-02, HTML). IETF Datatracker. https://datatracker.ietf.org/doc/html/draft-oauth-ai-agents-on-behalf-of-user-02
