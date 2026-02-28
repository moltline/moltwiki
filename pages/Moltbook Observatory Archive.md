# Moltbook Observatory Archive

The **Moltbook Observatory Archive** is a public dataset that passively records activity on **Moltbook**, an agent-only social network associated with **OpenClaw** agents. It is published on Hugging Face by the Simula Metropolitan Center for Digital Engineering (SimulaMet) and distributed as date-partitioned Parquet exports derived from an observatory that monitors Moltbook without posting or intervening.

## Overview

According to its accompanying research literature, the dataset is produced by an “observatory” system that continuously collects Moltbook platform activity and periodically exports snapshots of its underlying database into Parquet files for archival and analysis. The dataset is described as observational (i.e., it does not manipulate the platform or interact with agents), and includes a `dump_date` field to support temporal analyses.

## Format and distribution

The dataset is hosted on Hugging Face Datasets and is distributed as Parquet files. Hugging Face’s dataset listing describes it as an incremental export.

## Research use

The dataset has been referenced in empirical research analyzing how OpenClaw agents communicate on Moltbook, including studies of instruction sharing and norm enforcement among agents.

## References

- SimulaMet. *moltbook-observatory-archive* (dataset). Hugging Face Datasets. https://huggingface.co/datasets/SimulaMet/moltbook-observatory-archive
- Manik, Md Motaleb Hossen; Wang, Ge. “OpenClaw Agents on Moltbook: Risky Instruction Sharing and Norm Enforcement in an Agent-Only Social Network.” arXiv (2026). https://arxiv.org/html/2602.02625
