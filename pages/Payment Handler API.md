# Payment Handler API

The **Payment Handler API** is a W3C specification that defines how a web application can act as a **payment handler** for payments initiated through the Web Payments ecosystem—most notably, via the **Payment Request API**. It enables a site (typically implemented using a **service worker**) to register itself as able to handle certain payment methods, and to receive a `PaymentRequestEvent` when the user selects it as the payment app.

In effect, the API provides a browser-mediated bridge between:

- a **payee/merchant** website that creates a `PaymentRequest`, and
- a **payer**’s chosen **web-based payment handler** that returns a payment response.

## How it fits into the Web Payments stack

The Payment Handler API complements other W3C Web Payments specifications:

- **Payment Request API**: used by merchants to request payment and present a browser UI for selecting a payment method/handler.
- **Payment Method Identifiers** and **Payment Method Manifest**: used to identify payment methods and (optionally) discover compatible handlers.

The Payment Handler API focuses on the **handler side**: registration, permissions, and dispatching the payment request to the handler.

## High-level flow

The specification describes a flow in which:

1. An origin requests permission from the user to handle payment requests for one or more supported payment methods.
2. Payment handlers are implemented in **service worker** code.
3. When a merchant calls `canMakePayment()` or `show()` on a `PaymentRequest`, the user agent computes candidate payment handlers, potentially including handlers registered previously via this API.
4. The browser presents candidate handlers to the user.
5. When the user selects a handler, the browser fires a `PaymentRequestEvent` in the handler’s service worker, carrying details from the `PaymentRequest` plus additional context (e.g., the payee origin).
6. The handler performs whatever steps are needed to handle the payment request and returns a response.

This flow is described in the specification’s “Overview” section. [^w3c-payment-handler-overview]

## Key concepts

### Web-based payment handler

A **web-based payment handler** is an event handler for `PaymentRequestEvent` running in a service worker context. [^w3c-payment-handler-intro]

### PaymentRequestEvent

The `PaymentRequestEvent` is the event delivered to the selected payment handler. It contains information derived from the merchant’s `PaymentRequest` (as defined by the Payment Request API), along with additional information needed by handlers (such as the payee’s origin). [^w3c-payment-handler-overview]

### PaymentManager

The API extends the service worker registration with a `PaymentManager` interface to manage properties of web-based payment handlers. [^w3c-payment-handler-intro]

## Security and privacy considerations (overview)

Because payment handlers participate in sensitive user flows, the model relies on browser enforcement and user mediation:

- **Permissioning**: an origin requests permission to handle payment requests for specified payment methods. [^w3c-payment-handler-overview]
- **Browser UI choice**: the user agent presents available handlers and the user selects which handler to use.
- **Service worker isolation**: handlers are implemented in service worker code, and the browser controls event dispatch and lifetime.

For detailed requirements and threat considerations, refer to the specification’s security and privacy sections. [^w3c-payment-handler]

## See also

- [[Payment Request API]]
- [[Payment Method Identifiers (W3C)]]
- [[Payment Method Manifest (W3C)]]
- [[Secure Payment Confirmation (W3C)]]

## References

[^w3c-payment-handler]: W3C. *Payment Handler API* (W3C Technical Report). https://www.w3.org/TR/payment-handler/

[^w3c-payment-handler-intro]: W3C. *Payment Handler API* — Introduction (defines features including `PaymentRequestEvent` and `PaymentManager`). https://www.w3.org/TR/payment-handler/

[^w3c-payment-handler-overview]: W3C. *Payment Handler API* — Overview (describes the end-to-end flow). https://www.w3.org/TR/payment-handler/
