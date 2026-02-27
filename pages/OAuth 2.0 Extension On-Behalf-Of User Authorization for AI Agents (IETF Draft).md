---
title: "OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents (IETF Draft)"
---

# OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents (IETF Draft)

This IETF Internet-Draft proposes an OAuth 2.0 extension intended to let **AI agents (actors)** obtain access tokens to act **on behalf of** an end user, while preserving explicit user consent and improving auditability.

## What it proposes

The draft extends the OAuth 2.0 **Authorization Code** flow with two new parameters:

- `requested_actor` (authorization request): identifies the specific agent (actor) for which delegation is being requested.
- `actor_token` (token request): authenticates the agent during the exchange of an authorization code for an access token.

It also describes including delegation information in the resulting access token (for example, claims that identify the user, client, and actor) to make the delegation chain more transparent and auditable.

## Why this matters for agentic systems

Many “tool-using” or autonomous agent architectures need a way to:

- represent that the **user** approved an action,
- represent that a specific **agent** performed it,
- keep the **client app** in the loop for interactive consent,
- and allow resource servers to verify the delegation chain.

OAuth 2.0 already provides a widely deployed consent and token infrastructure; this draft explores a concrete way to adapt it to agent delegation rather than treating an agent as an indistinguishable part of a client application.

## Status and cautions

This is an **Internet-Draft** (work in progress), not an RFC. Internet-Drafts can change or be replaced, and should not be treated as stable standards.

## Sources

- IETF Datatracker: *OAuth 2.0 Extension: On-Behalf-Of User Authorization for AI Agents* (draft-oauth-ai-agents-on-behalf-of-user)
  - https://datatracker.ietf.org/doc/draft-oauth-ai-agents-on-behalf-of-user/
- HTML rendering (version -02)
  - https://datatracker.ietf.org/doc/html/draft-oauth-ai-agents-on-behalf-of-user-02
