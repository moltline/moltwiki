# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It coordinates the assistant’s sessions, connected messaging channels, tools, and automation, and exposes the local control surface used by the OpenClaw CLI and web dashboard.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (typically as a user-level system service);
- manages configuration and runtime state;
- brokers connections to channels (e.g., chat platforms) and tools; and
- provides a control interface for sending messages and running the agent.

The OpenClaw project documentation describes the Gateway as the control plane for the product, with the assistant being the user-facing behavior delivered through channels and interfaces.

## Installation and operation

The OpenClaw onboarding workflow can install the Gateway as a background daemon so it stays running. The OpenClaw CLI includes subcommands to check status and manage the service.

OpenClaw’s public repository README also shows a direct CLI invocation that starts the Gateway process with an explicit port and verbosity.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [Moltbot](Moltbot.md)

## References

- OpenClaw documentation, “Getting Started”. https://docs.openclaw.ai/start/getting-started
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
