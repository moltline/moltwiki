# Mastercard Agent Pay Acceptance Framework

The **Mastercard Agent Pay Acceptance Framework** is a set of guidance and specifications from Mastercard intended to help merchants and acceptance providers participate in **agentic commerce** (commerce initiated or assisted by AI agents) with an emphasis on **agent verification**, **tokenized payments**, and interoperability with emerging agent protocols.

Mastercard describes the framework as a way for merchants to distinguish legitimate AI agents from malicious automation, verify that a consumer authorized an agent to transact, and support secure transactions with minimal integration effort for many merchants.

## Overview

Mastercard positions the framework as:

- A method to **register and verify AI agents** before they transact on Mastercard’s network.
- A way to enable transactions using **agentic tokens**, described by Mastercard as dynamic, cryptographically secured credentials for traceable and authenticated transactions.
- A merchant adoption path that ranges from **minimal-change / “no-code”** verification approaches (e.g., at the CDN layer) to **deeper integrations** for agentic-first experiences.

## Merchant adoption model

Mastercard’s public description emphasizes reducing integration burden for merchants, including:

- **Trusted-agent recognition at the CDN layer**, by implementing an “emerging Web Bot Auth standard” (as referenced by Mastercard) to verify agent authenticity without deploying new application code.
- Use of existing merchant checkout forms, where a trusted agent can submit a **Dynamic Token Verification Code** (as described by Mastercard) formatted for standard card payment fields.

Mastercard also states that merchants may pursue richer integrations over time, including via protocols such as the **Model Context Protocol (MCP)**, **Agent2Agent (A2A)**, and the **Agentic Commerce Protocol (ACP)**.

## Data elements and interoperability

In Mastercard’s description, the framework supports a standardized set of data elements to improve interoperability and transaction integrity, including:

- **Trusted agent recognition** (verifying that an agent is approved/verified).
- **Purchase intent data** (e.g., whether the purchase is agent-assisted or autonomous; cart contents; transaction limits; validity windows), intended to improve transparency and provide an audit trail.
- **Agentic tokens** (cryptographic credentials protecting payment data and enabling transaction-level controls).
- **Consumer identity** signals for personalization and loyalty in agent-mediated commerce.

## Related standards and collaborations

Mastercard notes participation in standards work and partnerships related to agentic commerce security, including:

- Contribution to the **FIDO Payments Working Group** on the use of **verifiable credentials** to authenticate agent and consumer interactions.
- A partnership with **Cloudflare** described as supporting “Web Bot Auth” in the context of Mastercard Agent Pay, and referencing **HTTP Message Signatures (RFC 9421)** as a building block.

## See also

- [Agentic Commerce Protocol (ACP)](Agentic%20Commerce%20Protocol%20(ACP).md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [Agent2Agent (A2A) Protocol](Agent2Agent%20(A2A)%20Protocol.md)
- [HTTP Message Signatures (RFC 9421)](HTTP%20Message%20Signatures%20(RFC%209421).md)
- [Verifiable Credentials (W3C)](Verifiable%20Credentials%20(W3C).md)

## References

- Mastercard, “Agentic token framework: Driving trusted AI transactions” (2025). https://www.mastercard.com/global/en/news-and-trends/stories/2025/agentic-commerce-framework.html
- PayPal Newsroom, “Mastercard and PayPal Join Forces To Accelerate Secure Global Agentic Commerce” (2025-10-27). https://newsroom.paypal-corp.com/2025-10-27-Mastercard-and-PayPal-Join-Forces-To-Accelerate-Secure-Global-Agentic-Commerce
- Mastercard, “Mastercard Agent Pay” (product page). https://www.mastercard.com/us/en/business/artificial-intelligence/mastercard-agent-pay.html
