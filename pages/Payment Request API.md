# Payment Request API

The **Payment Request API** is a web platform API for initiating a user agent–mediated payment flow from a merchant website. A merchant constructs a `PaymentRequest`, the browser shows a payment UI, and—if the user approves—the site receives a `PaymentResponse` describing the selected payment method and method-specific data.[^mdn]

In September 2022, the W3C Web Payments Working Group published Payment Request as a W3C Recommendation. The Working Group later republished the specification as a Candidate Recommendation Snapshot (published 2024-08-06) as part of an effort to realign the specification text with interoperable implementations.[^w3c-rec-2022][^w3c-cr-2024][^w3c-ed][^w3c-news-cr-2024]

## What it does (and does not do)

**What it does:**

- Standardizes the *browser-facing* checkout invocation: a website requests a payment UI and receives a structured response if the user authorizes.[^mdn]
- Lets the merchant declare which payment methods it supports via payment method identifiers, and provide method-specific request data.[^w3c-payment-method-id]
- Enables integration with payment handlers (including web-based payment apps) that can service a payment request.[^w3c-payment-handler]

**What it does not do:**

- It is not a payment processor and does not move funds by itself. Merchants still need a backend integration appropriate to the chosen payment method.
- It does not guarantee availability of any specific payment method across browsers; support varies by user agent and payment method.[^mdn]

## Core objects and flow

A typical flow is:

1. **Construct** a `PaymentRequest(methodData, details, options)` in response to a user action (e.g., clicking a “Buy” button).[^mdn]
2. Optionally check **`canMakePayment()`** to learn whether the user agent reports it can support the request (behavior is user agent–specific).[^webkit-applepay-pr]
3. Call **`show()`** to display the payment UI. If the user authorizes, the promise resolves to a `PaymentResponse`; if the user cancels, it rejects (e.g., `AbortError`).[^mdn-show][^webkit-applepay-pr]
4. Process the method-specific response data on the merchant side and then call **`PaymentResponse.complete()`** to signal completion to the user agent.[^mdn]

## Related Web Payments specs

The Payment Request API is commonly discussed alongside:

- **Payment Handler API** (enables web-based payment apps to handle payment requests)[^w3c-payment-handler]
- **Payment Method Identifiers** (defines identifiers used to name payment methods in the ecosystem)[^w3c-payment-method-id]
- **Secure Payment Confirmation (SPC)** (integrates with Payment Request flows and WebAuthn for stronger authentication)[^spc]

## Embedded contexts, permissions, and secure contexts

- **Permissions Policy:** The API is controlled by the `payment` Permissions Policy feature; MDN notes the default allowlist for `payment` is `self`.[^mdn-permissions-policy-payment]
- **Cross-origin iframes:** MDN documents that the API is available in cross-origin iframes only when explicitly enabled, historically via the `allowpaymentrequest` iframe attribute.[^mdn]
- **Secure contexts:** WebKit’s Payment Request guidance notes that construction can throw if the frame is not in a secure context (HTTPS).[^webkit-applepay-pr]

## Specification status

The Payment Request API was published as a W3C Recommendation in 2022 and later republished as a W3C Candidate Recommendation Snapshot in 2024.[^w3c-rec-2022][^w3c-cr-2024] The W3C Web Payments Working Group continues work in its GitHub-hosted editor’s draft, including efforts to realign the text with interoperable implementations.[^w3c-ed]

Earlier in the standardization process, the Working Group recorded changes related to shipping/contact information collection in response to privacy and internationalization review feedback.[^w3c-transitions-346]

## Implementations

Browser support has varied by vendor and payment method. For example, WebKit announced support for using the Payment Request API to conduct Apple Pay transactions in Safari 11.1 on macOS and Safari on iOS 11.3.[^webkit-applepay-pr]

## See also

- [Payment Handler API](Payment%20Handler%20API.md)
- [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)

## References

[^mdn]: MDN Web Docs. “Payment Request API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Request_API (last modified 2025-04-10).
[^mdn-show]: MDN Web Docs. “PaymentRequest: show() method.” https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequest/show
[^w3c-rec-2022]: W3C. “Payment Request API (Recommendation).” https://www.w3.org/TR/2022/REC-payment-request-20220908/
[^w3c-cr-2024]: W3C. “Payment Request API (Candidate Recommendation Snapshot).” https://www.w3.org/TR/payment-request/ (published 2024-08-06).
[^w3c-ed]: W3C Web Payments Working Group (Editor’s Draft / GitHub). “Payment Request API.” https://w3c.github.io/payment-request/
[^w3c-news-cr-2024]: W3C News. “W3C Invites Implementations of Payment Request API.” https://www.w3.org/news/2024/w3c-invites-implementations-of-payment-request-api/
[^w3c-transitions-346]: W3C Transitions (GitHub). “CR Snapshot Update Request for Payment Request API #346.” https://github.com/w3c/transitions/issues/346
[^w3c-payment-handler]: W3C. “Payment Handler API.” https://www.w3.org/TR/payment-handler/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^spc]: W3C. “Secure Payment Confirmation.” https://www.w3.org/TR/secure-payment-confirmation/
[^mdn-permissions-policy-payment]: MDN Web Docs. “Permissions-Policy: payment directive.” https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Permissions-Policy/payment (last modified 2025-07-04).
[^webkit-applepay-pr]: WebKit Blog. “Introducing the Payment Request API for Apple Pay.” https://webkit.org/blog/8182/introducing-the-payment-request-api-for-apple-pay/ (2018-03-29).
