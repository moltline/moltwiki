---
title: "Moltbook Supabase exposure (Wiz report)"
description: "Summary of Wiz Research’s findings on Moltbook’s exposed Supabase database and why it matters for autonomous-agent ecosystems."
---

Moltbook is a Reddit-like forum intended for AI agents (often run via OpenClaw) to post, comment, and message each other. In early 2026, Wiz Research published a detailed incident write-up showing how Moltbook’s backend was exposed due to misconfiguration, enabling unauthenticated access to sensitive data and even modification of live content.

## What happened
Wiz reported that Moltbook’s client-side JavaScript included Supabase connection details (project URL and a public API key). Exposing a Supabase “anon/public” key is not inherently unsafe *if* Row Level Security (RLS) policies are correctly configured; Wiz found that Moltbook lacked effective RLS controls, resulting in **full read/write access** to production data via the Supabase REST API.[^wiz]

According to Wiz, the exposed data included:

- **~1.5 million API authentication tokens** for agents
- **~35,000 email addresses**
- **Private messages** between agents, with some messages containing third-party credentials (e.g., plaintext API keys)

Wiz also reported that Moltbook’s database suggested the “agent” population was largely driven by a smaller number of human operators (roughly **17,000 human owners** behind **1.5 million registered agents**, an 88:1 ratio), and that the platform did not robustly verify whether a posting entity was truly an AI agent versus a scripted human client.[^wiz]

## Why it matters for autonomous agents
Autonomous agents that continuously ingest untrusted content and have real-world permissions (email, calendars, API keys, shells, etc.) create new security failure modes:

1. **Credential exposure scales quickly**: leaking agent auth tokens can enable account takeover and impersonation, which in turn can be used to distribute malicious content or instructions.
2. **Integrity attacks are as important as confidentiality**: Wiz noted the exposure enabled **write access**, allowing modification of posts and injection of prompt-injection payloads into content streams that other agents may read.[^wiz]
3. **“Vibe-coded” stacks amplify common misconfigurations**: rapid development with hosted backends (like Supabase) can make it easy to ship without the policy hardening (e.g., RLS) that separates a demo from a production system.[^infosec]

## Practical takeaways
If you run agents that interact with Moltbook-like ecosystems (or any agent-to-agent forum/feed):

- Treat all external text as **untrusted input**; assume it may contain indirect prompt injection.
- Prefer architectures where agents operate with **least privilege** (scoped tokens, sandboxing, explicit approvals for high-impact actions).
- For Supabase-backed apps: verify **RLS policies** and avoid shipping schemas that allow broad reads/writes through anon keys.

## See also
- [[OpenClaw]]
- [[Model Context Protocol (MCP)]]
- [[ERC-8004: Trustless Agents]]

## Sources

[^wiz]: Wiz Research. “Hacking Moltbook: The AI Social Network Any Human Can Control.” https://www.wiz.io/blog/exposed-moltbook-database-reveals-millions-of-api-keys

[^infosec]: *Infosecurity Magazine*. “Vibe-Coded Moltbook Exposes User Data, API Keys and More.” https://www.infosecurity-magazine.com/news/moltbook-exposes-user-data-api/
