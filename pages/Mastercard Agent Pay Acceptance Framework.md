# Mastercard Agent Pay Acceptance Framework

The **Mastercard Agent Pay Acceptance Framework** is a set of specifications and practices described by Mastercard for enabling merchants to accept payments initiated by AI agents in so-called *agentic commerce*. Mastercard presents the framework as a trust and interoperability layer focused on registering and verifying agents, and enabling tokenized transactions with minimal changes required by merchants.

## Overview

Mastercard positions the framework as addressing merchant concerns about distinguishing legitimate AI agents from malicious automation, verifying that a consumer authorized an agent to transact, and improving traceability and auditability of agent-initiated purchases.

In Mastercard’s description, the framework emphasizes:

- **Agent registration and verification** before an agent is permitted to transact on the Mastercard network.
- Use of **"agentic tokens"** (described as dynamic, cryptographically secured credentials) to initiate transactions and to make agent involvement recognizable.
- A "minimal lift" approach for merchants, including verification of agent authenticity at the **content delivery network (CDN) layer**, and reuse of existing checkout forms.

## Merchant verification approach

Mastercard states that merchants can verify agent authenticity by implementing an emerging **Web Bot Auth** standard at the CDN layer, allowing merchants to recognize Mastercard-approved agents while blocking untrusted traffic.

Mastercard also describes a mechanism in which verified agents submit a **Dynamic Token Verification Code** (an agentic token formatted for standard card payment fields) through existing checkout forms.

## Interoperability and related protocols

Mastercard describes the framework as designed to be compatible with multiple agent-oriented protocols and integration approaches, mentioning **Model Context Protocol (MCP)**, **Agent2Agent (A2A)**, and the **Agentic Commerce Protocol (ACP)** as examples of protocols that may be used for richer data exchange by "agentic-first" merchants.

Mastercard also states it is contributing to the **FIDO Payments Working Group** on the use of verifiable credentials for authenticating agent and consumer interactions.

## Industry partnerships

Mastercard has described partnerships intended to support adoption of the framework, including work with **Cloudflare** related to Web Bot Auth, and a collaboration with **PayPal** in which PayPal would pilot the framework in connection with integrating Mastercard Agent Pay into PayPal’s wallet.

## References

1. Mastercard. "Agentic token framework: Driving trusted AI transactions." *Mastercard News & Trends* (2025). https://www.mastercard.com/global/en/news-and-trends/stories/2025/agentic-commerce-framework.html
2. PayPal Newsroom. "Mastercard and PayPal Join Forces To Accelerate Secure Global Agentic Commerce." (27 Oct 2025). https://newsroom.paypal-corp.com/2025-10-27-Mastercard-and-PayPal-Join-Forces-To-Accelerate-Secure-Global-Agentic-Commerce
