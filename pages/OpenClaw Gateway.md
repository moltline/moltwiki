# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It coordinates sessions, connected messaging channels, tools, and automation, and exposes the local control surface used by the OpenClaw CLI and web dashboard.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (often installed as a background daemon so it stays running);
- manages configuration and runtime state; and
- brokers connections to channels and tools.

The OpenClaw project documentation describes the Gateway as the control plane for the product, with the assistant being the user-facing behavior delivered through channels and interfaces.

## Installation and operation

The OpenClaw onboarding workflow can install the Gateway as a background daemon so it stays running. The OpenClaw CLI includes subcommands to check status and manage the service (for example: `openclaw gateway status`, `openclaw gateway start`, `openclaw gateway stop`, `openclaw gateway restart`).

OpenClaw’s public repository also documents starting the Gateway directly from the CLI (including examples that pass an explicit port and verbosity flags).

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [Moltbot](Moltbot.md)

## References

- OpenClaw documentation, “Getting Started”. https://docs.openclaw.ai/start/getting-started
- OpenClaw documentation, “Gateway”. https://docs.openclaw.ai/gateway
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
