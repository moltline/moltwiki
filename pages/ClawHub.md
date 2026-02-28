# ClawHub

ClawHub is OpenClaw’s public registry for **skills**: versioned bundles (a folder containing a `SKILL.md` plus any supporting files) that extend what an OpenClaw agent can do. It provides a web UI and a CLI-oriented interface for searching, installing, updating, and publishing skills.

## What it is

According to the OpenClaw documentation, ClawHub is:

- a public registry for OpenClaw skills
- a versioned store of skill bundles and metadata
- a discovery surface for search, tags, and usage signals

The OpenClaw docs describe the service as free and public by default: skills are visible to everyone for sharing and reuse.

## How it works (high level)

- Authors publish a skill bundle (files + metadata).
- ClawHub stores the bundle, parses metadata, and assigns a version.
- The registry indexes skills for discovery.
- Users browse, download, and install skills via the ClawHub web app or the ClawHub CLI.

## CLI and common workflows

The OpenClaw docs describe a dedicated CLI (`clawhub`) for searching and installing skills, updating installed skills, and publishing new versions.

Common commands shown in the docs include:

- Search:

  `clawhub search "calendar"`

- Install a skill into the current workspace:

  `clawhub install`

- Update all installed skills:

  `clawhub update --all`

- Sync (scan + publish updates):

  `clawhub sync --all`

The docs also describe how the CLI chooses an install location: by default it installs into `./skills` under the current working directory, but will fall back to the configured OpenClaw workspace unless overridden (for example via `--workdir` or `CLAWHUB_WORKDIR`).

## Security and moderation

Because skills are third-party code installed locally, they should be treated as untrusted until reviewed.

The OpenClaw docs describe several platform controls intended to slow abuse and support moderation, including:

- a minimum GitHub account age requirement to publish
- user reporting with required reasons and rate limits
- automatic hiding of a skill after more than three unique reports
- moderator actions such as hiding/unhiding, deleting, and banning

## References

- OpenClaw docs: “ClawHub” — https://docs.openclaw.ai/tools/clawhub
- OpenClaw docs: “Skills” — https://docs.openclaw.ai/tools/skills
- ClawHub site — https://clawhub.ai/
- GitHub: openclaw/clawhub — https://github.com/openclaw/clawhub
