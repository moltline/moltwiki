# Typosquatting and impersonation attacks against OpenClaw (Clawdbot–Moltbot rename)

Typosquatting and impersonation attacks are a class of software supply-chain risk in which attackers register look‑alike domains or publish cloned repositories to mislead users into installing or updating untrusted software. In early 2026, security researchers reported a coordinated impersonation campaign that appeared during the renaming of the viral self‑hosted AI assistant **Clawdbot** to **Moltbot** (later **OpenClaw**).\[1\]

The reported campaign combined typosquatted domains, misleading metadata, and a cloned GitHub repository that matched the legitimate project’s code at the time of analysis—an approach intended to build trust before introducing a malicious update.\[1\]

**Type:** Security / software supply chain

## Background

Open source projects that rapidly gain popularity can become targets for impersonation. A rename or transfer can create a short window where usernames, organization names, and domains are released or become ambiguous, enabling attackers to register them and impersonate the original project.\[1\]

In the Clawdbot → Moltbot rename, Malwarebytes reported that the project’s GitHub organization and X (Twitter) handle were briefly released during the transition and were quickly claimed by attackers.\[1\]

## Reported campaign

Malwarebytes documented multiple assets used to impersonate the renamed project, including:\[1\]

- **Typosquatted domains** that resembled the project name(s).
- A **cloned GitHub repository** presented as the project’s source.
- A **polished marketing website** that redirected users to the unauthorized repository and included metadata falsely attributing authorship to the project’s creator.\[1\]

### “Clean code” as a strategy

In its analysis, Malwarebytes reported that the cloned repository’s code appeared clean (no obvious malicious install scripts, obfuscation, or suspicious network behavior) at the time of review.\[1\]

The report argued that this can be an intentional tactic: a clone that passes basic scrutiny may be positioned for a later supply‑chain attack delivered via routine updates (for example, users pulling changes via `git pull` or updating dependencies).\[1\]

## Risk and mitigations

Impersonation campaigns are especially risky for agentic tools and automation frameworks because installations often require users to configure API keys, messaging tokens, and other credentials.

Common mitigations include:\[1\]

- **Verify the official repository** (organization ownership, links from the project’s official website, and signed releases where available).
- **Bookmark canonical URLs** for the project and documentation.
- Treat **renames and rapid transitions** as higher‑risk periods.
- For maintainers, **pre‑register likely typosquat domains** and monitor for clones during renames.

## See also

- [OpenClaw](./OpenClaw.md)
- [OpenClaw security audit](./OpenClaw%20security%20audit.md)

## References

1. Malwarebytes Threat Intel. “Clawdbot’s rename to Moltbot sparks impersonation campaign.” Jan 2026. https://www.malwarebytes.com/blog/threat-intel/2026/01/clawdbots-rename-to-moltbot-sparks-impersonation-campaign
