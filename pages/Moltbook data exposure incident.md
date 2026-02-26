# Moltbook data exposure incident

The **Moltbook data exposure incident** was a security incident in which a publicly accessible backend configuration allowed unauthenticated access to data associated with **Moltbook**, a social network marketed as being primarily for AI agents.

In early February 2026, security firm **Wiz** reported that Moltbook’s underlying **Supabase** backend lacked effective access controls, enabling read and (initially) write access to production data using a client-exposed API key. Wiz stated that exposed data included large numbers of API authentication tokens, email addresses, and private messages, and that the issue was remediated after disclosure to the Moltbook team.[1]

## Background

Moltbook is a social platform positioned as a forum where AI agents post and interact, using mechanisms such as posts, comments, votes, and reputation/karma.[1] Reuters described Moltbook as a new social network advertised as being exclusively for OpenClaw bots.[2]

## Incident

### Discovery
Wiz reported that it identified a Supabase API key embedded in Moltbook’s client-side JavaScript and that the backend configuration permitted unauthenticated access to production data via Supabase’s APIs.[1]

### Exposed data
Wiz stated that the exposed data included:

- **API authentication tokens** for agents (credentials that could enable account impersonation).[1]
- **Email addresses** associated with human account owners and other signups.[1]
- **Private messages** between agents, which Wiz said in some cases contained third-party credentials such as API keys.[1]

### Remediation
Wiz stated that it disclosed the issue to the Moltbook team, which secured the exposure within hours, and that additional remediation was performed to restrict write access.[1]

## Reporting and impact

Reuters reported on the incident and cited Wiz’s assessment that Moltbook had a “major flaw” that exposed private data on thousands of people.[2] In a separate Reuters report, China’s Ministry of Industry and Information Technology warned that improperly configured deployments of the OpenClaw open-source agent could expose users to cyberattacks and data breaches, and referenced the Moltbook exposure as part of broader scrutiny of agent-related services.[3]

## See also

- [Moltbook](./Moltbook.md)
- [OpenClaw](./OpenClaw.md)

## References

1. Wiz, “Hacking Moltbook: The AI Social Network Any Human Can Control” (Feb 2026). https://www.wiz.io/blog/exposed-moltbook-database-reveals-millions-of-api-keys
2. Reuters, “'Moltbook' social media site for AI agents had big security hole, cyber firm Wiz says” (Feb 2, 2026). https://www.reuters.com/legal/litigation/moltbook-social-media-site-ai-agents-had-big-security-hole-cyber-firm-wiz-says-2026-02-02/
3. Reuters, “China warns of security risks linked to OpenClaw open-source AI agent” (Feb 5, 2026). https://www.reuters.com/world/china/china-warns-security-risks-linked-openclaw-open-source-ai-agent-2026-02-05/
