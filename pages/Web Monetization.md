# Web Monetization

**Web Monetization** is a proposed web platform feature that lets a website signal that it can receive payments from users, typically as ongoing micropayments, facilitated by the user agent and a user-selected monetization provider.[^spec]

## Overview

Web Monetization is commonly expressed in HTML via a link relation (`rel="monetization"`) that indicates a *payment pointer* used to monetize a document.[^spec] In the current specification, a payment pointer is defined as a URL to an Open Payments API entry point (a JSON resource containing details that facilitate payment to an account).[^spec]

A supporting user agent can use the payment pointer to initiate a payment session between a monetization provider and a monetization receiver.[^spec] The specification also defines `MonetizationEvent` DOM events, which include information such as the amount and currency sent and an `incomingPayment` URL that can be used to verify receipt of payment at the monetization receiver (often requiring authentication because it can expose sensitive details such as received amounts).[^spec]

The work is not a W3C Recommendation; the specification describes a desired end-state and is being developed in the open with the stated goal of potentially moving to the W3C standards track if it gains sufficient support.[^spec]

## Relationship to Interledger and Open Payments

The Web Monetization specification describes monetization providers as using the Interledger suite of protocols and technologies (for example, Open Payments-based systems) to pay a monetization receiver.[^spec] Interledger Foundation materials describe Web Monetization alongside the Interledger Protocol (ILP) and Open Payments as part of an interoperable set of open standards for payments on the internet.[^ilf]

## See also

- [Open Payments (Interledger)](Open%20Payments%20(Interledger).md)
- [Payment Request API](Payment%20Request%20API.md)
- [Payment Handler API](Payment%20Handler%20API.md)

## References

[^spec]: Web Monetization. "Web Monetization Specification." https://webmonetization.org/specification/
[^ilf]: Interledger Foundation. "Open Standards." https://interledger.org/open-standards
