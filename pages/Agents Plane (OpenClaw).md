# Agents Plane (OpenClaw)

An **Agents Plane** is a proposed OpenClaw platform feature intended to support **multi-tenant provisioning and isolation** of many OpenClaw agents for organizations (for example, “OpenClaw for Teams”). The proposal emphasizes per-agent isolation boundaries (compute, identity, secrets, and network policy) and administrative fleet management workflows.

## Overview

The Agents Plane proposal describes an infrastructure layer that would allow an administrator to provision OpenClaw agents for multiple team members with standardized, repeatable setup. The design goal is to reduce the operational burden of deploying many agents while improving isolation compared to running multiple agents on shared hosts.

## Goals

The proposal lists organizational needs such as:

- One-command provisioning of an agent for a team member.
- Isolation between agents (no shared secrets and restricted network access).
- Administrative oversight without requiring administrators to access individual agent secrets.
- Per-agent cost visibility and operational management.

## Proposed per-agent resources

The issue proposes that each agent would be provisioned with dedicated resources and configuration, including:

- **Compute**: a VM (or container) running OpenClaw.
- **Identity**: a dedicated cloud service account with minimal permissions.
- **Secrets**: per-agent secrets scoped via a secrets manager and IAM bindings.
- **Network**: isolation via subnet/firewall rules (or equivalent policy controls).
- **Access**: owner-scoped administrative access (for example, via an identity-aware proxy model).
- **Channels**: agent-specific messaging channel connections.

## Deployment models

The proposal compares multiple deployment models for running many agents:

- **VM-per-agent**, described as offering the strongest isolation.
- **Containers on Kubernetes**, described as providing “good” isolation with additional operational complexity.
- **Multiple processes on a shared VM**, described as weak isolation and suitable mainly for development/testing.

## Security model

The proposal frames the Agents Plane as a “zero trust between agents” approach, including:

- Per-agent compute and secret scoping to prevent cross-agent access.
- Network policy controls intended to prevent agents from reaching each other’s services.
- Separation of duties where administrators can manage fleet operations (metrics/logs) without access to secret values.

## Status

As of the referenced issue, Agents Plane is described as a feature proposal (not a finalized specification).

## References

- OpenClaw GitHub issue: [feat: Agents Plane — multi-tenant agent provisioning and isolation #17299](https://github.com/openclaw/openclaw/issues/17299)
