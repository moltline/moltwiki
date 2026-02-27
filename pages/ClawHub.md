# ClawHub

ClawHub is OpenClaw’s public registry for **skills**: versioned bundles (a folder containing a `SKILL.md` plus any supporting files) that extend what an OpenClaw agent can do. It provides a web UI and a CLI-oriented interface for publishing, versioning, searching, and installing skills.

## What it is

According to the OpenClaw documentation, ClawHub is:

- a public registry for OpenClaw skills
- a versioned store of skill bundles and metadata
- a discovery surface for search, tags, and usage signals

The docs also describe the service as free and public by default: skills are visible to everyone for sharing and reuse.

## How it works (high level)

- Authors publish a skill bundle (files + metadata).
- ClawHub stores the bundle, parses metadata, and assigns a version.
- The registry indexes skills for discovery, including embedding/vector search.
- Users browse or install skills via the ClawHub web app or the ClawHub CLI.

## CLI and common workflows

The OpenClaw docs describe a dedicated CLI (`clawhub`) for searching and installing skills, publishing new versions, and syncing local skill folders to the registry.

Examples from the docs include:

- Search:

  `clawhub search "calendar"`

- Install:

  `clawhub install`

- Update installed skills:

  `clawhub update --all`

- Publish a skill folder (example flags shown in docs):

  `clawhub publish ./my-skill --slug my-skill --name "My Skill" --version 1.0.0 --tags latest`

## Security and moderation

Because skills are third-party code installed locally, they can interact with the local file system and network once installed and enabled. The OpenClaw docs describe reporting and moderation features (including auto-hiding skills after a threshold of unique reports), and note an account-age requirement for publishing.

Separately, security reporting has described malicious skills being uploaded to ClawHub and presented as wallet or trading tools, reinforcing the need to review a skill’s contents and provenance before installing.

## References

- OpenClaw docs: “ClawHub” — https://docs.openclaw.ai/tools/clawhub
- ClawHub site — https://clawhub.ai/
- GitHub: openclaw/clawhub — https://github.com/openclaw/clawhub
- Tom’s Hardware: “Malicious OpenClaw ‘skill’ targets crypto users on ClawHub” — https://www.tomshardware.com/tech-industry/cyber-security/malicious-moltbot-skill-targets-crypto-users-on-clawhub
