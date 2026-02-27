# Payment Request API

The **Payment Request API** is a web platform API that standardizes how a merchant website can invoke a browser-provided payment UI and exchange payment information with the user agent. It is part of the broader W3C Web Payments work and is designed to reduce checkout friction compared with traditional, form-based payment flows.[^mdn]

In September 2022, the W3C Web Payments Working Group published Payment Request as a W3C Recommendation; subsequent work has continued in W3C’s GitHub-hosted specification to better align the text with interoperable implementations.[^w3c-rec-2022][^w3c-ed]

## Overview

A merchant site typically creates a `PaymentRequest` object in response to a user gesture (e.g., clicking a “Buy” button). The browser then presents a native or browser UI that lets the user select a payment method and provide the necessary details. If the user approves, the site receives a `PaymentResponse` containing the selected payment method identifier and associated data.[^mdn]

The Payment Request API is commonly discussed alongside related specifications in the Web Payments ecosystem, including:

- **Payment Handler API** (enables web-based payment apps to handle payment requests)[^w3c-payment-handler]
- **Payment Method Identifiers** (defines identifiers used to name payment methods in the ecosystem)[^w3c-payment-method-id]
- **Secure Payment Confirmation (SPC)** (a W3C specification that integrates with Payment Request flows and WebAuthn for stronger authentication)[^spc]

## Key concepts

- **User agent–mediated payment UI:** The browser mediates the user experience for selecting and authorizing payment, rather than the merchant building a bespoke checkout UI.[^mdn]
- **Payee, payer, and payment method:** The specification describes the user agent as an intermediary between the payee (merchant), the payer (user), and the payment method used to pay.[^w3c-ed]
- **Payment method identifiers and method-specific data:** A merchant declares one or more supported payment methods (and optional method-specific data) when constructing a `PaymentRequest`.[^w3c-ed]
- **Transaction details and options:** The request includes transaction details (e.g., total and optional line items) and may include options needed to complete the transaction (e.g., requesting contact or shipping information, depending on implementation and specification version).[^w3c-ed][^mdn]
- **Embedded contexts:** The API is available in cross-origin iframes only when explicitly allowed (e.g., via the `allowpaymentrequest` attribute).[^mdn]

## See also

- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)
- [HTTP 402 Payment Required](HTTP%20402%20Payment%20Required.md)

## References

[^mdn]: MDN Web Docs. “Payment Request API.” https://developer.mozilla.org/en-US/docs/Web/API/Payment_Request_API (last modified 2025-04-10).
[^w3c-rec-2022]: W3C. “Payment Request API (Recommendation).” https://www.w3.org/TR/2022/REC-payment-request-20220908/
[^w3c-ed]: W3C Web Payments Working Group (GitHub). “Payment Request API (Editor’s Draft).” https://w3c.github.io/payment-request/
[^w3c-payment-handler]: W3C. “Payment Handler API.” https://www.w3.org/TR/payment-handler/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^spc]: W3C. “Secure Payment Confirmation.” https://www.w3.org/TR/secure-payment-confirmation/
