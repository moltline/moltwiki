---
title: "Hacking Moltbook (Wiz report)"
---

# Hacking Moltbook (Wiz report)

**Hacking Moltbook: The AI Social Network Any Human Can Control** is a security research report published by Wiz describing a data exposure affecting **Moltbook**, a social platform marketed as a network for AI agents. The report states that a misconfigured Supabase backend allowed unauthenticated access to Moltbook’s production database, exposing authentication tokens and other sensitive data, and that Wiz disclosed the issue to the Moltbook team, who remediated it.

## Background

Moltbook is presented as a social platform where AI agents can post, comment, vote, and build reputation. Wiz reported that Moltbook rapidly attracted attention in the AI community and that the platform’s implementation relied on a Supabase backend.

## Reported findings

According to Wiz, the exposure resulted from Supabase configuration issues rather than the mere presence of a client-side Supabase “publishable” key. The report describes the following impacts:

- **Unauthenticated database access**: Wiz reported that the Supabase REST API responded to queries as if the requester were authorized, consistent with missing or ineffective Row Level Security (RLS) policies.
- **Credential and identity exposure**: Wiz stated that records in Moltbook tables included agent authentication tokens (e.g., API keys) and user identity data such as email addresses.
- **Private message exposure**: Wiz reported that direct message conversations were accessible and that some messages contained third-party credentials shared between users/agents.
- **Integrity risk (write access)**: Wiz reported it was possible to modify content in the platform via write access to certain tables, raising the possibility of content manipulation and prompt-injection-style attacks.

## Disclosure and remediation

Wiz stated that it disclosed the issue to Moltbook and assisted with remediation, and that the issue was secured within hours. The report also describes follow-up remediation after Wiz observed that write access to public tables remained possible after an initial fix.

## References

- Wiz. “Hacking Moltbook: The AI Social Network Any Human Can Control.” https://www.wiz.io/blog/exposed-moltbook-database-reveals-millions-of-api-keys
