---
title: Payment Handler API (W3C)
---

# Payment Handler API (W3C)

The **Payment Handler API** is a W3C specification that enables a web application to act as a **payment handler** for the [Payment Request API](Payment%20Request%20API.md). It is designed to let browsers route a merchant’s checkout request to a user-selected payment app implemented on the Web, typically using a [service worker](https://www.w3.org/TR/service-workers/).

In the W3C Web Payments architecture, a merchant site (the **payee**) invokes `PaymentRequest.show()`. The user agent (browser) then discovers compatible payment handlers and, after user selection, dispatches a payment request event to the chosen handler, which returns data that becomes (or is used to construct) the `PaymentResponse` delivered back to the merchant site.

## Overview

A typical flow envisioned by the specification is:

1. A web origin registers itself as a payment handler (for one or more payment method identifiers) and may request permission to handle payment requests.
2. The payment handler is implemented in **service worker** code.
3. When a merchant invokes the Payment Request API (e.g., by calling `show()`), the browser computes a set of candidate payment handlers that match the merchant’s accepted payment methods.
4. The browser presents candidates to the user.
5. After the user chooses a handler, the browser fires a `PaymentRequestEvent` in the selected handler’s service worker.
6. The handler performs whatever steps are required to fulfill the request; if user interaction is needed, it can open a window.
7. The browser receives the handler’s response asynchronously and returns a `PaymentResponse` to the merchant.

(Adapted from the W3C editor’s draft description of the Payment Handler API flow.)

## Key concepts

### Web-based payment handler

A **web-based payment handler** is a payment app delivered from a web origin and implemented primarily via a service worker that listens for payment request events.

### PaymentRequestEvent

The specification defines a `PaymentRequestEvent` that is dispatched to the selected payment handler. The event carries details derived from the merchant’s `PaymentRequest` as well as additional context (for example, the payee’s origin) so that the handler can prepare an appropriate response.

### PaymentManager

The API extends service worker registration with a `PaymentManager` interface that allows a payment handler to manage properties used by the user agent (for example, presentation metadata such as labels and icons, depending on user-agent support and the specification’s current state).

## Relationship to other Web Payments specifications

The Payment Handler API is designed to complement:

- **Payment Request API** — standardizes the merchant-facing JavaScript API used to initiate a payment request and obtain a `PaymentResponse`.
- **Payment Method Identifiers** and **Payment Method Manifest** — define how payment methods are identified and how user agents can discover/install/register handlers for those methods.

## Security and privacy considerations

Because payment handling involves sensitive user and transaction data, the specification discusses security and privacy topics such as:

- permission and user mediation for registering and invoking payment handlers,
- isolation and origin-based security properties of service workers,
- user agent UI requirements intended to reduce spoofing and confusion during payment flows.

Implementations may also be analyzed in the context of broader security work on the W3C Web Payments APIs.

## References

- W3C. *Payment Handler API* (Technical Report). https://www.w3.org/TR/payment-handler/
- W3C Web Payments Working Group. *Payment Handler API source (Editor’s Draft)*. https://github.com/w3c/payment-handler/
- W3C. *Payment Request API* (Technical Report). https://www.w3.org/TR/payment-request/
- W3C. *Payment Method Identifiers* (Technical Report). https://www.w3.org/TR/payment-method-id/
- W3C. *Payment Method Manifest* (Technical Report). https://www.w3.org/TR/payment-method-manifest/
- W3C. *Service Workers 1* (Technical Report). https://www.w3.org/TR/service-workers/
- IEEE Computer Society. *A Formal Security Analysis of the W3C Web Payment APIs* (paper). https://www.computer.org/csdl/proceedings-article/sp/2022/131600a134/1FlQNCzbW7e
