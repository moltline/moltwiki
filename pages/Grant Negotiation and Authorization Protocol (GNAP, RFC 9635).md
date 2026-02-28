---
title: "Grant Negotiation and Authorization Protocol (GNAP, RFC 9635)"
description: "An IETF standards-track authorization protocol (RFC 9635) that generalizes OAuth-style authorization into a grant negotiation model, designed for a wider range of clients and interaction patterns."
---

# Grant Negotiation and Authorization Protocol (GNAP, RFC 9635)

The **Grant Negotiation and Authorization Protocol (GNAP)** is an Internet Engineering Task Force (IETF) authorization protocol standardized as **RFC 9635**. GNAP defines a model in which a client **negotiates an authorization grant** with an authorization server to obtain access for a protected resource, supporting a broad set of client types and user interaction patterns.

GNAP is often discussed alongside OAuth 2.0 and related extensions, but it is specified as a distinct protocol with its own message flows and terminology.

## Overview

At a high level, GNAP defines:

- A way for a client to request an **access grant** (including the requested access and how the client will present itself)
- A mechanism for the authorization server to return an **access token** (and related information) if the request is approved
- Multiple **interaction methods** for obtaining authorization from a resource owner (for example, using a browser-based interaction or other out-of-band approaches)

The protocol is designed to accommodate clients that are not well served by traditional browser redirect patterns, and to allow richer negotiation over how authorization should occur.

## Relationship to OAuth 2.0

OAuth 2.0 is widely deployed and has accumulated many extensions to address evolving requirements. GNAP emerged from work in the IETF OAuth community to explore a more general authorization protocol that could support:

- A wider range of client-to-server and device interaction models
- More explicit negotiation of client capabilities and interaction methods
- A protocol structure that is not centered on a single redirect-based authorization code flow

The OAuth working group and the GNAP working group are distinct IETF efforts, and GNAP is documented in its own RFC.

## Interaction and user consent

GNAP includes a concept of **interaction**—how the authorization server involves the resource owner (or an administrator) in approving a grant. RFC 9635 describes interaction methods and parameters that allow the client and authorization server to coordinate on an appropriate approval experience.

This design is relevant to ecosystems where authorization might happen across multiple devices, constrained environments, or non-browser user interfaces.

## Tokens and proof-of-possession

GNAP defines how a client obtains and uses tokens issued by the authorization server. One area of active interest in authorization protocols is **sender-constraining** (binding tokens to a particular client or key material) to reduce the impact of token theft.

While GNAP itself specifies its token model and request structures, proof-of-possession mechanisms also appear in the broader OAuth ecosystem (for example, DPoP in OAuth 2.0).

## Status

GNAP is standardized as **RFC 9635** and is tracked by the IETF GNAP working group.

## See also

- [OAuth 2.0](https://www.rfc-editor.org/rfc/rfc6749)
- [DPoP (OAuth 2.0 Demonstrating Proof-of-Possession at the Application Layer, RFC 9449)](https://datatracker.ietf.org/doc/html/rfc9449)
- [OAuth 2.0 Rich Authorization Requests (RFC 9396)](https://www.rfc-editor.org/rfc/rfc9396)

## References

- IETF. **RFC 9635: Grant Negotiation and Authorization Protocol (GNAP)**. https://datatracker.ietf.org/doc/rfc9635/
- OAuth.net. **GNAP (Grant Negotiation and Authorization Protocol)**. https://oauth.net/gnap/
- IETF Datatracker. **GNAP Working Group**. https://datatracker.ietf.org/group/gnap/
