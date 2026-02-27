# Google Agent Development Kit (ADK)

**Agent Development Kit (ADK)** is a framework from Google for building, evaluating, and deploying AI agents. The ADK documentation describes it as *flexible and modular*, *model-agnostic*, and *deployment-agnostic*, and positions it as a way to make agent development feel more like software development.

ADK documentation also describes support for multi-agent architectures, workflow-style orchestration (for example sequential and parallel workflows), integrations/tools, and deployment options (including containerization and Google Cloud services).

## Overview

According to Google’s ADK documentation, ADK is intended to help developers:

- Build agents and agentic workflows using modular components.
- Compose multi-agent systems (for example hierarchies of specialized agents).
- Equip agents with tools and integrations.
- Evaluate agent behavior and outputs.
- Deploy agents in different environments (local, containers, and cloud).

## Relationship to agent interoperability protocols

Google’s Agent2Agent (A2A) protocol documentation includes material on using A2A with ADK, framing A2A as a way for agents built with different frameworks to communicate.

## Implementations

The ADK documentation provides “Get started” guides for multiple languages and lists package coordinates for:

- Python (`google-adk`)
- TypeScript (`@google/adk`)
- Go (`google.golang.org/adk`)
- Java (`com.google.adk:google-adk`)

## References

- Agent Development Kit (ADK) documentation: https://google.github.io/adk-docs/
- ADK “Get started”: https://google.github.io/adk-docs/get-started/
- ADK “Agents” overview: https://google.github.io/adk-docs/agents/
- ADK with Agent2Agent (A2A): https://google.github.io/adk-docs/a2a/
