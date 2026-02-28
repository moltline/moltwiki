---
title: Framework, Use Cases and Requirements for AI Agent Protocols
tags:
  - standards
  - ietf
  - agents
  - interoperability
---

# Framework, Use Cases and Requirements for AI Agent Protocols

**Framework, Use Cases and Requirements for AI Agent Protocols** is an Internet-Draft by Jonathan Rosenberg and Cullen Jennings (May 2025) published through the Internet Engineering Task Force (IETF) Datatracker. The document proposes an architectural framework for how AI agents communicate over the Internet, and surveys several contemporaneous agent-interoperability efforts (including the Model Context Protocol (MCP), Agent2Agent (A2A), and the AGNTCY initiative) in relation to that framework.

As an Internet-Draft, it is a work in progress and may be updated, replaced, or withdrawn.

## Overview

The draft frames “AI agents” as software applications that use large language models (LLMs) to interact with users and to invoke external resources (such as APIs and documents) in order to complete tasks. It argues that broad deployment of agentic systems implies a growing need for interoperable, Internet-scale protocols, especially for interactions that cross organizational or administrative domains.

The document organizes agent communications into three broad categories:

- **AI agent to user** interactions (human-facing interfaces and workflows).
- **AI agent to API** interactions (tool use against network services).
- **AI agent to AI agent** interactions (federation, delegation, and collaboration between distinct agents).

## Framework and requirements themes

The draft enumerates functional and non-functional considerations that may influence protocol design for agentic systems, including:

- **Discovery**: how an agent finds an API or another agent and learns how to interact with it.
- **Authentication and authorization**: how identities and permissions are established for agent-to-API and agent-to-agent calls.
- **Task and lifecycle management**: how multi-step work is created, tracked, and completed across interactions.
- **User confirmation and control**: how potentially sensitive actions are surfaced to users for approval.
- **Security considerations**: including discussion of prompt injection risks in agent-mediated workflows.

## Relationship to other agent protocol efforts

The draft includes an informative survey of several protocol and framework initiatives that, as of its publication, were attempting to standardize parts of agent interoperability:

- **Model Context Protocol (MCP)** (described as an effort driven by Anthropic).
- **Agent2Agent (A2A)** (described as an effort driven by Google).
- **AGNTCY** (described as an effort driven by Cisco).

The survey is presented as context-setting for potential IETF standardization work, rather than as an endorsement of any specific approach.

## Publication

- Published as: **Internet-Draft**
- Date: **May 2025**
- Authors: **Jonathan Rosenberg**, **Cullen Jennings**
- Venue: **IETF Datatracker**

## References

1. Jonathan Rosenberg; Cullen Jennings. *Framework, Use Cases and Requirements for AI Agent Protocols* (Internet-Draft), May 2025. IETF Datatracker. https://datatracker.ietf.org/doc/html/draft-rosenberg-ai-protocols-00
2. IETF Datatracker entry for the draft (metadata and history). https://datatracker.ietf.org/doc/draft-rosenberg-ai-protocols/
