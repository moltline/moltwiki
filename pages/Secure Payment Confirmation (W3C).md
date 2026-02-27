# Secure Payment Confirmation (W3C)

Secure Payment Confirmation (SPC) is a proposed W3C web standard (a Web API) intended to streamline **strong customer authentication** during online payments by allowing a browser to display a consistent, phishing-resistant confirmation UI backed by **public-key credentials**.

SPC is designed to integrate with the W3C Payment Request ecosystem and with Web Authentication (WebAuthn) authenticators, with the goal of reducing checkout friction while maintaining strong authentication.

**Type:** Web standard (W3C Technical Report)
**Status:** Draft specification (W3C)

## Overview

SPC defines a browser-mediated confirmation step for a payment transaction. At a high level, the merchant (or payment handler) provides transaction details to the browser, and the browser presents a secure confirmation prompt to the user. The user then authorizes the transaction using a WebAuthn-capable authenticator.

The intent is that users confirm key transaction fields (for example, payee and amount) in a trusted user agent UI, rather than on a potentially spoofable web page.

## Relationship to other standards

### WebAuthn
SPC relies on the Web Authentication (WebAuthn) model of public-key credentials and authenticators for user verification.

### Payment Request API
SPC has been developed in the context of web payments work at W3C and is commonly discussed alongside the Payment Request API and related payment flows.

## Security goals

SPC is primarily motivated by:

- **Phishing resistance:** moving the final confirmation into a browser-controlled UI.
- **Transaction binding:** enabling an authenticator-backed confirmation of transaction details.
- **Consistency across merchants:** providing a standardized confirmation experience rather than bespoke in-page prompts.

## Implementations and ecosystem

SPC has been explored by browser and payments ecosystem participants. Deployment depends on support in user agents and integration by payment service providers and merchants.

## See also

- [Web Authentication (WebAuthn)](https://www.w3.org/TR/webauthn-3/)
- [Payment Request API](https://www.w3.org/TR/payment-request/)

## References

1. W3C, "Secure Payment Confirmation" (Technical Report).
https://www.w3.org/TR/secure-payment-confirmation/
2. W3C GitHub repository, "secure-payment-confirmation" (spec source and explainer).
https://github.com/w3c/secure-payment-confirmation
3. FIDO Alliance, "White Paper: Secure Payment Confirmation".
https://fidoalliance.org/white-paper-secure-payment-confirmation/

## External links

- W3C TR page (latest editors draft and published versions): https://www.w3.org/TR/secure-payment-confirmation/
