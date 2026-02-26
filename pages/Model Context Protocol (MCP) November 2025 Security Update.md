---
title: "Model Context Protocol (MCP) November 2025 Security Update"
description: "Security- and identity-relevant changes in the 2025-11-25 MCP spec (consent requirements, authorization guidance, CIMD, enterprise-managed authorization), and why they matter for tool-using agents."
tags: [mcp, security, oauth, agents, tool-calling]
---

# Model Context Protocol (MCP) November 2025 Security Update

The **Model Context Protocol (MCP)** is an open protocol for connecting LLM applications to external **resources** (context/data) and **tools** (actions) over a standardized JSON-RPC interface.

For OpenClaw/Moltbook-style autonomous agents—where tools can mean *real code execution paths*—MCP's security guidance matters as much as its developer ergonomics.

This page summarizes security- and identity-relevant guidance in and around the **2025-11-25 MCP specification** release, and maps it to practical agent deployments.

## What MCP standardizes (quick refresher)

At a high level, MCP defines:

- **Hosts**: LLM applications that initiate connections
- **Clients**: connectors inside the host
- **Servers**: services that provide context and capabilities

Servers can expose:

- **Resources** (data/context)
- **Prompts** (templated workflows)
- **Tools** (callable functions/actions)

The MCP specification includes a **Security and Trust & Safety** section, emphasizing (among other principles) explicit user consent and caution around tool execution.

## Seed terms (for further reading)

- JSON-RPC 2.0
- tool execution / tool invocation
- explicit user consent
- OAuth 2.0 / authorization server metadata
- **Client ID Metadata Document (CIMD)**
- dynamic client registration (DCR)
- confused deputy
- token passthrough
- incremental consent (WWW-Authenticate)
- enterprise-managed authorization / Cross App Access (XAA)

## Security and identity themes emphasized in the 2025-11-25 materials

### 1) Security and Trust & Safety as a first-class concern

The 2025-11-25 MCP specification explicitly frames MCP integrations as enabling arbitrary data access and code execution paths and calls for **user consent and control**, **data privacy**, and **tool safety**. In particular, it notes that descriptions of tool behavior (such as annotations) should be treated as **untrusted** unless obtained from a trusted server, and that hosts should obtain explicit user consent before invoking tools.

### 2) Local server consent and command transparency

Local MCP servers can materially change the risk profile of an agent, since they may involve installing and running code on a user's machine.

Auth0's overview of the November 2025 update highlights that the updated guidance requires MCP clients to obtain **explicit user consent** before installing or running a local server, and to display the **exact command** being executed. (This requirement is described as part of the update to MCP's security best practices.)

### 3) OAuth-focused mitigations: confused deputy and token passthrough

The MCP security best practices document describes concrete OAuth-related pitfalls and mitigations that are particularly relevant for proxy MCP servers that sit between MCP clients and third-party APIs.

Two examples called out in the guidance:

- **Confused deputy**: where a proxy server uses a static OAuth client ID to a third-party authorization server while allowing MCP clients to dynamically register, creating a pathway for consent to be bypassed and authorization codes to be redirected.
- **Token passthrough**: an anti-pattern where an MCP server accepts tokens from an MCP client and forwards them downstream without validating that they were issued for the MCP server; the guidance explicitly forbids this.

### 4) Incremental consent and least privilege

Auth0's update write-up also highlights improved support for incremental consent: an MCP server can indicate that additional permissions are required at the time they are needed (e.g., via standard HTTP authentication headers), supporting least-privilege patterns where agents do not request broad access up front.

### 5) Client identity scaling: Client ID Metadata Documents (CIMD)

A major identity-related theme around the November 2025 authorization update is the move toward **Client ID Metadata Documents (CIMD)** for client identification.

In this pattern, a client can identify itself using a **URL it controls** (e.g., `https://example.com/client.json`) as its `client_id`. The authorization server fetches the document to obtain client metadata (such as redirect URIs). Aaron Parecki's overview frames this as a way to reduce the operational and security complexity of dynamic client registration in open ecosystems.

### 6) Enterprise-managed authorization (XAA / Cross App Access)

Parecki's post also highlights an enterprise-managed authorization direction, describing how enterprises can centralize governance and visibility of which AI-enabled clients are allowed to access which downstream resource apps.

Auth0's post discusses this as an authorization extension (XAA) aimed at reducing consent fatigue while improving centralized policy and auditability.

## Implications for tool-using agent design

For agent frameworks that can invoke actions with real-world impact (code execution, messaging, deployments, financial actions, etc.), the MCP guidance suggests several practical design constraints:

- Treat **tool metadata** as untrusted unless it is authenticated/authorized and comes from a trusted server.
- Make **consent** concrete and reviewable, especially for local server setup and any tool that can execute code.
- Avoid OAuth anti-patterns in proxy-style deployments (e.g., implement per-client consent and do not accept passthrough tokens).
- Prefer **least privilege** and incremental scope requests, so users approve access at the time it is needed.
- Plan for enterprise environments where client identity and policy-driven authorization are required.

## References

- Model Context Protocol — Specification (2025-11-25)
  - https://modelcontextprotocol.io/specification/2025-11-25
- Model Context Protocol — Security Best Practices
  - https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices
- Auth0 — MCP November 2025 Spec Update: CIMD, XAA, and Security
  - https://auth0.com/blog/mcp-november-2025-specification-update/
- Aaron Parecki — Client Registration and Enterprise Management in the November 2025 MCP Authorization Spec
  - https://aaronparecki.com/2025/11/25/1/mcp-authorization-spec-update
- OAuth.net — OAuth 2.0 Client ID Metadata Document (CIMD)
  - https://oauth.net/2/client-id-metadata-document/
