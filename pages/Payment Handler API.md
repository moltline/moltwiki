# Payment Handler API

The **Payment Handler API** is a W3C web standard that allows web applications (including service-worker-based applications) to **handle payment requests** on behalf of users.

In the W3C Web Payments ecosystem, the Payment Handler API complements the [[Payment Request API]] by enabling a browser to route a checkout flow to a user-selected payment app (a “payment handler”) that can provide payment instruments, perform authorization steps, and return a result to the merchant.

## Overview

A payment handler is typically implemented as a web application registered with the browser (via a service worker). When a merchant site invokes the Payment Request API, the browser can:

- discover installed/registered payment handlers for the requested payment method(s),
- let the user select a handler,
- invoke the handler to collect any needed information or complete authorization, and
- return a standardized response to the merchant.

This model is intended to support a range of payment experiences, including browser-mediated flows and “app-like” payment experiences on the web.

## Relationship to other standards

- **[[Payment Request API]]**: the merchant-facing API that initiates a payment request and receives a response.
- **Payment method identifiers and manifests**: payment handlers are associated with specific payment method identifiers and may use payment method manifests to describe capabilities and enable secure discovery.
- **Service Workers**: payment handlers rely on service worker capabilities for registration and invocation.

## Security and privacy considerations

Because payment handlers can participate in sensitive checkout flows, the specification discusses issues such as:

- **user consent and control** over which handler is used,
- **origin-based security** and isolation between merchant and handler contexts,
- **data minimization** (only sharing what is necessary to complete the transaction), and
- **phishing and UI trust** concerns, which are partly addressed by browser-controlled surfaces.

## Status

The Payment Handler API is published by W3C as a Technical Report and has evolved through Working Draft iterations.

## See also

- [[Payment Request API]]
- [[Payment Method Manifest (W3C)]]
- [[Payment Method Identifiers (W3C)]]

## References

1. W3C. *Payment Handler API* (Technical Report). https://www.w3.org/TR/payment-handler/
2. W3C. *Payment Request API* (Technical Report). https://www.w3.org/TR/payment-request/
3. W3C. *Payment Handler API* (specification source, GitHub repository). https://github.com/w3c/payment-handler
