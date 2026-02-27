# Multiple OpenClaw Gateways (same host)

Running multiple **OpenClaw Gateways** on the same machine can be useful for isolation (for example, a “rescue” bot kept separate from the primary assistant) or for redundancy. The OpenClaw documentation recommends a single Gateway for most setups, because one Gateway can manage multiple messaging connections and agents, but describes a supported approach for multi-Gateway deployments when needed.

## Overview

A multi-Gateway setup typically means:

- each Gateway runs as a separate process (often installed as a separate service);
- each Gateway has its own configuration and state directories; and
- each Gateway listens on a distinct base port so that any derived ports (for browser control and related services) do not collide.

When these resources are not isolated, concurrent Gateways can interfere with each other through configuration races, shared caches, or port conflicts.

## Isolation requirements

The OpenClaw documentation lists an isolation checklist for running multiple Gateways on the same host. Each instance should have its own:

- configuration path (for example, via `OPENCLAW_CONFIG_PATH`);
- state directory (for example, via `OPENCLAW_STATE_DIR`, which contains sessions, credentials, and caches);
- workspace root (for example, `agents.defaults.workspace` in configuration); and
- base Gateway port (for example, `gateway.port` or `--port`).

In addition, any ports derived from the base port (such as browser control and Chrome DevTools Protocol (CDP) port ranges) must not overlap between instances.

## Profiles

OpenClaw supports the concept of profiles, which scope per-instance configuration and state and can also suffix service names. The documentation presents profiles as the recommended approach for running multiple Gateways on the same host.

## Ports and derived services

OpenClaw’s documentation describes a base port (the Gateway port) and derived ports used by related services. In multi-Gateway setups, the base ports must be separated enough to avoid collisions in derived port ranges.

## Use case: rescue bot

A common multi-Gateway pattern is a “rescue bot”: a second, isolated Gateway that can still run and provide control access if the primary Gateway is misconfigured or down. The documentation recommends keeping this rescue instance isolated by profile/config, state directory, workspace, and base port.

## See also

- [OpenClaw Gateway](OpenClaw%20Gateway.md)
- [OpenClaw](OpenClaw.md)

## References

- OpenClaw documentation: “Multiple Gateways (same host)”. https://docs.openclaw.ai/gateway/multiple-gateways
