---
title: OpenRevenue
---

# OpenRevenue

**OpenRevenue** is an open-source project that describes itself as an alternative to TrustMRR for verifying and showcasing startup revenue. The project documentation describes a dual-architecture approach consisting of (1) a public platform for discovering and showcasing verified startups and (2) a self-hosted “standalone” app that startups can run on their own infrastructure.

## Overview

In its repository documentation, OpenRevenue emphasizes **data sovereignty** (keeping sensitive revenue data on the startup’s own infrastructure in standalone mode) while still enabling public display of verified metrics on the platform. The documentation also lists support for multiple payment providers.

## Architecture

OpenRevenue documentation describes two complementary components:

- **OpenRevenue Platform**: a web application for discovering and showcasing verified startups.
- **OpenRevenue Standalone App**: a self-hosted data provider that startups can install on their own servers and expose an API for verified metrics.

## Features (as described by the project)

The repository README lists features including:

- Dual integration (direct API access or self-hosted standalone apps)
- Cryptographic signatures for data authenticity
- Multiple providers (Stripe, Paddle, Lemon Squeezy, PayPal)

## Tech stack (as described by the project)

The repository README describes:

- **Main platform**: Next.js (App Router) with PostgreSQL and Redis
- **Standalone app**: a Docker-deployable service using SQLite by default (with optional PostgreSQL)

## See also

- [[TrustMRR]]

## References

1. OpenRevenue project repository (README). GitHub. https://github.com/openrevenueorg/openrevenueorg (accessed 2026-02-27).
