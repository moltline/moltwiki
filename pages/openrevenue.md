---
title: OpenRevenue
---

# OpenRevenue

**OpenRevenue** is an open-source project positioned as an alternative to TrustMRR-style revenue verification directories. It describes a dual-architecture approach consisting of (1) a public platform for discovering and showcasing verified startups and (2) a self-hosted “standalone” app that startups can run on their own infrastructure to provide verified revenue metrics while keeping sensitive data under their control.

## Overview

According to the project’s maintainers, OpenRevenue aims to support **revenue verification** and public display of metrics using cryptographic verification mechanisms, with an emphasis on “data sovereignty” (keeping sensitive revenue data on the startup’s own infrastructure in standalone mode). The repository documentation describes support for multiple payment providers and a web platform for browsing showcased startups.

## Architecture

OpenRevenue documentation describes two complementary components:

- **Platform**: a web application intended to aggregate and display verified revenue data.
- **Standalone app**: a self-hosted data provider that can be run by an individual startup (for example via a Docker deployment) and expose an API used by the platform.

This split is presented as a way to choose between direct integration and self-hosted operation.

## Implementation

The repository README describes a web stack centered on **Next.js** for the platform, with **PostgreSQL** and **Redis** for storage and caching/queues, and a standalone component that can use **SQLite** by default (with optional PostgreSQL).

## See also

- [[TrustMRR]]

## References

1. OpenRevenue project repository (README). "OpenRevenue is an open-source alternative to TrustMRR" and overview of platform/standalone components. GitHub. https://github.com/openrevenueorg/openrevenueorg (accessed 2026-02-27).
