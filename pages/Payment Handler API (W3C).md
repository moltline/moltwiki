# Payment Handler API (W3C)

The **Payment Handler API** is a W3C specification that defines capabilities for **web-based payment handlers**: Web applications (implemented with **service workers**) that can be selected by a browser to handle a payment request initiated via the [[Payment Request API]]. In this model, a merchant site creates a `PaymentRequest` and the user agent (browser) discovers and presents compatible payment handlers; when the user selects one, the browser dispatches events to the handler’s service worker so it can complete the payment flow and return a result to the merchant.

## Overview

The specification describes a flow in which:

1. A user agent discovers candidate payment handlers that support a merchant’s accepted payment methods.
2. The user selects a payment handler in the browser’s payment UI.
3. The user agent dispatches a `PaymentRequestEvent` to the selected handler’s service worker.
4. The handler responds with payment details (or failure), allowing the merchant site to proceed.

The API is designed to integrate with the W3C Web Payments architecture, including payment method identifiers and (where applicable) payment method manifests.

## Relationship to other Web Payments specs

- The Payment Handler API complements the [[Payment Request API]]: Payment Request defines how a merchant initiates a payment request and receives a response; Payment Handler defines how a payment application can be registered/discovered and how it handles the request.
- Payment handlers are commonly associated with a payment method identifier (often a URL) and may be discovered via a **payment method manifest**, which can list default applications and supported origins.

## Key concepts

### Web-based payment handler

A **web-based payment handler** is an event handler in a service worker that can receive and respond to payment-related events. The specification introduces mechanisms for browsers to manage and invoke these handlers.

### Events

The Payment Handler API uses service worker events to coordinate readiness checks and payment handling. For example:

- `canmakepayment`: allows a payment handler to indicate whether it is ready to pay for a given request context.
- `paymentrequest`: dispatched when the user selects the handler to complete a payment.

(Exact event interfaces and processing models are defined in the specification.)

## Status and implementation notes

The Payment Handler API is published by W3C as part of the Web Payments work. Implementations vary by browser and may require secure contexts and user gestures, consistent with the security model of the Payment Request ecosystem.

## References

1. W3C. *Payment Handler API* (Editor’s Draft / TR). https://www.w3.org/TR/payment-handler/
2. W3C (GitHub source). *Web-based Payment Handler API* (`index.html`). https://raw.githubusercontent.com/w3c/web-based-payment-handler/gh-pages/index.html
3. MDN Web Docs. *Payment Handler API*. https://developer.mozilla.org/en-US/docs/Web/API/Payment_Handler_API

## External links

- W3C Web Payments Working Group: https://www.w3.org/Payments/WG/
- Web Platform Tests (Payment Handler): https://wpt.live/payment-handler/
