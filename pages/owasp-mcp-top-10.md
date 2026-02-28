---
title: "OWASP MCP Top 10 (2025)"
description: "A concise map of the OWASP MCP Top 10 risks for Model Context Protocol deployments, with practical relevance for agentic systems."
---

# OWASP MCP Top 10 (2025)

The **OWASP MCP Top 10** is an OWASP project that catalogs security risks specific to **MCP-enabled systems** (Model Context Protocol), especially where agentic workflows connect models to tools, servers, and downstream services.

It’s useful as a shared vocabulary for threat modeling and as a checklist when reviewing:

- MCP servers (local or remote)
- MCP clients/hosts that load tool descriptions into model context
- agent runtimes that chain tools across multiple servers

Source: OWASP project repo (roadmap + overview) and individual risk pages.  
<https://github.com/OWASP/www-project-mcp-top-10>

## The Top 10 categories

From the OWASP MCP Top 10 roadmap/overview:

1. **MCP01: Token Mismanagement & Secret Exposure**
   - Hard-coded credentials, long-lived tokens, secrets leaking via prompts/logs/traces.
2. **MCP02: Privilege Escalation via Scope Creep**
   - Permissions expand over time; weak scope enforcement enables unintended actions.
3. **MCP03: Tool Poisoning**
   - Compromised tools/plugins/outputs inject malicious or misleading context.
4. **MCP04: Software Supply Chain Attacks & Dependency Tampering**
   - Compromised dependencies alter agent behavior or introduce backdoors.
5. **MCP05: Command Injection & Execution**
   - Agents construct/execute commands or code from untrusted input without validation.
6. **MCP06: Prompt Injection via Contextual Payloads**
   - The “interpreter” is the model; injected instructions arrive via retrieved/embedded context.
7. **MCP07: Insufficient Authentication & Authorization**
   - Weak identity verification or access control across servers/tools/agents.
8. **MCP08: Lack of Audit and Telemetry**
   - Missing logs/immutable audit trails for tool calls, context changes, and interactions.
9. **MCP09: Shadow MCP Servers**
   - Unapproved/unsupervised MCP deployments outside governance (“Shadow IT” for MCP).
10. **MCP10: Context Injection & Over-Sharing**
   - Context windows shared/persistent/poorly scoped leak sensitive info across tasks/users/agents.

## Why this matters for agentic + MCP systems

MCP introduces a distinctive security reality: **tool schemas/descriptions become operational context** for the model. That makes governance of:

- tool definitions (integrity, change control)
- authorization boundaries (least privilege, audience restriction)
- and auditing (who did what, via which tool)

as important as traditional API security.

## Practical ways to use the list

- **Threat model by category**: map each MCP server/client feature to one or more MCP0x risks.
- **Review gates**: require explicit sign-off for MCP01/02/07 issues (identity, tokens, scope).
- **Operational checks**: ensure MCP08 is satisfied (structured logs + correlation IDs + retention).
- **Governance**: inventory servers and block unregistered endpoints to reduce MCP09.

## References

- OWASP MCP Top 10 (project overview + roadmap):
  - <https://github.com/OWASP/www-project-mcp-top-10>
- Example individual page (MCP10):
  - <https://owasp.org/www-project-mcp-top-10/2025/MCP10-2025%E2%80%93ContextInjection&OverSharing>
