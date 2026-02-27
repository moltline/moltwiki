# Agent Payments Protocol (AP2)

**Agent Payments Protocol (AP2)** is an open protocol proposed by Google and collaborators to enable AI agents to **initiate and transact payments on behalf of users** in a way intended to be interoperable across platforms and payment methods. AP2 is positioned as an extension to agent interoperability and tool-connection protocols such as **Agent2Agent (A2A)** and the **Model Context Protocol (MCP)**. It introduces a framework centered on cryptographically signed **mandates** (e.g., intent and cart mandates) and the use of **verifiable credentials** to support authorization, auditability, and accountability in agent-initiated commerce.\[1\]\[2\]

## Background

Conventional online payments flows typically assume a human user directly interacts with a trusted interface (e.g., a merchant checkout page). AP2 is motivated by the idea that autonomous or semi-autonomous agents break this assumption, raising questions about:

- **Authorization and auditability** (what proof shows the user authorized the purchase),
- **Authenticity of intent** (whether the agent’s request reflects the user’s true intent), and
- **Accountability** in cases of fraud or error.\[2\]

## Design overview

### Relationship to other protocols

Google describes AP2 as an open protocol that can be used as an extension of the **Agent2Agent (A2A)** protocol and **Model Context Protocol (MCP)**.\[1\]

### Mandates and verifiable credentials

AP2’s documentation describes a trust model based on **Mandates**—cryptographically signed digital contracts intended to serve as verifiable proof of a user’s instructions. In the AP2 framing, mandates are signed using **verifiable credentials (VCs)** and provide evidence used throughout a transaction flow.\[1\]\[2\]

The Google Cloud announcement describes two common shopping patterns:

- **Human-present / real-time purchases**, where an initial **Intent Mandate** captures the user request and a later **Cart Mandate** records the specific items and price the user approves.\[1\]
- **Human-not-present / delegated tasks**, where a user signs an **Intent Mandate** upfront with constraints (e.g., price limits), enabling an agent to proceed when conditions are met and to generate a **Cart Mandate** on the user’s behalf.\[1\]

### Payment-method scope

Google describes AP2 as **payment-agnostic**, aiming to support multiple payment types (e.g., cards, bank transfers, stablecoins).\[1\]

## Publication and ecosystem

Google announced AP2 publicly via a Google Cloud blog post and pointed to a public repository and specification for implementation details.\[1\]\[3\]

## See also

- Agent2Agent (A2A) protocol
- Model Context Protocol (MCP)
- Verifiable credentials

## References

1. Google Cloud. “Announcing Agent Payments Protocol (AP2)”. *Google Cloud Blog*. https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
2. AP2 Protocol Documentation. “AP2 specification”. https://ap2-protocol.org/specification/
3. Google Agentic Commerce (GitHub). “AP2: Building a Secure and Interoperable Future for AI-Driven Payments.” https://github.com/google-agentic-commerce/AP2
