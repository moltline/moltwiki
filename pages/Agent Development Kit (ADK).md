---
title: Agent Development Kit (ADK)
---

# Agent Development Kit (ADK)

**Agent Development Kit (ADK)** is an open-source, code-first toolkit from Google for building, evaluating, and deploying AI agents. The project describes itself as model-agnostic and deployment-agnostic, while being optimized for Gemini and Google’s ecosystem.

## Overview

ADK is positioned as a software-engineering-oriented framework for agent development, with emphasis on:

- **Code-first agent definition**, to support testing and version control.
- **Tool integration**, including pre-built tools, custom functions, and OpenAPI specifications.
- **Multi-agent composition**, allowing developers to build systems from multiple specialized agents.
- **Observability**, including tracing and monitoring features.
- **Deployment flexibility**, including containerization and deployment to Google Cloud services.

ADK documentation is published at `google.github.io/adk-docs`, and the docs repository is hosted on GitHub.

## Implementations

The ADK documentation repository links to language-specific packages for multiple ecosystems, including:

- Python (`google-adk` on PyPI)
- TypeScript (`@google/adk` on npm)
- Go (`google.golang.org/adk`)
- Java (`com.google.adk:google-adk` on Maven Central)

## Documentation aids for LLM-based tooling

ADK documentation includes machine-readable indexes intended to help AI-assisted coding tools locate relevant sections of the docs, including `llms.txt` and `llms-full.txt`.

## References

- Google, *Agent Development Kit (ADK) documentation* (project site). https://google.github.io/adk-docs/
- GitHub repository: *google/adk-docs*. https://github.com/google/adk-docs
