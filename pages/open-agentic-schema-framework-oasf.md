---
title: "Open Agentic Schema Framework (OASF)"
description: "AGNTCY’s schema framework for describing AI agents (records, skills/domains, modules) to support validation and discovery."
---

# Open Agentic Schema Framework (OASF)

The **Open Agentic Schema Framework (OASF)** is an open, standardized schema system for describing **AI agent records**—including agent identity and metadata, capabilities, and annotations (e.g., skills/domains)—so that agentic systems can validate, exchange, and discover agent descriptions in a consistent way.

OASF is developed in the **AGNTCY** ecosystem and is explicitly inspired by the **Open Cybersecurity Schema Framework (OCSF)** in its data-modeling philosophy and parts of its implementation.

## What OASF standardizes

OASF aims to provide common structures that make agent descriptions interoperable across tools and platforms:

- **Records as the primary object**: OASF centers on a “record” object as the main data structure for representing agentic information and metadata.
- **Taxonomies for discovery**: Records can be annotated with **skills** and **domains** to help with announcement and discovery across agent networks.
- **Extensibility via modules**: OASF supports modular extensions so third parties can add structured information without breaking compatibility.
- **Validation & tooling**: The project includes schema validation and a schema server for browsing and validating records.

## Schema server

A hosted schema server is provided for browsing the schema and related taxonomies, and the repository includes instructions for running the server locally.

## Versioning approach

OASF describes a **schema versioning and immutability** policy: once a schema version is released, it is intended to remain stable except for non-breaking fixes (e.g., documentation or minor bug corrections). Structural changes are expected to land in subsequent versions.

## Relationship to adjacent agent standards

OASF is often discussed alongside other agent interoperability efforts:

- **Agent Connect Protocol (ACP)**: a related AGNTCY specification focused on invoking/configuring remote agents over APIs.
- **Agent-to-agent protocols** (e.g., A2A): OASF is primarily about **describing** agents/records, whereas agent messaging protocols focus on **communication**.

## References

- AGNTCY OASF repository (README): https://github.com/agntcy/oasf
- Hosted OASF schema server: https://schema.oasf.outshift.com/
- AGNTCY documentation (OASF server docs): https://docs.agntcy.org/oasf/oasf-server/
- OCSF (inspiration): https://ocsf.io/
