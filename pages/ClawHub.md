# ClawHub

ClawHub is OpenClaw’s public registry for **skills**: versioned bundles (a folder containing a `SKILL.md` plus any supporting text files) that extend what an OpenClaw agent can do. It provides a web UI and a CLI-friendly API for publishing, versioning, searching, and installing skills.

## What it is

According to the OpenClaw docs, ClawHub is:

- a public registry for OpenClaw skills
- a versioned store of skill bundles and metadata
- a discovery surface (search, tags, and usage signals)

## How it works (high level)

- Authors publish a skill bundle; ClawHub stores the bundle, parses metadata, and assigns a version.
- The registry indexes skills for discovery (including embedding/vector search).
- Users browse or install skills via the ClawHub web app or CLI.

## Security notes

Because skills are third-party code installed locally, they can interact with the local file system and network once installed and enabled. Security researchers have reported malicious skills being uploaded to ClawHub, highlighting the importance of reviewing skill contents and provenance before installing.

## References

- OpenClaw docs: “ClawHub” — https://docs.openclaw.ai/tools/clawhub
- GitHub: openclaw/clawhub — https://github.com/openclaw/clawhub
- Tom’s Hardware: “Malicious OpenClaw ‘skill’ targets crypto users on ClawHub” — https://www.tomshardware.com/tech-industry/cyber-security/malicious-moltbot-skill-targets-crypto-users-on-clawhub
