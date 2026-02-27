# Web Payments HTTP Messages

**Web Payments HTTP Messages** (sometimes referred to as **Web Payments HTTP Messages 1.0**) is a W3C specification that defines a set of HTTP message formats for initiating and acknowledging payment requests over HTTP. The work is part of the W3C **Web Payments** ecosystem and describes messages intended to support interactions among roles such as payers, payees, and payment service providers.[^w3c-tr][^w3c-gh]

The specification is distinct from browser APIs like the [Payment Request API](Payment%20Request%20API.md); instead, it focuses on protocol-level message structures transported via HTTP.[^w3c-tr]

## Overview

The specification defines “core Web Payments messages” used to:

- initiate a payment request via HTTP, and
- acknowledge a payment request via HTTP.[^w3c-tr]

It is designed to support a Web Payments architecture in which multiple parties exchange standardized payment-related messages, potentially enabling interoperable payment flows across different implementations.[^w3c-tr]

## Relationship to other Web Payments work

- **[Payment Request API](Payment%20Request%20API.md):** a web platform API for merchant sites to invoke browser-mediated payment UI. Web Payments HTTP Messages instead defines HTTP-level messages and does not require a browser-mediated UI.[^w3c-tr][^w3c-payment-request]
- **Web Payments Overview:** a separate W3C document that introduces goals, roles, and information flows in the Web Payments ecosystem.[^w3c-overview]

## Publication and status

W3C publishes the specification at `w3.org/TR/webpayments-http-messages/` and maintains an editor’s draft in a GitHub repository under the W3C organization.[^w3c-tr][^w3c-gh]

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Web-based Payment Handler API (W3C)](Web-based%20Payment%20Handler%20API%20(W3C).md)

## References

[^w3c-tr]: W3C. “Web Payments HTTP Messages 1.0.” https://www.w3.org/TR/webpayments-http-messages/
[^w3c-gh]: W3C (GitHub). “w3c/webpayments-http-messages.” https://github.com/w3c/webpayments-http-messages
[^w3c-overview]: W3C. “Web Payments Overview 1.0” (Editor’s Draft). https://w3c.github.io/webpayments-overview/
[^w3c-payment-request]: W3C. “Payment Request API.” https://www.w3.org/TR/payment-request/
