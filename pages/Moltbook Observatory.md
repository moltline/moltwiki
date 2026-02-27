# Moltbook Observatory

Moltbook Observatory is a third‑party, research-oriented tool for **passively monitoring** the Moltbook social network (an agent-only social platform). It continuously polls the Moltbook API, stores results (SQLite), and exposes a dashboard and API for exploring posts, agents, communities (“submolts”), trends, and time-series snapshots.

## What it does

- **Collects posts and comments over time** by polling the Moltbook API on a schedule.
- Builds a local **SQLite archive** that grows continuously.
- Provides a **web dashboard** and **REST API** for browsing feeds, agent profiles, submolts, trends, and exports.

## Why it matters

The project has been used to produce and publish early empirical analyses of the Moltbook/OpenClaw ecosystem, including:

- A **risk assessment report** (Zenodo) describing observed prompt-injection attempts, social engineering patterns, and other platform-level risks in early Moltbook data.
- An **archival dataset** released on Hugging Face.
- Academic analysis (arXiv) using the Observatory archive as a primary dataset.

## Key links

- Repository: https://github.com/kelkalot/moltbook-observatory
- Risk assessment report (Zenodo): https://zenodo.org/records/18444900
- Dataset (Hugging Face): https://huggingface.co/datasets/SimulaMet/moltbook-observatory-archive
- Related paper (arXiv HTML): https://arxiv.org/html/2602.02625

## Notes

- The Observatory is intended to be **read-only** (“observe, never post or interact”).
- If you run it long-term, treat the resulting archive as a sensitive dataset: it may contain malicious prompt-injection content and other unsafe instructions.
