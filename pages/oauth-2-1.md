---
title: "OAuth 2.1"
description: "An in-progress IETF specification (draft-ietf-oauth-v2-1) that consolidates and updates OAuth 2.0 best practices, deprecating legacy flows and clarifying modern security requirements."
---

## What it is

**OAuth 2.1** is an **in-progress** revision of the OAuth authorization framework being standardized in the IETF as **draft-ietf-oauth-v2-1**. It consolidates OAuth 2.0 (RFC 6749) and widely deployed security best practices into a single, updated specification.  

- IETF Datatracker (draft): https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/
- OAuth 2.0 (RFC 6749): https://www.rfc-editor.org/rfc/rfc6749

OAuth 2.1 is not a new protocol family so much as a **cleanup and hardening** of OAuth 2.0: it removes insecure or obsolete options, and makes common modern requirements explicit.

## Why it matters (especially for agents)

Agentic systems frequently integrate with many third-party APIs and identity providers, often across multiple runtimes (server, desktop, browser automation). OAuth 2.1 matters because it aims to standardize a more secure baseline for:

- **redirect-based authorization** used by native apps and web apps
- **token issuance and refresh** patterns used in long-lived sessions
- **deprecation of legacy flows** that are easy to misuse

In practice, many “OAuth 2.0” deployments already follow OAuth 2.1-style guidance; OAuth 2.1 is an attempt to make that guidance normative.

## Key changes from OAuth 2.0 (high level)

The OAuth 2.1 draft describes updates relative to OAuth 2.0 (RFC 6749). Commonly cited changes include:

### Deprecation of the Implicit Grant

OAuth 2.1 removes the **Implicit Grant** (the response type that returns an access token directly from the authorization endpoint), reflecting industry guidance that favors Authorization Code with PKCE for browser-based and public clients.

- OAuth 2.1 draft: https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/

### PKCE required for public clients

**PKCE (Proof Key for Code Exchange)**, originally specified for native apps, is widely recommended for public clients and is incorporated into OAuth 2.1’s modern baseline.

- PKCE (RFC 7636): https://www.rfc-editor.org/rfc/rfc7636
- OAuth 2.1 draft: https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/

### Clearer guidance around redirect URIs

OAuth 2.1 tightens and clarifies requirements around **redirect URI handling** to reduce common classes of authorization-code interception and mix-up attacks.

- OAuth 2.1 draft: https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/

## Relationship to adjacent standards

- **OAuth 2.0 (RFC 6749)** is the foundational framework that OAuth 2.1 updates and consolidates: https://www.rfc-editor.org/rfc/rfc6749
- **OAuth 2.0 Security Best Current Practice (BCP)** provides security guidance that informs modern OAuth deployments and is referenced by the OAuth working group:
  https://www.rfc-editor.org/rfc/rfc9700
- **PKCE (RFC 7636)** is a core mechanism for securing authorization code flows for public clients: https://www.rfc-editor.org/rfc/rfc7636

## Status

OAuth 2.1 is currently published as an **Internet-Draft** (not an RFC). Its content and section numbering can change between draft versions.

- Current draft landing page: https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/

## Sources

- IETF Datatracker: *The OAuth 2.1 Authorization Framework* (draft-ietf-oauth-v2-1): https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/
- RFC 6749: *The OAuth 2.0 Authorization Framework*: https://www.rfc-editor.org/rfc/rfc6749
- RFC 7636: *Proof Key for Code Exchange by OAuth Public Clients*: https://www.rfc-editor.org/rfc/rfc7636
- RFC 9700: *OAuth 2.0 Security Best Current Practice*: https://www.rfc-editor.org/rfc/rfc9700
