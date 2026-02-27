---
title: Moltbook Observatory
---

# Moltbook Observatory

The **Moltbook Observatory** is an open-source, passive data collection and analytics project for **Moltbook** (an agent-only social network). It continuously polls the Moltbook API, stores results in a local SQLite database, and can serve a web dashboard + REST API for browsing posts, agents, submolts (communities), trends, and time-series “snapshot” metrics.

A key output of the project is the **Moltbook Observatory Archive**: an incremental export of the observatory’s SQLite database published as **date-partitioned Parquet files** on Hugging Face for easier querying and long-term archival.

## What it collects (high level)

From the project documentation, the Observatory is designed to collect and store (at least):

- **Posts** (title/body, author, submolt, timestamps, vote counts, comment counts, URL)
- **Agent profiles** (names/ids, descriptions, karma, follower/following counts, first-seen / last-active timestamps)
- **Submolts** (community metadata and subscriber counts)
- **Trends / analytics** (e.g., word-frequency trends)
- **Snapshots** (hourly platform-wide metrics for time-series analysis)

## How it works (architecture)

The Observatory runs background polling jobs against the Moltbook API and writes the results into a SQLite database. It can also expose a dashboard and REST endpoints for inspection/export.

Conceptually:

- Moltbook API → scheduled pollers → SQLite database → dashboard + API + exports

## The Moltbook Observatory Archive (dataset)

The **Moltbook Observatory Archive** is a public dataset described as an *incremental export* of the Observatory’s SQLite database, released as **date-partitioned Parquet** files. This format supports efficient browsing and analysis (e.g., with DuckDB, Polars, Spark) without requiring access to the live Moltbook API.

## Why it matters in the OpenClaw/Moltbook ecosystem

- Enables **reproducible research** on agent-to-agent social dynamics, instruction sharing, and safety behaviors.
- Supports **longitudinal analyses** (platform growth, topic drift, network effects) via snapshot/time-series tables.
- Provides a data substrate for studies like the February 2026 arXiv paper analyzing instruction risk and norm enforcement among OpenClaw agents on Moltbook.

## Sources

- Moltbook Observatory repository (overview, polling schedule, stored tables, API/export endpoints): https://github.com/kelkalot/moltbook-observatory
- Moltbook Observatory Archive dataset (incremental SQLite export as date-partitioned Parquet): https://huggingface.co/datasets/SimulaMet/moltbook-observatory-archive
- *OpenClaw Agents on Moltbook: Risky Instruction Sharing and Norm Enforcement in an Agent-Only Social Network* (arXiv, Feb 2026; uses the Observatory Archive): https://arxiv.org/html/2602.02625
