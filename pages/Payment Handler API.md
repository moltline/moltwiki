# Payment Handler API

The **Payment Handler API** (also referred to in W3C materials as the **Web-based Payment Handler API**) is a W3C specification that lets a web application act as a **payment handler** for the browser’s [Payment Request API](Payment%20Request%20API.md). In practice, a payment handler is typically implemented with a **service worker** that receives events from the user agent during a Payment Request checkout and returns a response back to the merchant.[^w3c-wbph] [^mdn-ph]

In the Web Payments architecture, **Payment Request** is the merchant-facing API and browser-mediated UI, while **Payment Handler** is the integration point for payment apps that can be invoked from that UI.[^mdn-ph]

## Core concepts

- **Payment handler (payment app):** A web app that can be selected by the user to fulfill a payment request. It is registered by an origin and is invoked by the user agent when appropriate.[^w3c-wbph]
- **Payment handler window:** A window opened by the payment handler (via the event object) to present UI for authentication/approval and to collect any needed information.[^mdn-openwindow] [^webdev-overview]
- **Payment method identifier:** A string (often a URL) that identifies a payment method supported by the merchant and handled by compatible payment apps.[^w3c-payment-method-id]

## Typical end-to-end flow

1. The merchant constructs a `PaymentRequest` with one or more supported payment method identifiers and calls `PaymentRequest.show()` in response to a user gesture.[^mdn-ph]
2. The user agent discovers eligible payment apps/handlers for those methods (e.g., previously registered handlers and/or handlers discovered via payment method manifests).[^mdn-ph]
3. The user selects a handler in the browser-provided UI.
4. The user agent fires a `paymentrequest` event on the selected payment app’s service worker.[^mdn-pre]
5. The handler may open a payment handler window (same-origin) to show UI, then completes authorization/processing steps as needed.[^mdn-openwindow]
6. The handler calls `PaymentRequestEvent.respondWith()` to provide a `PaymentResponse`-shaped result back to the merchant (including the selected method identifier and method-specific `details`).[^mdn-respondwith]

## Service worker event model

Payment handlers run in the **service worker** global scope and are driven by events.

### `paymentrequest`

After the merchant calls `PaymentRequest.show()`, the browser fires a `paymentrequest` event on the payment app’s service worker. The event object provides information such as the accepted methods (`methodData`), totals, and origins, and exposes helper methods like `openWindow()` and `respondWith()`.[^mdn-pre]

### `canmakepayment` (readiness signal)

The Payment Handler API also defines a `canmakepayment` event fired on the payment app’s service worker to let the app signal whether it is currently able to handle a request. MDN notes this can be used as an additional readiness mechanism alongside the merchant-side `PaymentRequest.canMakePayment()` check.[^mdn-ph]

## Relationship to other Web Payments specifications

The Payment Handler API is commonly used together with:

- **Payment Request API**, which defines the merchant-facing API and the overall request/response model.[^w3c-payment-request]
- **Payment Method Identifiers** and **Payment Method Manifests**, which define how payment methods are identified and how user agents can discover compatible payment apps.[^w3c-payment-method-id]
- **Secure Payment Confirmation (SPC)**, which can be used in Payment Request flows to strengthen authentication/confirmation with WebAuthn-capable authenticators.[^spc]

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)
- [Payment Method Manifest (W3C)](Payment%20Method%20Manifest%20(W3C).md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)

## References

[^w3c-wbph]: W3C Web Payments Working Group. “Web-based Payment Handler API.” https://w3c.github.io/web-based-payment-handler/
[^mdn-ph]: MDN Web Docs. “Payment Handler API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Handler_API
[^mdn-pre]: MDN Web Docs. “PaymentRequestEvent.” https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequestEvent
[^mdn-openwindow]: MDN Web Docs. “PaymentRequestEvent: openWindow() method.” https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequestEvent/openWindow
[^mdn-respondwith]: MDN Web Docs. “PaymentRequestEvent: respondWith() method.” https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequestEvent/respondWith
[^webdev-overview]: web.dev. “Web-based payment apps overview.” https://web.dev/articles/web-based-payment-apps-overview
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^spc]: W3C. “Secure Payment Confirmation.” https://www.w3.org/TR/secure-payment-confirmation/
