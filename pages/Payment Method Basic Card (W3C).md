# Payment Method: Basic Card (W3C)

**Payment Method: Basic Card** is a W3C specification that defines data structures and a processing model for a card-based payment method identifier, typically used as `"basic-card"`, in the Web Payments ecosystem.

It was designed to be used with the **Payment Request API**, enabling a web site (merchant) to request payment using a standardized method identifier and a browser-mediated user experience. The Web Payments Working Group has since discontinued work on the document.

## Overview

In the W3C Web Payments architecture, a *payment method identifier* is a string that indicates a particular payment method a merchant supports. The Basic Card specification describes:

- a standardized payment method identifier (`"basic-card"`), and
- the data structures used to exchange card details and related information when that identifier is selected.

The Payment Request API allows a merchant to provide one or more supported payment method identifiers; the user agent (e.g., a browser) selects an appropriate payment app or built-in handler based on user choice and availability.

## Relationship to other Web Payments specifications

- **Payment Request API**: defines the browser-facing API for initiating a payment request and returning a payment response.
- **Payment Method Identifiers**: defines how payment method identifiers are defined and validated; Basic Card is an example of a standardized identifier.
- **Payment Handler API / Web-based Payment Handler**: defines how a payment app can be registered and invoked; Basic Card can be implemented by browser-integrated logic or by payment apps, depending on user agent support.

## Status and deprecation

The Web Payments Working Group has indicated that work on the Basic Card specification has been discontinued. Independently, browser vendors have also changed support for the `"basic-card"` method over time.

## See also

- [Payment Request API](Payment%20Request%20API.md)
- [Payment Handler API](Payment%20Handler%20API.md)
- [Payment Method Identifiers (W3C)](Payment%20Method%20Identifiers%20(W3C).md)

## References

- W3C (Editor’s Draft). *Payment Method: Basic Card*. https://w3c.github.io/payment-method-basic-card/
- W3C. *Payment Method Identifiers*. https://www.w3.org/TR/payment-method-id/
- W3C. *Payment Request API*. https://www.w3.org/TR/payment-request/
- Chromium Blog. *Sunsetting the "basic-card" payment method in the Payment Request API* (Oct 21, 2021). https://blog.chromium.org/2021/10/sunsetting-basic-card-payment-method-in.html
