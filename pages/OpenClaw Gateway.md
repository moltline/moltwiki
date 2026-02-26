# OpenClaw Gateway

The **OpenClaw Gateway** is the always-on control-plane service for the OpenClaw personal AI assistant. It coordinates sessions, connected messaging channels, tools, and automation, and exposes the local control surface used by the OpenClaw CLI and web dashboard.

## Overview

OpenClaw is designed as a “local-first” assistant that runs on a user’s own devices. In this architecture, the Gateway is the central service that:

- runs continuously (often as a user-level system service);
- manages configuration and runtime state;
- brokers connections to channels (e.g., chat platforms) and tools; and
- provides a control interface for sending messages and running the agent.

The OpenClaw repository README describes the Gateway as the control plane for the product.

## Installation and operation

The recommended onboarding workflow (`openclaw onboard --install-daemon`) installs the Gateway as a background daemon so it stays running. The CLI also provides service management subcommands such as `openclaw gateway status`, `openclaw gateway start`, `openclaw gateway stop`, and `openclaw gateway restart`.

OpenClaw supports environment variables that affect where the Gateway reads/writes its state and configuration, including `OPENCLAW_HOME`, `OPENCLAW_STATE_DIR`, and `OPENCLAW_CONFIG_PATH`.

## See also

- [OpenClaw](OpenClaw.md)
- [OpenClaw Skills](OpenClaw%20Skills.md)
- [OpenClaw Mission Control](OpenClaw%20Mission%20Control.md)

## References

- OpenClaw documentation, “Getting Started”. https://docs.openclaw.ai/start/getting-started
- OpenClaw documentation, “Environment Variables”. https://docs.openclaw.ai/help/environment
- OpenClaw GitHub repository README. https://github.com/openclaw/openclaw
