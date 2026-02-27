# Web Payments Overview 1.0 (W3C)

**Web Payments Overview 1.0** is a W3C Working Group Note that describes the **Web Payments ecosystem** at a conceptual level: its goals, the kinds of messages exchanged during a payment flow, and the roles of participants (payer, payee, mediator, payment app, payment network). It also links to specifications that define pieces of the ecosystem in more detail.[^w3c-note]

Unlike individual API specifications (e.g., browser APIs), the note is primarily an **architectural orientation document** intended to help implementers understand how the Web Payments family of specifications fits together.[^w3c-note]

## Goals

The note frames Web Payments goals in terms of general Web principles (e.g., device independence, accessibility, machine readability, and privacy) and additional ecosystem goals such as improving user experience, supporting a range of security needs, and enabling interoperability with existing and emerging payment schemes.[^w3c-note]

## Message structure

The document describes a **payment request** as comprising:

- **Payment methods** (which mechanisms can be used)
- **Payment details** (transaction-specific information)
- **Payment options** (information to be collected to fulfill the transaction, such as shipping or contact information)

It similarly describes a **payment response** as comprising:

- The selected **payment method**
- **Transaction details**
- **Response details** (including information requested in the payment request)

These conceptual pieces are reflected in the Web Payments browser-facing APIs, particularly the [Payment Request API](Payment%20Request%20API.md).[^w3c-note][^w3c-payment-request]

## Roles

The note identifies several roles and their interactions:

- **Payer**: transmits value to the payee
- **Payee**: receives value from the payer (e.g., a merchant)
- **Mediator**: routes payment requests between the payee and a payment app
- **Payment app**: processes payment requests and returns payment responses
- **Payment network**: transfers value between entities

In the browser-based Web Payments model, the **user agent** often plays the mediator role by presenting a payment UI and invoking payment apps (for example, via the [Payment Handler API](Payment%20Handler%20API.md)).[^w3c-note][^w3c-payment-handler]

## Relationship to other specifications

The note links to (and is commonly read alongside) several Web Payments specifications, including:

- **Payment Request API** (browser API for merchants to request payment)[^w3c-payment-request]
- **Payment Method Identifiers** (identifier formats for payment methods)[^w3c-payment-method-id]
- **Payment Handler API** (web-based payment apps that handle requests)[^w3c-payment-handler]
- **Payment Method Manifest** (authorization/discovery metadata for payment apps per payment method)[^w3c-payment-method-manifest]

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Payment Handler API](Payment%20Handler%20API.md)
- [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)
- [Payment Method Manifest (W3C)](Payment%20Method%20Manifest%20(W3C).md)
- [Secure Payment Confirmation (W3C)](Secure%20Payment%20Confirmation%20(W3C).md)

## References

[^w3c-note]: W3C. “Web Payments Overview 1.0.” https://www.w3.org/TR/webpayments-overview/
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
[^w3c-payment-handler]: W3C. “Payment Handler API.” https://www.w3.org/TR/payment-handler/
[^w3c-payment-method-id]: W3C. “Payment Method Identifiers.” https://www.w3.org/TR/payment-method-id/
[^w3c-payment-method-manifest]: W3C. “Payment Method Manifest.” https://www.w3.org/TR/payment-method-manifest/
