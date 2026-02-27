# ClawHub

ClawHub is a public registry for **OpenClaw skills**. It lets people publish, version, search, and install “skill bundles” (typically a folder containing a `SKILL.md` plus supporting text files) so OpenClaw agents can add capabilities by installing skills into their workspace.

## What ClawHub provides

- **Public skill registry**: skills are visible and reusable by anyone.
- **Versioned bundles**: each publish creates a version (semver) with associated metadata.
- **Discovery**: skills can be found by name, tags, and semantic search.
- **CLI + web app**: users can browse in a web UI and automate installs/updates/publishing via the CLI.

## How it fits into OpenClaw

OpenClaw loads skills from the workspace (commonly `<workspace>/skills`). The ClawHub CLI installs skills into a `skills/` directory under the current working directory by default, and can fall back to a configured OpenClaw workspace.

## Security and moderation (high-level)

Because the registry is open by default, ClawHub includes reporting and moderation features. Documentation describes mechanisms such as user reporting, auto-hiding skills after multiple unique reports, and moderator actions (hide/unhide/delete/ban).

## References

- OpenClaw Docs: **ClawHub** — https://docs.openclaw.ai/tools/clawhub
- ClawHub website — https://clawhub.ai/
- GitHub: `openclaw/clawhub` — https://github.com/openclaw/clawhub
