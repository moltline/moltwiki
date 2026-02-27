# Agentic Commerce Protocol (ACP)

The **Agentic Commerce Protocol (ACP)** is an open standard for enabling programmatic commerce flows between **buyers**, **AI agents**, and **businesses**. It is described as an interaction model that lets an agent and a merchant coordinate product selection, checkout, and fulfillment using structured messages and APIs, with the business remaining the merchant of record.

ACP has been publicly described by Stripe as an open standard codeveloped with OpenAI and used to power embedded checkout experiences in ChatGPT.

## Overview

ACP aims to reduce fragmentation in “agentic commerce” integrations by providing a common protocol that merchants and agent surfaces can implement once and reuse across compatible agents. Public materials describe ACP as supporting:

- **Product discovery and selection** in an agent interface.
- **Checkout initiation** and order creation via standardized API interactions.
- **Payment credential handling** via tokenized or delegated mechanisms (implementation-dependent).
- **Fulfillment and post-purchase updates**, including asynchronous flows.

## Specification and implementation

The ACP specification is published as an open-source project and includes machine-readable artifacts such as OpenAPI definitions and JSON Schemas, as well as RFC-style documents. The project uses **date-based versioning** (YYYY-MM-DD) for specification snapshots.

Public documentation describes production-facing implementations by OpenAI (for ChatGPT and related agent surfaces) and by Stripe (for merchant and payment tooling).

## Governance

The ACP repository describes the specification as being maintained by **OpenAI and Stripe** (as maintainers), with governance documentation published alongside the specification.

## See also

- [Universal Commerce Protocol (UCP)](Universal%20Commerce%20Protocol%20(UCP).md)
- [Agent Payments Protocol (AP2)](Agent%20Payments%20Protocol%20(AP2).md)

## References

1. Stripe. “Developing an open standard for agentic commerce.” *Stripe Blog*. https://stripe.com/blog/developing-an-open-standard-for-agentic-commerce
2. Agentic Commerce Protocol (ACP) specification repository. *GitHub*. https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
3. OpenAI Developers. “Agentic Commerce.” https://developers.openai.com/commerce/
