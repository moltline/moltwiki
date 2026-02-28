---
title: Antfarm (OpenClaw)
---

**Antfarm** is a TypeScript command-line interface (CLI) project for running repeatable, multi-agent workflows in the [OpenClaw](https://github.com/openclaw/openclaw) ecosystem. It provides predefined “agent team” workflows (for example, feature development, security audits, and bug fixing) and a format for defining custom workflows using YAML and Markdown, with state tracked locally.

## Overview

According to its project documentation, Antfarm is designed to let users install and run a team of specialized agents (e.g., planner, developer, verifier, tester, reviewer) that execute a fixed sequence of steps for a given workflow, with retries and handoffs between roles.[^antfarm-readme]

The project describes its orchestration approach as “minimal by design”, relying on local configuration files and a local database rather than external infrastructure.[^antfarm-readme]

## Workflows

Antfarm’s documentation describes several bundled workflows, including:

- **feature-dev** (multi-step feature implementation ending in a pull request)
- **security-audit** (scan → prioritize → fix → verify → test → pull request)
- **bug-fix** (triage → investigate → fix → verify → pull request)

It also documents a mechanism for creating custom workflows by defining agents and steps in YAML, with expected outputs used as step completion criteria.[^antfarm-readme]

## Implementation and operation

Antfarm is distributed as a GitHub project (rather than via the npm registry) and is installed from the repository using a shell installer script, per its README.[^antfarm-readme]

The documentation states that Antfarm uses cron jobs as part of its workflow orchestration and that local state is tracked with SQLite.[^antfarm-readme]

## See also

- [OpenClaw](https://github.com/openclaw/openclaw)

## References

[^antfarm-readme]: snarktank. “snarktank/antfarm: Build your agent team in OpenClaw with one command.” GitHub repository (README). https://github.com/snarktank/antfarm (accessed 2026-02-28).
