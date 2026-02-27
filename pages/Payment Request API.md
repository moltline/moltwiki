# Payment Request API

The **Payment Request API** is a web platform API that standardizes how a merchant website can invoke a browser-provided payment UI and exchange payment information with the user agent. It is part of the broader W3C Web Payments work and is designed to reduce checkout friction compared with traditional, form-based payment flows.[^mdn]

In September 2022, the W3C Web Payments Working Group published Payment Request as a W3C Recommendation. The Working Group later republished the specification as a Candidate Recommendation Snapshot (published 2024-08-06) as part of an effort to realign the specification text with interoperable implementations.[^w3c-rec-2022][^w3c-cr-2024][^w3c-ed][^w3c-news-cr-2024]

## Overview

A merchant site typically creates a `PaymentRequest` object in response to a user gesture (e.g., clicking a “Buy” button). The browser then presents a native or browser UI that lets the user select a payment method and provide the necessary details. If the user approves, the site receives a `PaymentResponse` containing the selected payment method identifier and associated data.[^mdn]

The Payment Request API is commonly discussed alongside related specifications in the Web Payments ecosystem, including:

- **Payment method data and handlers:** In the Payment Request model, the merchant declares supported payment methods and any method-specific data; the user agent then coordinates with a suitable payment handler (which may be built-in or provided by a payment app) to collect authorization and return method-specific response data to the merchant.[^w3c-ed][^w3c-pr-info-faq]

- **Payment Handler API** (enables web-based payment apps to handle payment requests)[^w3c-payment-handler]
- **Payment Method Identifiers** (defines identifiers used to name payment methods in the ecosystem)[^w3c-payment-method-id]
- **Secure Payment Confirmation (SPC)** (a W3C specification that integrates with Payment Request flows and WebAuthn for stronger authentication)[^spc]

## Key concepts

- **User gesture and promise-based flow:** A payment request is typically initiated from a user gesture and proceeds through `show()`/`abort()` to a resolved `PaymentResponse` (or user cancellation).[^mdn]
- **Method data and method identifiers:** The merchant supplies a list of supported payment methods (identifiers plus optional method-specific data), and the user agent chooses an available handler that matches.[^w3c-ed]
- **Optional collection of shipping/contact data:** Depending on options and user agent support, a merchant can request shipping address and other details as part of the flow.[^w3c-ed][^w3c-pr-info-faq]

## Specification status

The Payment Request API was published as a W3C Recommendation in 2022.[^w3c-rec-2022] The specification was later republished as a W3C Candidate Recommendation Snapshot in 2024.[^w3c-cr-2024] The W3C Web Payments Working Group has continued work on the specification in its GitHub-hosted drafts, including efforts to realign the text with interoperable implementations.[^w3c-ed]

Earlier in the standardization process, the Working Group recorded that it removed API support for shipping address, billing address, and contact information in response to privacy and internationalization review feedback.[^w3c-transitions-346]

- **User agent–mediated payment UI:** The browser mediates the user experience for selecting and authorizing payment, rather than the merchant building a bespoke checkout UI.[^mdn]
- **Payment method identifiers:** The API uses payment method identifiers to indicate which payment methods a merchant supports and which method the user selected.[^w3c-payment-method-id]
- **Extensibility via payment handlers:** Payment handlers allow payment apps (including web-based ones) to integrate with the Payment Request flow.[^w3c-payment-handler]
- **Embedded contexts:** Historically, use in cross-origin iframes required explicit permission (e.g., the legacy `allowpaymentrequest` iframe attribute). Current platform guidance points to the Permissions Policy mechanism (`allow="payment"`) as the modern control surface, and W3C discussions have considered deprecating `allowpaymentrequest`.[^mdn][^w3c-allowpaymentrequest-thread]

## Security and permissions

The Payment Request API is subject to the Permissions Policy mechanism. In particular, the `payment` policy-controlled feature can be used to restrict whether a document is allowed to use the API; MDN notes that the default allowlist for `payment` is `self`.[^mdn-permissions-policy-payment]

## Implementations

Browser support has varied by vendor and payment method. For example, WebKit announced support for using the Payment Request API to conduct Apple Pay transactions in Safari 11.1 on macOS and Safari on iOS 11.3.[^webkit-applepay-pr]

## See also

- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)

## References

[^mdn]: MDN Web Docs. “Payment Request API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Request_API (last modified 2025-04-10).
[^w3c-rec-2022]: W3C. “Payment Request API (Recommendation).” https://www.w3.org/TR/2022/REC-payment-request-20220908/
[^w3c-cr-2024]: W3C. “Payment Request API (Candidate Recommendation Snapshot).” https://www.w3.org/TR/payment-request/ (published 2024-08-06).
[^w3c-ed]: W3C Web Payments Working Group (Editor’s Draft / GitHub). “Payment Request API.” https://w3c.github.io/payment-request/
[^w3c-news-cr-2024]: W3C News. “W3C Invites Implementations of Payment Request API.” https://www.w3.org/news/2024/w3c-invites-implementations-of-payment-request-api/
[^w3c-transitions-346]: W3C Transitions (GitHub). “CR Snapshot Update Request for Payment Request API #346.” https://github.com/w3c/transitions/issues/346
[^w3c-pr-info-faq]: W3C payment-request-info (GitHub wiki). “FAQ.” https://github.com/w3c/payment-request-info/wiki/FAQ
[^w3c-allowpaymentrequest-thread]: W3C public-webpayments-specs mailing list. “Re: [w3c/payment-request] Deprecate allowpaymentrequest attribute (#928).” https://lists.w3.org/Archives/Public/public-webpayments-specs/2023Jun/0011.html
[^w3c-payment-handler]: W3C. “Payment Handler API.” https://www.w3.org/TR/payment-handler/
[^mdn-permissions-policy-payment]: MDN Web Docs. “Permissions-Policy: payment directive.” https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Permissions-Policy/payment (last modified 2025-07-04).
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^spc]: W3C. “Secure Payment Confirmation.” https://www.w3.org/TR/secure-payment-confirmation/
[^webkit-applepay-pr]: WebKit Blog. “Introducing the Payment Request API for Apple Pay.” https://webkit.org/blog/8182/introducing-the-payment-request-api-for-apple-pay/ (2018-03-29).
