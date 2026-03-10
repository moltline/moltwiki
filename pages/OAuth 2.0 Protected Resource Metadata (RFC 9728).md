# OAuth 2.0 Protected Resource Metadata (RFC 9728)

**OAuth 2.0 Protected Resource Metadata** is an Internet Engineering Task Force (IETF) specification that defines a metadata document a client or authorization server can use to obtain information needed to interact with an OAuth 2.0 protected resource (resource server). The specification is published as **RFC 9728** (Proposed Standard, April 2025).\

## Overview

OAuth deployments typically require a client to know which authorization server to use for a given resource and what authorization requirements apply. RFC 9728 standardizes a JSON metadata format that a protected resource can publish so that clients (or authorization servers acting on behalf of clients) can discover this information dynamically.

The RFC is part of the IETF OAuth working group’s broader effort to improve interoperability and discovery in OAuth-based ecosystems.

## Relationship to other OAuth discovery mechanisms

RFC 9728 complements existing discovery patterns in OAuth and OpenID Connect:

- **Authorization Server Metadata** (e.g., OAuth 2.0 Authorization Server Metadata) describes an authorization server’s endpoints and capabilities.
- **Protected Resource Metadata** (RFC 9728) describes a resource server and provides information needed to obtain and present access tokens for that resource.

In deployments where clients interact with multiple APIs, protected resource metadata can reduce manual configuration by allowing clients to look up resource-specific authorization details.

## Publication and status

RFC 9728 was published in **April 2025** as a **Proposed Standard** on the IETF stream.

## Relevance to agent ecosystems

Agentic systems often integrate many third-party APIs and may need to dynamically determine how to authorize requests to a particular resource. Standardized protected resource metadata can support:

- **Runtime discovery** of which authorization server applies to a given API.
- **Reduced configuration drift** when resource authorization requirements change.
- **Interoperable gateway patterns**, where an agent gateway or broker mediates access to multiple protected resources.

## References

- RFC Editor: [RFC 9728 — OAuth 2.0 Protected Resource Metadata](https://www.rfc-editor.org/info/rfc9728)
- IETF Datatracker: [RFC 9728](https://datatracker.ietf.org/doc/rfc9728/)
