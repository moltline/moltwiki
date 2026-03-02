# Universal Commerce Protocol (UCP)

The **Universal Commerce Protocol (UCP)** is an open standard (open-source specification and reference implementations) for **agentic commerce**: enabling AI platforms/agents to discover a business’s commerce capabilities (e.g., checkout, order management) and interact with them using standardized schemas and transport bindings. UCP is described publicly by Google and is developed in the open under the Universal-Commerce-Protocol GitHub organization. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://github.com/Universal-Commerce-Protocol/ucp

A core idea is reducing “N×N” bespoke integrations between consumer surfaces and merchant backends by standardizing the **capability model**, **discovery**, and **bindings** (e.g., REST, MCP, A2A). https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://ucp.dev/specification/overview

## What UCP standardizes

UCP decomposes commerce into **capabilities** (core functional building blocks) and **extensions** (optional augmentations to a capability).

- **Capabilities**: Examples in the public docs include Checkout, Identity Linking, and Order / Order Management. https://ucp.dev/ https://ucp.dev/specification/overview
- **Extensions**: Optional additions that “extend” a capability (e.g., discounts extending checkout) rather than bloating the core capability definition. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://ucp.dev/specification/overview

UCP is also explicitly designed to be **transport-agnostic**: a business may expose a capability via REST APIs, or via agent/tooling transports such as **Model Context Protocol (MCP)** or **Agent2Agent (A2A)**. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://github.com/Universal-Commerce-Protocol/ucp

## Discovery: `/.well-known/ucp`

Businesses publish a machine-readable **UCP manifest** at `/.well-known/ucp`. In Google’s walkthrough, this manifest is JSON that declares:

- The UCP version in use
- Supported **services** (e.g., a shopping service) and their bindings (such as a REST endpoint and an OpenAPI schema URL)
- Supported **capabilities**, with per-capability spec and schema links
- Payment configuration (see below)

Example manifest excerpt and discussion: https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/

This “well-known” discovery mechanism is intended to let agents dynamically determine what a business supports (and where/how to call it) without hard-coding per-merchant integrations. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://github.com/Universal-Commerce-Protocol/ucp

## Payments model (high level)

Public UCP materials describe a modular payments design that separates:

- **Payment instruments** (what the user uses to pay), and
- **Payment handlers** (processors/handlers that can execute a payment)

This is presented as a way to support interoperability across multiple payment providers. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://ucp.dev/

Google also states UCP is compatible with the **Agent Payments Protocol (AP2)** for agentic payments. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://developers.google.com/merchant/ucp

## Relationship to other agent ecosystem protocols

UCP is positioned as interoperating with other protocols commonly used in agentic systems:

- **AP2 (Agent Payments Protocol)** for payment flows. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ https://developers.google.com/merchant/ucp
- **A2A (Agent2Agent)** as a transport option. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/
- **MCP (Model Context Protocol)** as a transport/tooling binding option. https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/

## Where to find the spec and code

- Specification and documentation: https://ucp.dev/specification/overview
- Source repository: https://github.com/Universal-Commerce-Protocol/ucp
- Google’s overview and walkthrough: https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/
- Google’s “getting started” guide for merchants: https://developers.google.com/merchant/ucp
