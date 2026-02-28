---
title: "RFC 9207 (OAuth 2.0 Authorization Server Issuer Identification)"
description: "Defines the OAuth 2.0 'iss' authorization response parameter to prevent mix-up attacks in multi-issuer clients."
---

# RFC 9207 (OAuth 2.0 Authorization Server Issuer Identification)

## Summary

[RFC 9207](https://www.rfc-editor.org/rfc/rfc9207) specifies an OAuth 2.0 extension that adds an `iss` parameter to the **authorization response** (including error responses). The `iss` value identifies the authorization server (AS) that produced the response, enabling clients that talk to **multiple authorization servers** to defend against **mix-up attacks**.

## What problem it solves (mix-up attacks)

In the OAuth 2.0 authorization code flow, the authorization response is typically delivered to the client via the resource owner’s user agent (browser redirect). In base OAuth 2.0, that redirect response does not include an explicit identifier for which authorization server issued it.

For clients integrated with multiple authorization servers, this ambiguity enables *mix-up attacks*, where an attacker can trick the client into sending an authorization code or token to the wrong party.

RFC 9207’s `iss` parameter gives the client a reliable way to confirm the issuer of the response before proceeding.

## The `iss` response parameter

### Authorization server requirements

An authorization server that supports RFC 9207:

- **MUST** include `iss` in authorization responses to the client, including error responses. The `iss` value is the AS **issuer identifier** as defined by OAuth Authorization Server Metadata (RFC 8414). It **MUST** be an `https` URL with no query or fragment components. \[[RFC 9207](https://www.rfc-editor.org/rfc/rfc9207)]
- If it publishes metadata per RFC 8414, it **MUST**:
  - Ensure its metadata `issuer` value is identical to the `iss` response parameter value.
  - Advertise support by setting `authorization_response_iss_parameter_supported` to `true`. \[[RFC 9207](https://www.rfc-editor.org/rfc/rfc9207)]

### Client validation

A client that supports RFC 9207:

- Extracts `iss` from the authorization response (when present), URL-decodes it, and compares it to the expected issuer identifier for the authorization server it initiated the request against.
- If the value does not match, the client **MUST** reject the authorization response and **MUST NOT** proceed. \[[RFC 9207](https://www.rfc-editor.org/rfc/rfc9207)]

## Relationship to the broader OAuth security ecosystem

- **RFC 8414 (OAuth 2.0 Authorization Server Metadata)** defines the issuer identifier concept used by RFC 9207.
- **OAuth 2.0 Security Best Current Practice** discusses mix-up attacks and related mitigations; RFC 9207 standardizes an interoperable countermeasure.
- Profiles like **OpenID FAPI 2.0 Security Profile** reference RFC 9207 as part of hardened OAuth deployments.

## Practical notes

- RFC 9207 is most relevant for clients that support **multiple issuers** (e.g., “Sign in with X” across multiple identity providers, multi-tenant enterprise SSO, or aggregator clients).
- For single-issuer clients, mix-up attacks are not applicable; however, adding a second issuer later can introduce the risk.

## References

- RFC 9207: OAuth 2.0 Authorization Server Issuer Identification — https://www.rfc-editor.org/rfc/rfc9207
- RFC 8414: OAuth 2.0 Authorization Server Metadata — https://www.rfc-editor.org/rfc/rfc8414
- OpenID FAPI 2.0 Security Profile (draft): https://openid.net/specs/fapi-2_0-security-02.html
