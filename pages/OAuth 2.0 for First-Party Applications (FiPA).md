---
title: OAuth 2.0 for First-Party Applications (FiPA)
---

# OAuth 2.0 for First-Party Applications (FiPA)

**OAuth 2.0 for First-Party Applications** (often abbreviated **FiPA**) is an Internet-Draft in the IETF OAuth working group that proposes an extension to OAuth 2.0 enabling *first-party* client applications to obtain user authorization through a primarily **native (browserless) user experience**, using traditional browser-based authorization flows as a fallback in higher-risk or error conditions. It introduces an **Authorization Challenge Endpoint** intended to let a client collect user input directly and exchange it for an authorization result.\
\
FiPA is positioned as an alternative to the best practice in **OAuth 2.0 for Native Apps** (RFC 8252), which recommends using an external user-agent (system browser) for authorization requests from native applications.

## Overview

The draft describes a protocol in which:

- The client collects initial information from the user.
- The client sends a request to a new **Authorization Challenge Endpoint**.
- The authorization server responds with either an **authorization code** or an **error** indicating additional steps (including the possibility of redirecting to a browser-based flow).

The draft frames this as supporting native “in-app” experiences while retaining browser redirection as a fallback in “unexpected, high risk, or error conditions.”

## Relationship to agentic systems

In agentic applications (e.g., autonomous agents that initiate actions on behalf of a user), authorization UX and phishing resistance are recurring concerns. FiPA is relevant insofar as it:

- explicitly discusses **phishing** and user-experience risk in the context of first-party clients, and
- references the use of **sender-constrained tokens**, including **DPoP** (RFC 9449), as part of its security considerations.

FiPA is not specific to AI agents, but its focus on native authorization experiences intersects with agentic application design, especially where an “agent UI” aims to keep the user in one surface while still performing OAuth-based authorization.

## Status

FiPA is published as an **Internet-Draft** (work in progress) and may change or expire; it is not an RFC as of its current draft versions.

## References

- Aaron Parecki, et al. **“OAuth 2.0 for First-Party Applications”** (Internet-Draft, IETF Datatracker). https://datatracker.ietf.org/doc/draft-ietf-oauth-first-party-apps/
- IETF. **“OAuth 2.0 for Native Apps”** (RFC 8252). https://www.rfc-editor.org/rfc/rfc8252.html
- IETF. **“OAuth 2.0 Demonstrating Proof-of-Possession at the Application Layer (DPoP)”** (RFC 9449). https://www.rfc-editor.org/rfc/rfc9449.html
