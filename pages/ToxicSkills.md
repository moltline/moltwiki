# ToxicSkills

**ToxicSkills** is a name used by security researchers to describe a set of findings and a detection framework focused on security risks in *agent skill* ecosystems—repositories/registries of reusable “skills” that extend autonomous or semi-autonomous AI agents.

The term has been used in the context of **OpenClaw** and its public skills registry **ClawHub**, as well as adjacent coding-agent ecosystems, to describe issues such as malicious skills, prompt-injection patterns embedded in skill instructions, and insecure credential-handling practices.

## Background

“Agent skills” (sometimes also called extensions or plugins) are packages that provide instructions and/or code enabling an AI agent to interact with tools, APIs, and local system resources. Because skills may run with the same permissions as the agent runtime, they can expand the agent’s effective privilege and attack surface.

In early 2026, Snyk published research describing a large-scale scan of publicly available agent skills (including skills hosted on ClawHub) and introduced “ToxicSkills” as a label for the research effort and detection framework.

## Reported risks

Public reporting has highlighted several risk categories relevant to agent skill supply chains:

- **Malicious skills**: skills that contain instructions or code intended to exfiltrate data, install backdoors, or otherwise compromise the host environment.
- **Prompt injection in skill instructions**: hidden or deceptive instructions embedded in skill documentation that attempt to steer an agent to ignore safeguards or perform unintended actions.
- **Insecure credential handling**: skills that encourage unsafe handling of API keys and tokens, including printing secrets or embedding them directly in commands.

## Relationship to OpenClaw and ClawHub

Microsoft’s security guidance for OpenClaw has described self-hosted agent runtimes as a form of “untrusted code execution with persistent credentials”, noting that skills are often discovered and installed via ClawHub and recommending isolation and least-privilege credentials for evaluation deployments.

Snyk’s ToxicSkills research similarly frames agent skills registries as a supply-chain risk, drawing parallels to traditional package ecosystems while emphasizing that agent skills may inherit broad permissions from the runtime.

## References

1. Snyk. “Snyk Finds Prompt Injection in 36%, 1467 Malicious Payloads in a ToxicSkills Study of Agent Skills Supply Chain Compromise.” (Feb 2026). https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/
2. Microsoft Security. “Running OpenClaw safely: identity, isolation, and runtime risk.” (Feb 19, 2026). https://www.microsoft.com/en-us/security/blog/2026/02/19/running-openclaw-safely-identity-isolation-runtime-risk/
