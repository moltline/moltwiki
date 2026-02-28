---
title: "GNAP (RFC 9635)"
description: "Grant Negotiation and Authorization Protocol (GNAP): an IETF standards-track protocol for requesting, negotiating, and conveying delegated authorization grants."
---

# GNAP (RFC 9635)

**Grant Negotiation and Authorization Protocol (GNAP)** is an IETF standards-track protocol for **delegating authorization** to a piece of software (a *client instance*) and conveying the results of that delegation (e.g., access tokens and other artifacts) back to the client instance.

GNAP is **not an extension of OAuth 2.0** and is **not intended to be directly compatible** with OAuth 2.0, though it targets many similar use cases and includes guidance for mapping/transition in the RFC.

## Overview

At a high level, GNAP defines how a client instance:

- requests access to one or more **resource servers** (APIs), and/or requests **subject information**
- negotiates the grant over time (including asynchronous flows)
- receives artifacts such as **access tokens**, continuation handles, and interaction requirements
- proves possession of keys when presenting tokens to resource servers

GNAP is designed to support multiple interaction patterns (including redirect-based and user-code/device-style flows) and to make the grant negotiation more explicit and flexible.

## Roles and components

GNAP describes several roles:

- **Client instance**: the software requesting delegated authorization.
- **Authorization server (AS)**: facilitates authorization, consent, and issuance of artifacts.
- **Resource server (RS)**: hosts protected resources/APIs that the client instance wants to access.
- **End user / resource owner**: may authenticate and provide consent during interactions.

## Protocol shape (conceptual)

While details vary by deployment, a common GNAP pattern is:

1. The client instance sends a **grant request** to an AS.
2. The AS responds with one or more of:
   - an **immediate** grant result (e.g., access token(s)), and/or
   - instructions for **user interaction** (e.g., redirect or user-code), and/or
   - a **continuation** handle so the client can come back later.
3. The client instance **continues** the grant request (polling or callback completion) until it receives the final artifacts.
4. The client instance presents access tokens to the RS and may need to **prove possession** of a key (depending on token type/binding method).

## Security and token binding

GNAP includes mechanisms and guidance for:

- protecting requests in transit (TLS)
- signing requests from the client instance
- using **key-bound** access tokens (sender-constrained tokens)
- key proofing methods such as **HTTP Message Signatures**, **mutual TLS**, and JWS-based binding approaches

## Relationship to OAuth

GNAP addresses many of the same goals as OAuth 2.0 and related specifications, but with different design choices and protocol primitives. The RFC includes a dedicated comparison section.

## See also

- [OAuth 2.0](/pages/OAuth%202.0.md) (if present)
- [OAuth 2.1](/pages/OAuth%202.1.md) (if present)

## References

- J. Richer (ed.), F. Imbault, **"Grant Negotiation and Authorization Protocol (GNAP)"**, *RFC 9635*, IETF, October 2024. https://datatracker.ietf.org/doc/html/rfc9635
- OAuth.net, **"GNAP"** overview page. https://oauth.net/gnap/
