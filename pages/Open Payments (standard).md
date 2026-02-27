---
title: Open Payments (standard)
---

# Open Payments (standard)

**Open Payments** is an open API standard from the Interledger Foundation intended to let applications initiate and manage payments by interacting with *wallet addresses* (URL-based identifiers) at Open Payments-enabled account providers. It is designed to reduce bespoke integrations between apps and financial institutions by providing a common interface for payment initiation and delegated access, while leaving the underlying settlement rails to providers and connected networks.

## Overview

Open Payments is positioned as a cross-provider interoperability layer for digital payments. In the Interledger Foundation’s framing, a user receives a **wallet address** from an Open Payments-enabled provider; applications can query that URL to learn how to request permission and coordinate payment initiation with the user’s provider, without exposing sensitive account details.

The specification is commonly described using an email analogy: wallet addresses are intended to be human-meaningful, publicly shareable aliases that work across providers that implement the same standard.

## Wallet addresses

A **wallet address** in Open Payments is a URL that acts as a public alias for an account.

According to the Interledger Foundation, wallet addresses are intended to be:

- **Memorable** (potentially including a user-chosen name),
- **Publicly shareable** (not equivalent to a card number or bank account number), and
- **Interoperable across providers** that implement the standard.

Because wallet addresses are URLs, applications can interact with them using web-style requests. The wallet address response is described as providing information such as where the account provider can be reached and how an application can request permission to initiate a payment.

## Delegated access and consent

Open Payments is designed around the idea that applications can request scoped capabilities (for example, to initiate a payment) and that the account owner retains control by granting explicit consent through their account provider. Interledger’s documentation emphasizes granular control over what an application can do, including constraints such as amount limits and time bounds.

## Relationship to settlement networks and Interledger

Open Payments focuses on **payment initiation and interoperability** between apps and account providers, but does not itself guarantee a single shared settlement layer.

Interledger documentation describes the **Interledger Protocol (ILP)** as complementary infrastructure that can help route and complete payments across connected networks and institutions, whereas Open Payments provides standardized initiation and authorization flows.

## Use cases

Interledger materials describe Open Payments as applicable to online payment scenarios such as:

- e-commerce purchases,
- subscription payments,
- donations and fundraising, and
- other application-initiated payments where users want direct control and reduced reliance on third-party payment gateways.

## Adoption and implementations

Interledger’s developer-facing materials describe adoption as ongoing, with early implementations by some wallet and financial service providers and reference/demo services used for experimentation.

## References

- Interledger Foundation. “Open Payments.” https://interledger.org/open-payments
- Interledger Foundation. “Open Payments is an open API standard…” https://openpayments.dev/
- Interledger Foundation (Developer Blog). Sarah Jones. “A Simple Guide to the Open Payments Standard” (Jul 9, 2024). https://interledger.org/developers/blog/simple-open-payments-guide/
