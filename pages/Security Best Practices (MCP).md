---
title: "Security Best Practices (MCP)"
---

# Security Best Practices (MCP)

**Model Context Protocol (MCP)** deployments commonly involve untrusted inputs (model prompts, tool descriptions, server-provided metadata, third-party OAuth endpoints) and privileged actions (tool execution, network access, data retrieval). The MCP documentation includes a dedicated **Security Best Practices** guide that complements the MCP Authorization specification.

This page summarizes the themes and concrete mitigations described in the MCP security guidance, and links to the primary sources.

## Overview

The MCP security guidance is aimed at:

- Developers implementing MCP authorization flows.
- MCP server operators.
- Security professionals evaluating MCP-based systems.

It is intended to be read alongside the MCP Authorization specification and broader OAuth guidance such as **OAuth 2.0 Security Best Current Practice (RFC 9700)**.

## Notable risks and mitigations

### Confused deputy (OAuth proxying)

MCP deployments sometimes include an **MCP proxy server** that fronts a third-party API protected by a third-party authorization server. If the MCP proxy uses a **static OAuth client_id** when talking to the third-party authorization server, but also supports **dynamic client registration** for MCP clients, a user’s prior consent to the static client_id can be abused to skip consent in later flows.

The MCP guidance describes mitigations that include:

- Implementing **per-client consent** at the MCP proxy layer *before* initiating the third-party authorization flow.
- Storing per-client consent decisions securely.
- Validating `redirect_uri` via **exact matching** against the registered value.
- Using strong, server-side state handling and ensuring the state/session used to complete the OAuth callback is not established until after the user approves consent.

### Token passthrough (anti-pattern)

The MCP guidance calls out “token passthrough” as an anti-pattern: accepting a token from an MCP client and forwarding it to a downstream API without enforcing that the token was **issued for the MCP server**.

The guidance states that MCP servers **must not** accept tokens that were not explicitly issued for the MCP server, because passthrough can bypass security controls, weaken auditability, and break trust boundaries between services.

### SSRF via OAuth discovery metadata

MCP clients can be induced to fetch attacker-controlled URLs during OAuth-related discovery (for example, via metadata URLs and endpoints referenced by an MCP server). This can enable **server-side request forgery (SSRF)** against internal services or cloud metadata endpoints.

Mitigations described in the MCP guidance include:

- Requiring **HTTPS** for OAuth-related URLs in production.
- Blocking requests to **private and reserved IP ranges** (including link-local addresses such as `169.254.169.254`).
- Validating redirect targets and considering disabling automatic redirect following.
- Using an **egress proxy** / outbound network policy enforcement for server-side deployments.

### Session hijacking and event injection

The security guidance describes risks where an attacker obtains or injects session identifiers and uses them to impersonate a client or inject malicious events into resumable streams.

Mitigations described include:

- Verifying authorization for inbound requests (i.e., not relying on sessions as authentication).
- Using secure, non-deterministic session identifiers.
- Binding session identifiers to user-specific information.

### Local MCP server compromise

When MCP clients support installing or executing local MCP servers (for example, via one-click configuration flows), the security guidance highlights the risk of arbitrary command execution and data exfiltration if the configuration mechanism is not properly consented and constrained.

## Relationship to other MCP security material

The MCP specification changelog notes updates to the Security Best Practices guidance over time.

## References

- Model Context Protocol docs: *Security Best Practices*. https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices
- Model Context Protocol specification: *Key Changes (2025-11-25)* (mentions security best practices updates). https://modelcontextprotocol.io/specification/2025-11-25/changelog
- IETF: *OAuth 2.0 Security Best Current Practice* (RFC 9700). https://datatracker.ietf.org/doc/html/rfc9700
