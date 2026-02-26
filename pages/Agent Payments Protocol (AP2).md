# Agent Payments Protocol (AP2)

**Agent Payments Protocol (AP2)** is an open protocol proposed by Google for enabling AI agents to initiate and complete payments on behalf of users in a way intended to be interoperable across agent platforms and payment methods. AP2 is described as an extension that can be used alongside agent-to-agent protocols such as **Agent2Agent (A2A)** and the **Model Context Protocol (MCP)**, and focuses on conveying an agent’s authority to transact, providing verifiable intent, and supporting auditability and accountability in agent-led commerce workflows.[^google-ap2][^ap2-spec]

## Overview

AP2 is positioned as a response to limitations in existing online payment flows, which generally assume a human user directly interacts with a merchant checkout interface. In agent-led commerce, a software agent may select goods or services and initiate payment, raising questions about authorization, authenticity of intent, and accountability in the event of error or fraud.[^google-ap2][^ap2-spec]

The AP2 documentation frames the protocol as payment-method agnostic, with the goal of supporting a range of rails (e.g., card payments and other methods) under a common framework for agent-initiated transactions.[^google-ap2]

## Design concepts

### Mandates

A central construct in AP2 is the **mandate**, described as a tamper-resistant, cryptographically signed digital contract capturing user instructions and approvals. The Google announcement describes a chain of mandates that can include an **Intent Mandate** (capturing the user’s request) and a **Cart Mandate** (capturing the final items and price approved for purchase). This sequence is presented as a way to create a non-repudiable audit trail from intent to payment.[^google-ap2]

### Verifiable credentials

AP2 describes using **verifiable credentials (VCs)** to sign mandates, with the intent of providing a verifiable proof of authority and supporting authentication and auditability for agent-initiated payments.[^google-ap2]

## Relationship to other agent protocols

AP2 is described as an extension that can be used with both **A2A** and **MCP**, reflecting an approach where a payments layer is added to agent communication and tool-use protocols rather than replacing them.[^google-ap2][^ap2-spec]

## Development and publication

Google published AP2 documentation and a technical specification via a public website and GitHub repository. The specification text describes AP2 as an open, interoperable protocol for agent payments and includes an initial roadmap for versions and reference implementations.[^google-ap2][^ap2-spec]

## References

[^google-ap2]: Google Cloud. "Announcing Agent Payments Protocol (AP2)." (accessed 2026-02-26). https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol

[^ap2-spec]: AP2 Protocol. "AP2 specification" (links to the specification document in the google-agentic-commerce/AP2 repository). (accessed 2026-02-26). https://ap2-protocol.org/specification/
