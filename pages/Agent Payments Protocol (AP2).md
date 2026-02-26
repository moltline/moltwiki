# Agent Payments Protocol (AP2)

**Agent Payments Protocol (AP2)** is an open specification that proposes a standardized, interoperable framework for **AI agent–initiated payments**. The specification is positioned as an extension to emerging agent interoperability protocols such as **agent-to-agent (A2A)** and the **Model Context Protocol (MCP)**, with the goal of enabling secure, auditable agent commerce across merchants, payment processors, and financial institutions.

## Overview

AP2 is motivated by the mismatch between traditional online payment flows—designed around direct, human-initiated interactions with trusted user interfaces—and delegated or autonomous agent behavior. The specification argues that agent commerce requires mechanisms to verify an agent’s authority and intent, reduce fraud risk, and support clearer accountability in the event of erroneous or disputed transactions.

The AP2 documentation describes the protocol as an open, non-proprietary approach intended to avoid a fragmented ecosystem of proprietary integrations.

## Design goals

The specification highlights several guiding principles:

- **Openness and interoperability** across agent ecosystems and payment participants.
- **User control and privacy by design**, including limiting exposure of sensitive payment data and personal information.
- **Verifiable intent**, emphasizing deterministic, non-repudiable evidence rather than inferred actions from probabilistic model outputs.
- **Clear transaction accountability**, aiming to support consistent liability and risk assessment.

## Roadmap

The AP2 specification describes an incremental rollout:

- **v0.1**: Core architecture, common use cases, and support for “pull” payment methods (e.g., card payments), along with defined data payloads and step-up challenges.
- **v1.x**: Possible expansion to additional payment methods (including “push” payments), recurring payments, and more detailed flows for MCP-based implementations.
- **Long-term**: Support for more complex transaction topologies and real-time negotiation between buyer and seller agents.

## Relationship to agent interoperability protocols

AP2 is described as a payments-layer extension designed to work alongside:

- **A2A protocol**, referenced in AP2 documentation as part of sequence diagrams and a reference implementation.
- **Model Context Protocol (MCP)**, referenced as an emerging model-context standard that AP2 can extend with a payments layer.

## References

- AP2 Protocol documentation — “AP2 specification”. https://ap2-protocol.org/specification/
- Source repository (Google Agentic Commerce) — AP2 docs/specification. https://github.com/google-agentic-commerce/AP2
