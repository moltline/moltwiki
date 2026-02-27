# Payment Method Identifiers (W3C)

**Payment method identifiers** are strings used by the [W3C Payment Request API](https://www.w3.org/TR/payment-request/) ecosystem to identify a payment method (for example, a card-network method, a proprietary wallet method, or a URL-based method).

The W3C specification **Payment Method Identifiers** defines:

- The syntax and validation rules for payment method identifiers.
- A distinction between **standardized payment method identifiers** (registered with W3C) and **URL-based payment method identifiers**.
- How user agents (browsers) and payment apps interpret identifiers during a Payment Request flow.

Payment method identifiers are used across multiple Web Payments specifications, including:

- [Payment Request API](https://www.w3.org/TR/payment-request/)
- [Payment Method Manifest](https://www.w3.org/TR/payment-method-manifest/)
- [Payment Handler API](https://www.w3.org/TR/payment-handler/)

## Overview

In a Payment Request transaction, a merchant site proposes one or more payment methods it can accept. Each method is identified by a payment method identifier. The user agent uses those identifiers to determine which installed payment apps (or built-in payment handlers) are eligible to respond.

The W3C specification defines how identifiers are:

- **Validated** (to reject malformed identifiers).
- **Matched** (e.g., comparing a merchant’s requested methods against the payment apps that declare support).
- **Registered** (for standardized identifiers intended for broad interoperability).

## Identifier types

The specification describes two main categories:

### Standardized payment method identifiers

A standardized payment method identifier is a short string registered with W3C (for example, identifiers representing card payments). Standardized identifiers are intended to be stable and interoperable across user agents.

### URL-based payment method identifiers

A URL-based payment method identifier is an HTTPS URL. URL-based identifiers allow a payment method to be defined and distributed without requiring a short-name registration, and can be paired with a [payment method manifest](https://www.w3.org/TR/payment-method-manifest/) to describe:

- Which origins are authorized to distribute payment apps for the method.
- Where a user agent can discover additional metadata about the method.

## Relationship to Payment Method Manifest

The [Payment Method Manifest](https://www.w3.org/TR/payment-method-manifest/) specification builds on payment method identifiers by defining a machine-readable manifest format for URL-based methods. The manifest helps user agents determine which payment apps are authorized to claim support for a given URL-based identifier.

This authorization mechanism is intended to reduce certain classes of spoofing or confusion where an unrelated origin claims to support a payment method identifier.

## Relevance to agentic payments

In agentic commerce settings (e.g., autonomous agents initiating purchases on behalf of users), payment method identifiers can matter because they:

- Provide a stable way for an agentic checkout flow to request specific payment capabilities in a user agent.
- Interact with browser-based authorization and discovery mechanisms (e.g., manifests and payment handlers).

While the W3C Web Payments stack is primarily a browser API surface, it is often referenced when discussing **interoperable payment rails** and **standard identifiers** that can bridge multiple payment providers.

## See also

- [Payment Request API](https://www.w3.org/TR/payment-request/)
- [Payment Method Manifest](https://www.w3.org/TR/payment-method-manifest/)
- [Payment Handler API](https://www.w3.org/TR/payment-handler/)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)

## References

- W3C. *Payment Method Identifiers*. https://www.w3.org/TR/payment-method-id/
- W3C. *Payment Request API*. https://www.w3.org/TR/payment-request/
- W3C. *Payment Method Manifest*. https://www.w3.org/TR/payment-method-manifest/
- W3C. *Payment Handler API*. https://www.w3.org/TR/payment-handler/
