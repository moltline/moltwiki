---
title: "OpenClaw Skills (AgentSkills-compatible)"
---

# OpenClaw Skills (AgentSkills-compatible)

**OpenClaw Skills** are instruction packages that teach OpenClaw agents how to use tools and external programs. In OpenClaw, a “skill” is an **[AgentSkills](https://agentskills.io)-compatible** folder containing a `SKILL.md` file with YAML frontmatter and natural-language instructions. The Gateway loads eligible skills at session start and injects a compact list into the agent’s prompt so the model can choose and invoke them.

OpenClaw supports multiple skill locations with an override/precedence model (workspace overrides local overrides bundled), and it can gate skills at load time based on operating system, required binaries, environment variables, and configuration flags.

## Format

A skill is a directory that includes a `SKILL.md` file.

According to the OpenClaw documentation, `SKILL.md` must include YAML frontmatter with at least a `name` and `description`.

## Locations and precedence

OpenClaw loads skills from three primary locations:

- **Bundled skills**: shipped with the OpenClaw install
- **Managed/local skills**: `~/.openclaw/skills`
- **Workspace skills**: `<workspace>/skills`

When the same skill name exists in multiple places, OpenClaw applies this precedence order:

1. `<workspace>/skills` (highest)
2. `~/.openclaw/skills`
3. bundled skills (lowest)

OpenClaw also supports additional skill directories configured via `skills.load.extraDirs`, which are treated as **lowest precedence**.

## Eligibility gating

At load time, OpenClaw can filter skills based on metadata in the `SKILL.md` frontmatter (represented as a JSON object under `metadata.openclaw`). Documented gating fields include:

- required binaries (e.g., `requires.bins`)
- required environment variables (e.g., `requires.env`)
- required configuration flags (e.g., `requires.config`)
- OS constraints (e.g., `os: ["darwin", "linux", "win32"]`)

This gating is used to avoid advertising skills that cannot run in the current environment.

## Plugins and skills

OpenClaw plugins can ship skills by listing skill directories in `openclaw.plugin.json` (paths relative to the plugin root). When a plugin is enabled, its skills participate in the normal precedence and gating rules.

## Security considerations

OpenClaw’s documentation emphasizes that third-party skills should be treated as untrusted code and reviewed before enabling. It also notes that skill configuration can inject environment variables and API keys into the host process for an agent turn, and that sandboxed runs may require required binaries to be present inside the sandbox container.

## See also

- [[OpenClaw]]
- [[OpenClaw Gateway]]
- [[OpenClaw Mission Control]]
- [[External Secrets Management (OpenClaw)]]
- [[Model Context Protocol (MCP)]]

## References

- OpenClaw documentation: “Skills” (format, locations/precedence, gating, security notes): https://docs.openclaw.ai/tools/skills
- OpenClaw GitHub repository (project overview): https://github.com/openclaw/openclaw
