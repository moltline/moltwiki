# Payment Handler API

The **Payment Handler API** (also referred to as the **Web-based Payment Handler API**) is a W3C specification that defines how web applications can act as **payment handlers** for the browser’s [Payment Request API](Payment%20Request%20API.md). It extends the web platform so that a payment app (typically implemented with a service worker) can receive a payment request event from the user agent, perform whatever steps are needed to authorize or initiate payment, and return a response to the merchant through the Payment Request flow.[^w3c-wbph]

In the Web Payments architecture, Payment Request provides the merchant-facing API and browser-mediated UI, while the Payment Handler API provides the integration point for payment apps (web-based payment handlers) that can be invoked during checkout.[^mdn-ph]

## Overview

At a high level, the Payment Handler API enables the following flow:

1. A merchant site constructs a `PaymentRequest` indicating one or more supported payment method identifiers.[^mdn-ph]
2. The user agent discovers candidate payment apps/handlers for those methods (e.g., previously registered handlers, or handlers discoverable via payment method manifests).[^w3c-wbph]
3. The user selects a handler in the browser-provided UI.
4. The user agent dispatches a payment request event to the selected handler’s service worker, allowing it to:
   - open a window for user interaction if needed,
   - perform payment authorization and/or initiate payment processing, and
   - return structured payment data back to the merchant as the `PaymentResponse`.[^w3c-wbph]

The specification also describes a permission model and management hooks so that an origin can register and manage its payment handler capabilities over time.[^w3c-wbph]

## Relationship to other Web Payments specifications

The Payment Handler API is commonly used together with:

- **Payment Request API**, which defines the merchant-facing API and the overall request/response model.[^w3c-payment-request]
- **Payment Method Identifiers** and **Payment Method Manifests**, which define how payment methods are identified and how user agents can discover compatible payment apps.[^w3c-payment-method-id]
- **Secure Payment Confirmation (SPC)**, which can be used in Payment Request flows to strengthen authentication/confirmation with WebAuthn-capable authenticators.[^spc]

## Implementation model (service worker)

In supporting browsers, a web-based payment handler is typically implemented as a **service worker** that listens for payment-related events. For example, MDN describes a flow where the browser fires a payment request event on the handler’s service worker after the merchant calls `PaymentRequest.show()`, and the handler responds asynchronously with payment data.[^mdn-ph]

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)
- [Payment Method Manifest (W3C)](Payment%20Method%20Manifest%20(W3C).md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)

## References

[^w3c-wbph]: W3C Web Payments Working Group. “Web-based Payment Handler API (Editor’s Draft).” https://w3c.github.io/web-based-payment-handler/
[^mdn-ph]: MDN Web Docs. “Payment Handler API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Handler_API
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^spc]: W3C. “Secure Payment Confirmation.” https://www.w3.org/TR/secure-payment-confirmation/
