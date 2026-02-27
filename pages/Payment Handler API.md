# Payment Handler API

The **Payment Handler API** is a W3C Web Payments specification that enables Web applications ("payment handlers") to register with a user agent (e.g., a browser) to handle payment requests initiated by merchants through the [Payment Request API](./Payment%20Request%20API.md).

In effect, it defines how a browser can discover, invoke, and communicate with a payment app (often implemented as a service worker–based Web application) so that the app can provide payment instruments and complete a payment flow.

## Overview

The Payment Handler API is part of the W3C Web Payments ecosystem:

- **Merchant integration**: A merchant site uses the Payment Request API to request payment.
- **User agent mediation**: The browser presents available payment methods and routes the request.
- **Payment handler execution**: A registered payment handler receives the request and returns a response containing payment method–specific data.

The specification is designed to support multiple payment methods and to allow payment apps to integrate with the browser in a standardized way.

## Key concepts

### Payment handler

A **payment handler** is a Web application that can respond to a payment request. In many deployments, the handler is implemented with a **service worker** that can be invoked by the browser when a payment is requested.

### Payment method identifiers

Payment handlers typically declare which **payment method identifiers** they support. Payment method identifiers are defined separately (see [Payment Method Identifiers (W3C)](./Payment%20Method%20Identifiers%20(W3C).md)).

### Registration and invocation

A payment handler is registered with the user agent and can later be invoked during checkout when the user chooses it as the payment option. The API specifies the messages and events used to pass payment request details to the handler and to return a response.

## Relationship to other Web Payments specs

- [Payment Request API](./Payment%20Request%20API.md): Merchant-facing API to initiate a payment.
- [Payment Method Manifest (W3C)](./Payment%20Method%20Manifest%20(W3C).md): A mechanism for describing payment methods and where payment apps can be found.
- [Secure Payment Confirmation (W3C)](./Secure%20Payment%20Confirmation%20(W3C).md): A complementary API focused on strong customer authentication during payments.

## References

- W3C GitHub repository: https://github.com/w3c/payment-handler
- W3C Technical Report (TR): https://www.w3.org/TR/payment-handler/
- Editors Draft: https://w3c.github.io/payment-handler/

