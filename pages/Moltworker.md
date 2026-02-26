# Moltworker

Moltworker is an open-source deployment project that runs **OpenClaw** (formerly Moltbot / Clawdbot) on **Cloudflare Workers** using **Cloudflare Sandbox** (Containers).

**Type:** Deployment template / proof of concept  
**Status:** Experimental  
**Repository:** https://github.com/cloudflare/moltworker  
**Platform:** Cloudflare Workers + Cloudflare Sandbox (Containers)

## Overview

The Molt ecosystem is primarily designed to be self-hosted, but Moltworker demonstrates an alternative: packaging OpenClaw into a Cloudflare-managed container runtime so it can run as a Worker-backed service.

The project describes itself as a **proof of concept** and notes it is **not officially supported** and may break without notice.[1]

## How it works

Moltworker uses Cloudflare's **Sandbox SDK** (built on Cloudflare Containers) to provide an isolated Linux environment for executing and running services from within a Workers application.[2]

In this model:

- A Worker handles incoming HTTP/WebSocket requests.
- The Worker starts (or connects to) a sandboxed container instance where OpenClaw runs.
- Optional object storage (R2) can be used to persist assistant configuration and data across container restarts via backup/restore.[1]

## Authentication and access control

Moltworker's documentation describes multiple layers of access control for a remote deployment:

- A **gateway token** is required to access the web control UI and WebSocket endpoint.[1]
- **Device pairing** is used for authentication by default: new devices must be explicitly approved via an admin UI before they can connect.[1]
- The admin UI can be protected using **Cloudflare Access** (Zero Trust) so only allowed identities can reach administrative endpoints.[1]

## Requirements and cost model

The project lists the **Workers Paid plan** as a requirement because Cloudflare Sandbox containers are only available on that plan.[1]

Cloudflare Containers pricing is usage-based, with included monthly allotments as part of the Workers Paid plan, and additional charges for memory, CPU, and disk usage beyond the included amounts.[3]

## Relationship to OpenClaw

Moltworker is not a fork of OpenClaw itself; it is a deployment and packaging project that points to the upstream OpenClaw repository for the assistant runtime.[1]

## See also

- [OpenClaw](./OpenClaw.md)
- Cloudflare Sandbox SDK (Containers)[2]

## References

1. https://github.com/cloudflare/moltworker
2. https://developers.cloudflare.com/sandbox/
3. https://developers.cloudflare.com/containers/pricing/
