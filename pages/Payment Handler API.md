# Payment Handler API

The **Payment Handler API** is a set of Web platform features that let a *payment app* (typically implemented as a Progressive Web App using a service worker) handle payment requests initiated by merchant sites using the [Payment Request API](Payment%20Request%20API.md). In supporting browsers, the API enables a browser-mediated checkout flow where the user selects a payment app, and the app’s service worker receives events to validate readiness and complete the transaction.[^mdn-payment-handler]

The Payment Handler API is part of the broader W3C *Web Payments* standards family and is closely related to specifications that define payment method identification and discovery (e.g., payment method identifiers and manifests).[^webdev-setup][^w3c-payment-method-id]

## Overview

At a high level, a merchant constructs a `PaymentRequest` that lists one or more **payment method identifiers** (often URL-based identifiers) in `supportedMethods`. The user agent uses those identifiers to discover eligible payment apps, present them in a browser-provided UI, and—once the user chooses an app—invoke the selected app to handle the request.[^mdn-payment-handler][^webdev-setup]

For web-based payment apps, the Payment Handler API relies on a service worker that can respond to events such as:

- `canmakepayment`, which allows the payment app to indicate whether it is ready to handle a payment for the given request context.[^mdn-payment-handler]
- `paymentrequest`, which is fired to the payment app’s service worker to actually handle the payment flow and return a response to the user agent.[^mdn-payment-handler]

## Payment app discovery and manifests

In common deployments, discovery of a web-based payment app involves multiple documents linked to the payment method identifier:[^webdev-setup]

1. **Payment method identifier** (typically a URL controlled by the payment method owner).
2. **Payment method manifest**, a JSON document that can list default payment applications and (optionally) other supported origins.
3. **Web app manifest** for the payment app, which can declare a `serviceworker` entry used for payment handling.

This manifest chain enables browsers to locate and, in some cases, *just-in-time* install or register the payment app so that it can participate in Payment Request flows.[^mdn-payment-handler][^webdev-setup]

## Relationship to other Web Payments specifications

The Payment Handler API is usually discussed alongside:

- **Payment Request API**, which defines how merchant sites initiate a payment request and receive a response.[^w3c-payment-request]
- **Payment Method Identifiers**, which defines the identifiers used by merchants and user agents to refer to payment methods.[^w3c-payment-method-id]
- **Payment Method Manifest**, which defines the JSON manifest format used for payment method discovery.[^w3c-payment-method-manifest]

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)
- [Payment Method Manifest (W3C)](Payment%20Method%20Manifest%20(W3C).md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)

## References

[^mdn-payment-handler]: MDN Web Docs. “Payment Handler API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Handler_API
[^webdev-setup]: web.dev (Chrome Developers). “Setting up a payment method.” https://web.dev/articles/setting-up-a-payment-method (published 2017-09-27; last updated 2025-07-01).
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^w3c-payment-method-manifest]: W3C (Editor’s Draft). “Payment Method Manifest.” https://w3c.github.io/payment-method-manifest/
