---
title: "OAuth 2.0 Protected Resource Metadata (RFC 9728)"
---

**OAuth 2.0 Protected Resource Metadata** is an IETF standard (published as **RFC 9728**) that defines a machine-readable metadata format for **OAuth-protected resources** (for example, APIs) to advertise information that clients and authorization servers need in order to interact with them.

The specification is intended to complement existing OAuth discovery mechanisms (such as **Authorization Server Metadata**, RFC 8414) by providing a standardized way for a resource server to publish metadata about itself and its authorization requirements.

## Description

In OAuth deployments, a client often needs to learn details about a protected resource before it can request appropriate access tokens and make authorized requests. RFC 9728 defines:

- a **metadata document format** for protected resources, and
- **discovery mechanisms** (well-known URIs and `WWW-Authenticate` header parameters) so clients can locate that metadata.

A key piece of information in this metadata is the set of **authorization servers** that can issue access tokens accepted by the protected resource.

## Discovery

RFC 9728 describes how a client can discover a protected resource’s metadata document.

### `WWW-Authenticate` header

When a request is unauthorized, a resource server can return an HTTP authentication challenge that includes a pointer to its metadata document using the `resource_metadata` parameter.

### Well-known URIs

Protected resource metadata may also be hosted at standardized **well-known** locations under `/.well-known/`, enabling clients to construct candidate URLs and fetch the metadata.

## Relationship to agent ecosystems

Agentic systems that rely on HTTP APIs commonly need **automated, interoperable authorization discovery** so that software agents can determine:

- which authorization server(s) to use for a given API,
- which scopes or permissions may be required, and
- where to find related OAuth endpoints and capabilities.

For example, the **Model Context Protocol (MCP)** authorization specification requires MCP servers to implement **Protected Resource Metadata** to advertise associated authorization servers, enabling MCP clients to discover how to obtain tokens for protected MCP endpoints.

## See also

- OAuth 2.0 Authorization Server Metadata (RFC 8414)
- OAuth 2.0 Bearer Token Usage (RFC 6750)
- Model Context Protocol (MCP) authorization specification

## References

- IETF RFC 9728: *OAuth 2.0 Protected Resource Metadata*. https://datatracker.ietf.org/doc/html/rfc9728
- RFC Editor info page for RFC 9728. https://www.rfc-editor.org/info/rfc9728
- WorkOS blog: “Introducing RFC 9728: Say hello to standardized OAuth 2.0 resource metadata”. https://workos.com/blog/introducing-rfc-9728-say-hello-to-standardized-oauth-2-0-resource-metadata
- Model Context Protocol specification, “Authorization” (references RFC 9728 for protected resource metadata). https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
