# Web-based Payment Handler API (W3C)

The **Web-based Payment Handler API** is a W3C specification that defines how a **web application** can register as a **payment handler** and be invoked by the browser to respond to a merchant’s payment request initiated via the [Payment Request API](Payment%20Request%20API.md). It is part of the W3C **Web Payments** architecture and is designed around a **service worker** event model.[^w3c-web-based-payment-handler]

In this architecture, the merchant site calls `PaymentRequest.show()` (and optionally `canMakePayment()`), the user agent presents a chooser UI, and then the selected payment handler’s service worker receives a `paymentrequest` event and returns a response back to the merchant.[^w3c-web-based-payment-handler][^w3c-payment-request]

## Overview

A web-based payment handler is typically implemented as a **service worker** that:

- Is registered by an origin and granted permission to handle payment requests.
- Receives payment-related events (notably `paymentrequest`).
- Optionally opens a window to interact with the user.
- Produces a response that becomes the merchant’s `PaymentResponse`.

The specification also describes **just-in-time registration**, where a user agent may allow a payment handler to be registered during a transaction (for example, based on information discovered via a [payment method manifest](Payment%20Method%20Manifest%20(W3C).md)).[^w3c-web-based-payment-handler]

## Key interfaces and concepts

### `PaymentManager`

The spec extends `ServiceWorkerRegistration` with a `paymentManager` attribute, exposing the `PaymentManager` interface to payment handlers.[^w3c-web-based-payment-handler]

`PaymentManager` includes:

- `userHint`: a string that user agents may display to help users distinguish between handlers (e.g., a masked card suffix like “**** 1234”).[^w3c-web-based-payment-handler]
- `enableDelegations()`: a method for declaring which pieces of payer data the handler can provide via delegation.[^w3c-web-based-payment-handler]

### Delegations (`PaymentDelegation`)

The `PaymentDelegation` enum allows a handler to declare it can provide certain data elements, such as:

- `shippingAddress`
- `payerName`
- `payerPhone`
- `payerEmail`

This is intended to let the user agent and merchant rely on the payment handler to supply these fields when needed.[^w3c-web-based-payment-handler]

### `canmakepayment` event (`CanMakePaymentEvent`)

The Web-based Payment Handler API defines a `canmakepayment` event in the service worker global scope. A user agent may use this event to help filter available handlers (for example, to avoid showing handlers that cannot currently fulfill the request).[^w3c-web-based-payment-handler]

The handler responds via `CanMakePaymentEvent.respondWith(Promise<boolean>)` to signal whether it can make the payment.[^w3c-web-based-payment-handler]

## Relationship to other Web Payments specifications

- **[Payment Request API](Payment%20Request%20API.md):** the merchant-facing API that initiates the payment flow and ultimately receives a `PaymentResponse`.[^w3c-payment-request]
- **[Payment Method Identifiers](Payment%20Method%20Identifiers%20(W3C).md):** defines the identifier formats used to name payment methods.[^w3c-payment-method-id]
- **[Payment Method Manifest](Payment%20Method%20Manifest%20(W3C).md):** defines the manifest mechanism used for authorizing/discovering payment apps for a given payment method, and is referenced by the Web-based Payment Handler API’s just-in-time registration model.[^w3c-payment-method-manifest][^w3c-web-based-payment-handler]

## See also

- [Payment Handler API](Payment%20Handler%20API.md)
- [Payment Request API](Payment%20Request%20API.md)
- [Payment Method Manifest (W3C)](Payment%20Method%20Manifest%20(W3C).md)

## References

[^w3c-web-based-payment-handler]: W3C. “Web-based Payment Handler API.” https://www.w3.org/TR/web-based-payment-handler/
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^w3c-payment-method-manifest]: W3C. “Payment Method Manifest.” https://www.w3.org/TR/payment-method-manifest/
