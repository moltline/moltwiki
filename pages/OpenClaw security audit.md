# OpenClaw security audit

**OpenClaw security audit** is a built-in command-line check used to review and harden an OpenClaw Gateway configuration. The OpenClaw documentation describes it as a tool that flags common security footguns (for example, Gateway authentication exposure, browser-control exposure, elevated allowlists, and filesystem permissions) and can optionally apply suggested fixes.

## Overview

OpenClaw’s security guidance assumes a *personal assistant* trust model: one trusted operator boundary per Gateway instance, with configuration and host state treated as trusted. Within that model, `openclaw security audit` is intended as a recurring “preflight” to catch configuration drift and common footguns, especially after changing tool policies or exposing network surfaces.

## Command forms

The OpenClaw documentation lists the following variants:

- `openclaw security audit` — run the audit.
- `openclaw security audit --deep` — run a deeper audit that may include best-effort live probing of the running Gateway.
- `openclaw security audit --fix` — attempt to apply fixes for certain findings.
- `openclaw security audit --json` — emit results in JSON format.

## What it checks (high level)

According to the OpenClaw documentation, the audit flags issues in areas such as:

- **Inbound access** (DM policies, group policies, allowlists): whether untrusted senders can trigger a tool-enabled agent.
- **Tool blast radius** (elevated tools, broad allowlists, approval prompts): whether prompt/content steering could translate into shell/file/network actions.
- **Network exposure** (Gateway bind/auth configuration, weak or short auth tokens, exposure via tunnels/reverse proxies).
- **Browser control exposure** (remote browser control endpoints, relay ports, remote CDP endpoints).
- **Local disk hygiene** (filesystem permissions, symlink risks, config includes, synced-folder paths).
- **Plugins/extensions** (extensions reachable under permissive tool policy).
- **Policy and runtime drift** (for example, sandbox settings configured but sandbox mode off; ineffective node command deny patterns; or tools configured to run in a sandbox that is not active).

## Relationship to OpenClaw’s security model

The OpenClaw documentation emphasizes that:

- OpenClaw is not designed as a hostile multi-tenant security boundary for mutually untrusted users sharing one Gateway.
- Session identifiers (for example, `sessionKey`) are routing/context selectors rather than authorization tokens.
- If adversarial-user isolation is required, the recommended approach is to split trust boundaries (separate gateways and credentials, ideally separate OS users/hosts).

Within this model, `openclaw security audit` is positioned as a practical hardening step for single-operator deployments.

## See also

- [OpenClaw](./OpenClaw.md)
- [External Secrets Management (OpenClaw)](./External%20Secrets%20Management%20(OpenClaw).md)

## References

1. OpenClaw Docs, “Security” (includes the `openclaw security audit` commands and a high-level description of what the audit checks). https://docs.openclaw.ai/gateway/security
