---
title: Google Agent Development Kit (ADK)
---

# Google Agent Development Kit (ADK)

**Agent Development Kit (ADK)** is an open-source, code-first framework from Google for building, evaluating, and deploying AI agents and multi-agent systems. ADK is positioned as modular and flexible, and is described as *model-agnostic* and *deployment-agnostic* while being optimized for Gemini models and the Google ecosystem (including Google Cloud deployment options). ADK is available in multiple language implementations, including Python and TypeScript/JavaScript.

## Overview

ADK aims to make agent development resemble conventional software development by encouraging explicit, version-controlled definitions of:

- agent behavior and instructions
- tool use (built-in, third-party, and custom tools)
- orchestration and composition of multi-agent systems
- evaluation and observability (e.g., tracing/monitoring)

Google’s documentation describes ADK as supporting both predictable workflow-style orchestration (e.g., sequential or parallel execution patterns) and more dynamic routing driven by an LLM agent.

## Language implementations

Google publishes ADK tooling and/or SDKs for multiple programming languages. Public documentation and repositories include:

- **Python** (package: `google-adk`)
- **TypeScript/JavaScript** (package: `@google/adk`)

The ADK documentation site also lists additional language tracks (for example Go and Java) with corresponding “get started” guides.

## Key concepts

While details vary by language implementation, ADK documentation commonly describes:

- **Agents** as autonomous execution units that can call tools and delegate to other agents.
- **Multi-agent composition** as a way to build systems from specialized agents organized hierarchically.
- **Tools and integrations** including built-in tools, custom functions, and third-party integrations.
- **Deployment options** including local execution and containerized/cloud deployment paths.

## Relationship to other agent protocols and ecosystems

The TypeScript ADK repository notes planned or emerging integration with the **Agent2Agent (A2A)** protocol for remote agent-to-agent communication.

## References

- Google ADK documentation: https://google.github.io/adk-docs/
- GitHub: `google/adk-docs` (documentation source repository): https://github.com/google/adk-docs
- GitHub: `google/adk-js` (TypeScript implementation): https://github.com/google/adk-js
- Google Developers Blog (announcement of ADK for TypeScript, Dec 17, 2025): https://developers.googleblog.com/introducing-agent-development-kit-for-typescript-build-ai-agents-with-the-power-of-a-code-first-approach/
