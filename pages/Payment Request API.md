# Payment Request API

The **Payment Request API** is a web platform API that standardizes how a merchant website can invoke a browser-provided payment UI and exchange payment information with the user agent. It is part of the broader W3C Web Payments work and is designed to reduce checkout friction compared with traditional, form-based payment flows.[^mdn]

In September 2022, the W3C Web Payments Working Group published Payment Request as a W3C Recommendation; subsequent work has continued in W3C’s GitHub-hosted specification and Candidate Recommendation snapshots to better align the text with interoperable implementations.[^w3c-rec-2022][^w3c-edi]

## Overview

A merchant site typically creates a `PaymentRequest` object in response to a user gesture (e.g., clicking a “Buy” button). The browser then presents a native or browser UI that lets the user select a payment method and provide the necessary details. If the user approves, the site receives a `PaymentResponse` containing the selected payment method identifier and associated data.[^mdn]

The Payment Request API is commonly discussed alongside related specifications in the Web Payments ecosystem, including:

- **Payment method data and handlers:** In the Payment Request model, the merchant declares supported payment methods and any method-specific data; the user agent then coordinates with a suitable payment handler (which may be built-in or provided by a payment app) to collect authorization and return method-specific response data to the merchant.[^w3c-edi][^w3c-faq]

- **Payment Handler API** (enables web-based payment apps to handle payment requests)[^w3c-payment-handler]
- **Payment Method Identifiers** (defines identifiers used to name payment methods in the ecosystem)[^w3c-payment-method-id]
- **Secure Payment Confirmation (SPC)** (a W3C specification that integrates with Payment Request flows and WebAuthn for stronger authentication)[^spc]

## Key concepts

## Specification status

The Payment Request API was published as a W3C Recommendation in 2022.[^w3c-rec-2022] The W3C Web Payments Working Group has continued work on the specification in its GitHub-hosted drafts and Candidate Recommendation snapshots, including efforts to realign the text with interoperable implementations and to reintroduce address-related capabilities that were excluded from the 2022 Recommendation after privacy and internationalization review.[^w3c-edi]

- **User agent–mediated payment UI:** The browser mediates the user experience for selecting and authorizing payment, rather than the merchant building a bespoke checkout UI.[^mdn]
- **Payment method identifiers:** The API uses payment method identifiers to indicate which payment methods a merchant supports and which method the user selected.[^w3c-payment-method-id]
- **Extensibility via payment handlers:** Payment handlers allow payment apps (including web-based ones) to integrate with the Payment Request flow.[^w3c-payment-handler]
- **Embedded contexts:** The API can be used in cross-origin iframes only when the iframe is explicitly allowed (e.g., via `allowpaymentrequest`).[^mdn]

## See also

- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)

## References

[^mdn]: MDN Web Docs. “Payment Request API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Request_API (last modified 2025-04-10).
[^w3c-rec-2022]: W3C. “Payment Request API (Recommendation).” https://www.w3.org/TR/2022/REC-payment-request-20220908/
[^w3c-edi]: W3C Web Payments Working Group. “Payment Request API (Editor’s Draft / Candidate Recommendation Snapshot).” https://w3c.github.io/payment-request/ (see status section).
[^w3c-faq]: W3C Web Payments (GitHub wiki). “Payment Request API FAQ.” https://github.com/w3c/payment-request-info/wiki/FAQ
[^w3c-payment-handler]: W3C. “Payment Handler API.” https://www.w3.org/TR/payment-handler/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^spc]: W3C. “Secure Payment Confirmation.” https://www.w3.org/TR/secure-payment-confirmation/
