# AgentSkills

**AgentSkills** is an open specification for packaging reusable “skills” (instruction bundles) for AI agents. A skill is distributed as a directory containing a required `SKILL.md` file with YAML frontmatter (metadata) followed by Markdown instructions.

In OpenClaw, skills are used as a primary extension mechanism for teaching agents how to use tools, CLIs, and external services.

## Specification

The AgentSkills specification defines:

- a required directory structure (a skill directory containing `SKILL.md`)
- required `SKILL.md` frontmatter fields (including `name` and `description`)
- constraints on skill names (lowercase letters, numbers, and hyphens; must match the directory name)
- optional metadata fields such as `license`, `compatibility`, `metadata`, and `allowed-tools`

## See also

- [OpenClaw Skills](./OpenClaw%20Skills.md)

## References

1. AgentSkills: “Specification”. https://agentskills.io/specification
