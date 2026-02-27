---
title: Agent Definition Language (ADL)
---

# Agent Definition Language (ADL)

**Agent Definition Language (ADL)** is an open, vendor-neutral, declarative specification for describing AI agents in a consistent, auditable format. It is intended to standardize how an agent’s identity, model configuration, tools, permissions, retrieval-augmented generation (RAG) inputs, dependencies, and governance metadata are represented, with the goal of improving portability and interoperability across agent frameworks and platforms.

ADL is positioned as a “definition layer” for agents, analogous to the role of OpenAPI for HTTP APIs, and is explicitly focused on describing agents rather than executing them.

## Overview

In typical agent deployments, an agent’s behavior and constraints can be distributed across prompts, code, framework-specific configuration, and undocumented operational assumptions. ADL aims to consolidate these into a single machine-readable artifact that can be reviewed, validated, versioned, and shared across engineering, security, and compliance workflows.

The ADL project is published as an open-source specification under the Apache License 2.0.

## Scope

According to its maintainers, ADL defines agent attributes such as:

- **Identity and purpose** (e.g., name, description, role, ownership, version)
- **Language model configuration** (e.g., provider/model and settings)
- **Tools and actions** (including parameter descriptions and return schemas)
- **RAG inputs** (sources/indices and related metadata)
- **Permissions and sandbox boundaries** (e.g., file/network/environment access)
- **Dependencies** (e.g., packages and version pins)
- **Governance metadata** (e.g., creation/approval information and change history)

ADL does not define runtime execution semantics, tool invocation protocols, message transport, or agent-to-agent communication. The project describes ADL as complementary to protocols and standards such as the Model Context Protocol (MCP) and agent communication protocols.

## History

In February 2026, Next Moca announced and open-sourced ADL as a framework-agnostic specification intended to address fragmentation in how agents are defined and governed across vendors and platforms.

## References

- InfoQ. “Next Moca Releases Agent Definition Language as an Open Source Specification.” (Feb 2026). https://www.infoq.com/news/2026/02/agent-definition-language/
- Next Moca. “ADL — Agent Definition Language” (project repository). https://github.com/nextmoca/adl
