# ToxicSkills

**ToxicSkills** is a term used by security researchers to describe malicious and insecure **AI agent skill** packages (and the broader supply-chain risks around them), including skills that embed prompt-injection instructions, exfiltration payloads, or other unsafe behaviors in documentation and setup steps.

The term is notably associated with a 2026 study by Snyk that audited public “agent skills” marketplaces and reported widespread security issues, including confirmed malicious payloads.

## Background

“Agent skills” (also called plugins, tools, or extensions depending on platform) are reusable capability bundles that teach an AI agent how to use external systems (e.g., shells, APIs, filesystems, browsers). Because skills can expand an agent’s permissions and execution surface, they create a software supply-chain problem similar to package registries (e.g., npm, PyPI), but with additional risks from natural-language instructions and prompt injection.

Snyk’s ToxicSkills framing emphasizes that skills may contain:

- **Malicious payloads**, such as credential theft or backdoor installation instructions.
- **Prompt injection**, including hidden or deceptive instructions that attempt to override operator intent or system policies.
- **Insecure-by-design patterns**, such as unsafe credential handling or loading untrusted third-party content at runtime.

## Findings reported by Snyk (2026)

In a February 2026 blog post, Snyk reported results from scanning **3,984** agent skills collected from ClawHub and skills.sh (as of **2026-02-05**). Reported headline metrics included:

- **534 skills (13.4%)** with at least one **critical** security issue.
- **1,467 skills (36.82%)** with at least one security issue at any severity.
- **76 confirmed malicious payloads**, validated via human-in-the-loop review.

Snyk described multiple attack techniques observed in the corpus, including obfuscated exfiltration commands embedded in installation instructions and prompt-injection patterns designed to influence agent behavior.

## Threat model

ToxicSkills-style attacks are typically framed as **supply-chain compromises** that exploit the trust boundary between:

1. A skill marketplace or repository (distribution),
2. The human operator (review and installation), and
3. The agent runtime (execution with delegated permissions).

Commonly discussed risk factors include:

- **High privilege by default**: skills may run with the same access as the agent process.
- **“Markdown-as-installer”**: setup steps in documentation can be copy-pasted (or executed by automation) and may conceal malicious behavior.
- **Indirect prompt injection**: skills that fetch third-party content can relay attacker-controlled text into the agent context.

## Mitigations (high level)

Snyk and other security guidance commonly recommends a combination of:

- **Skill provenance controls** (vetting, pinning, internal mirrors/registries).
- **Least-privilege agent configuration** (scoped credentials, restricted filesystem mounts).
- **Runtime sandboxing** for skill execution.
- **Static and dynamic scanning** of skill bundles and their documentation for suspicious patterns.

## See also

- [ClawHub](./ClawHub.md)
- [OpenClaw Skills](./OpenClaw%20Skills.md)

## References

- Snyk blog: “Snyk Finds Prompt Injection in 36%, 1467 Malicious Payloads in a ToxicSkills Study of Agent Skills Supply Chain Compromise” (Feb 2026) — https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/
- Snyk’s open-source scanning engine referenced in the post: invariantlabs-ai/mcp-scan — https://github.com/invariantlabs-ai/mcp-scan
