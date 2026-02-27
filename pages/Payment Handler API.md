# Payment Handler API

The **Payment Handler API** is a Web platform specification that lets a **payment app** (typically implemented as a [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)) register to **handle payment requests** initiated via the [Payment Request API](https://developer.mozilla.org/en-US/docs/Web/API/Payment_Request_API). In supporting browsers, this enables web-based payment handlers (and, in some cases, platform apps referenced from a web app manifest) to participate in the browser’s payment UI flow. [^mdn-ph]

## Overview

At a high level:

1. A merchant site constructs a `PaymentRequest` and calls `show()` in response to a user gesture. [^mdn-ph]
2. The browser discovers payment handlers for the requested payment method(s) using the **payment method identifier** (often a URL) and associated manifests. [^mdn-ph]
3. A payment app’s Service Worker can be queried for readiness via a `canmakepayment` event, and asked to handle the transaction via a `paymentrequest` event. [^mdn-ph]

## Manifests and discovery

MDN describes a discovery flow where the browser loads the payment method identifier URL (e.g., `https://example.com/pay`) and looks for a `Link` header with `rel="payment-method-manifest"`; if present, it fetches the payment method manifest from that location, otherwise it may parse the response body at the identifier URL as the manifest. The payment method manifest can list default payment applications and supported origins. [^mdn-ph]

## Key events

A payment handler commonly uses Service Worker events:

- `canmakepayment`: allows the payment app to indicate whether it is ready to handle a payment for the given request. [^mdn-ph]
- `paymentrequest`: fired to initiate handling of a payment; the payment app may open a window for user interaction and then respond with the result. [^mdn-ph]

## Relationship to other web payments specs

- The Payment Handler API complements the [Payment Request API](Payment%20Request%20API.md) by enabling payment apps to integrate with browser-mediated payment flows. [^mdn-ph]
- It is also related to the concept of a **payment method manifest**, covered separately in [Payment Method Manifest (W3C)](Payment%20Method%20Manifest%20(W3C).md). [^mdn-ph]

## References

[^mdn-ph]: MDN Web Docs — “Payment Handler API”. https://developer.mozilla.org/en-US/docs/Web/API/Payment_Handler_API (accessed 2026-02-27)
