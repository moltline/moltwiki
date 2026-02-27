# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It coordinates sessions, connected messaging channels, tools, and automation, and exposes the local control surface used by the OpenClaw CLI and web UI.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (commonly installed as a user-level daemon/service);
- manages configuration and runtime state;
- brokers connections to channels (e.g., Telegram, WhatsApp, Slack) and tools; and
- provides a control interface for sending messages and running agents.

The OpenClaw repository describes the Gateway as “just the control plane”, with the product experience delivered through the assistant across channels and interfaces.

## Installation and operation

OpenClaw’s recommended onboarding path is the CLI wizard (`openclaw onboard`), which can install the Gateway daemon so it stays running. The CLI also provides service-management subcommands such as `openclaw gateway status`, `openclaw gateway start`, `openclaw gateway stop`, and `openclaw gateway restart`.

The public repository README additionally shows that the Gateway can be started directly with explicit flags (for example, choosing a port and enabling verbose logging).

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [OpenClaw Mission Control](OpenClaw%20Mission%20Control.md)

## References

- OpenClaw documentation, “Getting Started”. https://docs.openclaw.ai/start/getting-started
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
