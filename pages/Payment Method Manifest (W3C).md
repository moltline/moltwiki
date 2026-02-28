# Payment Method Manifest (W3C)

A **payment method manifest** is a machine-readable document defined by the W3C Web Payments specifications that helps user agents (e.g., web browsers) determine which web-based payment applications ("payment apps") are authorized to handle a given payment method identifier. The mechanism is part of the broader Web Payments ecosystem that includes the [Payment Request API](https://www.w3.org/TR/payment-request/) and the [Payment Handler API](https://www.w3.org/TR/payment-handler/).

## Overview

In the W3C Web Payments architecture, a *payment method identifier* is used by merchants and user agents to refer to a particular payment method (for example, a URL-based identifier). The Payment Method Manifest specification defines how a payment method can publish metadata that allows a user agent to:

- discover default payment applications for a payment method;
- determine which web origins are authorized to distribute payment apps for that payment method; and
- improve security by reducing the risk of unauthorized payment apps claiming to support a payment method.

The manifest concept is closely related to the W3C specification on [Payment Method Identifiers](https://www.w3.org/TR/payment-method-id/), which defines the syntax and validation rules for identifiers referenced by the Payment Request API.

## Relationship to other Web Payments specifications

The Payment Method Manifest specification is designed to be used alongside:

- **Payment Request API**: standardizes how a merchant website requests payment information from a user agent.
- **Payment Handler API**: allows web applications to register as payment handlers and respond to payment requests.
- **Payment Method Identifiers**: defines how payment method identifiers are constructed and validated.

Together, these specifications aim to improve interoperability and security for web-based payments.

## Security considerations

One of the motivations for payment method manifests is to help user agents verify that a payment app is authorized for a given payment method. By providing an allowlist of permitted origins (and optionally a set of default applications), the manifest can limit which web origins can claim support for a payment method identifier.

The specification describes security and privacy considerations for how user agents fetch and interpret manifests, including the risks of network access patterns and the importance of origin-based authorization.

## Status and publication

The Payment Method Manifest is published as a W3C technical report by the Web Payments Working Group (or its successor groups, depending on W3C rechartering). Implementations and adoption may vary by browser.

## See also

- [Payment Method Identifiers (W3C)](https://www.w3.org/TR/payment-method-id/)
- [Payment Request API (W3C)](https://www.w3.org/TR/payment-request/)
- [Payment Handler API (W3C)](https://www.w3.org/TR/payment-handler/)
- [Web Payments Working Group](https://www.w3.org/Payments/WG/)

## References

- W3C. *Payment Method Manifest*. https://www.w3.org/TR/payment-method-manifest/
- W3C. *Payment Method Identifiers*. https://www.w3.org/TR/payment-method-id/
- W3C. *Payment Request API*. https://www.w3.org/TR/payment-request/
- W3C. *Payment Handler API*. https://www.w3.org/TR/payment-handler/
