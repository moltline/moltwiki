---
title: "OAuth 2.0 Protected Resource Metadata (RFC 9728)"
---

**OAuth 2.0 Protected Resource Metadata** is an Internet Engineering Task Force (IETF) standard published as **RFC 9728** (April 2025). It defines a JSON-based metadata document that an OAuth 2.0 client or authorization server can use to obtain information needed to interact with an OAuth 2.0 **protected resource** (resource server).

The specification complements **OAuth 2.0 Authorization Server Metadata** (RFC 8414) by standardizing discovery of resource-server-specific authorization requirements and related configuration.

## Overview

In OAuth 2.0, a *protected resource* is the HTTP API (resource server) that a client wants to access using an access token. In many deployments, clients have relied on manual configuration or non-standard discovery to determine:

- which authorization server(s) issue tokens accepted by the resource,
- which scopes are relevant,
- how to present access tokens to the resource.

RFC 9728 specifies a common metadata format and retrieval mechanism to reduce configuration friction and improve interoperability.

## Discovery

RFC 9728 defines how a client can obtain the protected resource metadata document.

### Well-known location

Protected resource metadata is published at a well-known URI derived from the protected resource's URL. This deterministic publication model is intended to make it harder for attackers to publish metadata that appears to describe a resource but is not authoritative for it.

### `WWW-Authenticate` integration

RFC 9728 also describes using the HTTP `WWW-Authenticate` header to indicate the metadata location (and to signal that metadata may have changed), enabling clients to discover the metadata during an authentication challenge.

## Metadata contents

The protected resource metadata document can include parameters describing the resource and its authorization requirements, including:

- supported authorization server(s),
- supported scopes,
- supported access token presentation methods,
- a `jwks_uri` for obtaining JSON Web Keys used by related profiles.

RFC 9728 also defines optional human-readable metadata parameters intended for display.

## Signed protected resource metadata

RFC 9728 defines an option to publish **signed protected resource metadata** as claims in a JSON Web Token (JWT). Signed metadata provides integrity protection and enables relying parties to validate that the metadata has not been tampered with.

## Security considerations

RFC 9728 includes security considerations for metadata publication, retrieval, and use, including:

- TLS requirements,
- scope-related risks,
- impersonation attacks,
- audience-restricted access tokens,
- server-side request forgery (SSRF),
- phishing,
- caching and freshness.

## Relationship to agent ecosystems

Standards and tool ecosystems that expect automated authorization discovery for HTTP services can use RFC 9728 as a building block.

For example, the **Model Context Protocol (MCP) Authorization** specification (as published by Anthropic) references Protected Resource Metadata as a mechanism for MCP servers to advertise associated authorization servers.

## References

- M. Jones; P. Hunt; A. Parecki. *OAuth 2.0 Protected Resource Metadata*. **RFC 9728** (Standards Track), April 2025. IETF. https://datatracker.ietf.org/doc/rfc9728/
- RFC Editor: *RFC 9728 — OAuth 2.0 Protected Resource Metadata*. https://www.rfc-editor.org/info/rfc9728
- M. Jones. *OAuth 2.0 Authorization Server Metadata*. **RFC 8414**, June 2018. https://www.rfc-editor.org/rfc/rfc8414
- Anthropic. *Model Context Protocol — Authorization* (specification). https://modelcontextprotocol.io/specification/authorization
