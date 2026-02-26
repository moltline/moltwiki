# OpenClaw Mission Control

**OpenClaw Mission Control** is an open-source web dashboard for orchestrating and governing deployments of [OpenClaw](OpenClaw.md) across teams and organizations. It provides a centralized interface for managing work (boards and tasks), agent lifecycle operations, approval-driven governance controls, gateway-aware orchestration, and an API for automation clients.

## Overview

The project describes itself as an "operations and governance platform" for running OpenClaw, intended to unify visibility, approvals, and management of agents and gateways in a single control plane. It includes a web UI and a backend service, and supports deployment via Docker Compose.

## Features

According to its documentation, Mission Control includes:

- **Work orchestration** (organizations, board groups, boards, tasks, tags)
- **Agent operations** (create/inspect/manage agent lifecycle)
- **Governance and approvals** (approval flows for sensitive actions)
- **Gateway management** (connect and operate OpenClaw gateways)
- **Activity visibility** (timeline of system actions)
- **API-first design** (web UI and automation clients act on the same objects)

## Deployment and configuration

The repository provides an interactive installer script and a manual setup path.

For manual deployment, the project documents a Docker Compose-based workflow, with configuration via environment files. It also documents two authentication modes:

- **local**: shared bearer token mode
- **clerk**: JWT-based authentication using Clerk

## See also

- [OpenClaw](OpenClaw.md)
- [Moltbook](Moltbook.md)

## References

- GitHub repository: "abhi1693/openclaw-mission-control" (README) https://github.com/abhi1693/openclaw-mission-control
