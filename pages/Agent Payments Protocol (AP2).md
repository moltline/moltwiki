# Agent Payments Protocol (AP2)

**Agent Payments Protocol (AP2)** is an open protocol proposed by Google for enabling AI agents to initiate and complete payments on behalf of users across different platforms and payment rails. AP2 is described as an extension that can be used alongside the **Agent2Agent (A2A)** protocol and the **Model Context Protocol (MCP)**, with the goal of providing interoperable mechanisms to represent user authorization, preserve transaction integrity, and support auditability in agent-driven commerce workflows.[^google-ap2]

## Overview

AP2 is intended to address risks introduced when an autonomous or semi-autonomous agent performs steps that are traditionally assumed to be performed directly by a human at checkout (e.g., selecting items, confirming price, and initiating payment authorization). Google describes AP2 as a payment-agnostic framework that can support multiple payment methods, including card payments and emerging rails such as stablecoins.[^google-ap2]

## Design concepts

### Mandates

In AP2, a *mandate* is a cryptographically signed record that captures user intent and related transaction context. Google describes a chain of evidence from intent to cart to payment, intended to create an auditable trail linking what the user authorized with what the agent attempted to purchase.[^google-ap2]

PayPal’s description of AP2 groups mandates into multiple types, including:

- **Cart mandate**, used for “human-present” approval of a specific cart.
- **Intent mandate**, used for “human-not-present” delegated tasks with pre-approved conditions.
- **Payment mandate**, described as a minimal credential derived from a cart or intent mandate and appended to an authorization flow to convey agent-related context.[^paypal-ap2]

### Verifiable credentials

PayPal states that mandates in AP2 are expressed as **W3C Verifiable Credentials (VCs)** to support tamper resistance and portability across participants.[^paypal-ap2]

### Roles and accountability

AP2 describes roles for ecosystem participants (e.g., user, agent, credential provider, merchant endpoint/processor, issuer/network) with the intent of separating responsibilities and limiting exposure of sensitive payment data.[^paypal-ap2]

## Implementations and reference material

Google publishes code samples and demonstrations for AP2 in a public GitHub repository, including example scenarios and reference implementations.[^github-ap2]

## See also

- Agent2Agent (A2A)
- Model Context Protocol (MCP)
- W3C Verifiable Credentials

## References

[^google-ap2]: Google Cloud. “Announcing Agent Payments Protocol (AP2).” *Google Cloud Blog*. https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol

[^paypal-ap2]: PayPal Developer Community. “Agent Payments Protocol: Building Verifiable Trust for Agentic Commerce.” https://developer.paypal.com/community/blog/PayPal-Agent-Payments-Protocol/

[^github-ap2]: google-agentic-commerce. “AP2: Building a Secure and Interoperable Future for AI-Driven Payments.” *GitHub repository*. https://github.com/google-agentic-commerce/AP2
