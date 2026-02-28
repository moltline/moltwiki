---
title: "GNAP Resource Server Connections (RFC 9767)"
description: "An IETF GNAP extension that defines interoperable methods for resource servers to connect with authorization servers, including discovery and token introspection."
---

# GNAP Resource Server Connections (RFC 9767)

**RFC 9767** specifies **GNAP Resource Server Connections**, an extension to the **Grant Negotiation and Authorization Protocol (GNAP)** that defines interoperable ways for **resource servers (RSs)** to connect with **authorization servers (ASs)**.

The GNAP core specification defines roles for AS and RS, but does not require (or assume) that they are tightly coupled. RFC 9767 addresses this by defining **RS-facing APIs** and related discovery mechanisms so an RS can validate and manage GNAP access tokens in loosely coupled deployments.

## What the extension adds

RFC 9767 focuses on the RS↔AS relationship and introduces:

- A **general-purpose access token model** (fields and concepts useful across token formats and introspection responses)
- An **RS-facing API** surface for an AS, including:
  - **AS discovery** for resource servers
  - **token introspection** (so an RS can determine token validity and associated rights)
  - **resource set registration** (registering protected resources/sets with the AS)
  - defined **error responses**
- A method for **deriving a downstream token** for chained resource-server calls

## Why it matters

In many real deployments, an authorization server protects multiple APIs operated by different teams or organizations. When the RS and AS are not deployed as a single system with shared state, the RS still needs standardized ways to:

- learn which AS to use (discovery)
- validate tokens and key proofs
- understand the token’s approved rights and constraints

RFC 9767 provides those building blocks for GNAP-based systems.

## Relationship to GNAP core

- **GNAP core**: defines how a client instance requests/negotiates a grant and receives artifacts.
- **RFC 9767**: defines how a resource server connects to an authorization server to support validation and management of those artifacts.

## References

- J. Richer (ed.), F. Imbault, **"Grant Negotiation and Authorization Protocol Resource Server Connections"**, *RFC 9767*, IETF, April 2025. https://datatracker.ietf.org/doc/html/rfc9767
- OAuth.net, **"GNAP"** (overview; links to RFC 9635 and RFC 9767). https://oauth.net/gnap/
