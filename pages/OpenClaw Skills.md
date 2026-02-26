# OpenClaw Skills

OpenClaw *skills* are small, AgentSkills-compatible instruction bundles that teach OpenClaw agents how to use tools, CLIs, and external services. In OpenClaw, a skill is typically a directory containing a `SKILL.md` file (with YAML frontmatter) plus any supporting scripts or assets.

Skills are a primary extension mechanism: OpenClaw loads skills from multiple locations (bundled, user-managed, and per-workspace), applies precedence rules when names conflict, and filters skills at load time based on OS, required binaries, environment variables, and configuration.

## Format

OpenClaw skills follow the [AgentSkills](https://agentskills.io) layout: each skill has a `SKILL.md` file that includes at least a `name` and `description` in YAML frontmatter. The `SKILL.md` then contains the natural-language instructions that are injected into the agent prompt when the skill is eligible.

## Locations and precedence

OpenClaw loads skills from three places:

- **Bundled skills** (shipped with the OpenClaw install)
- **Managed/local skills** (typically under `~/.openclaw/skills`)
- **Workspace skills** (under `<workspace>/skills`)

When a skill name exists in multiple places, OpenClaw uses a precedence order: workspace skills override managed/local skills, which override bundled skills.

In multi-agent setups, each agent has its own workspace; workspace skills are therefore per-agent, while managed/local skills are shared on a machine.

## Plugins and skills

OpenClaw plugins can ship skills by listing skill directories in the plugin manifest. When a plugin is enabled, its skills load and participate in the same precedence and filtering rules as other skills.

## Load-time gating and eligibility

OpenClaw filters skills at load time using metadata in `SKILL.md`. Common gates include:

- required binaries on `PATH`
- required environment variables (or env provided via config)
- required OpenClaw configuration flags

This gating is used both to avoid presenting unusable skills to the model and to support platform-specific skills.

## Security considerations

OpenClaw’s documentation treats third-party skills as untrusted code: users are encouraged to review skills before enabling them, and to prefer sandboxed runs for risky tools. OpenClaw can inject per-skill environment variables and API keys for the duration of an agent run, then restore the original environment.

## See also

- [OpenClaw](./OpenClaw.md)

## References
1. OpenClaw Docs: “Skills”. https://docs.openclaw.ai/tools/skills

## External links
- AgentSkills specification: https://agentskills.io
- ClawHub (skills registry): https://clawhub.com
