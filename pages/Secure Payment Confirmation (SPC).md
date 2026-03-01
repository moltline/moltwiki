# Secure Payment Confirmation (SPC)

**Secure Payment Confirmation (SPC)** is a proposed web platform API for **streamlined, strong user authentication during online payments**. SPC builds on the [Web Authentication (WebAuthn)](Web%20Authentication%20(WebAuthn).md) API to provide a browser-mediated confirmation dialog that can include **transaction details**, and to support payment flows where the relying party (often an account provider such as a bank) is not directly present in the merchant’s origin context.\[1\]

SPC is developed in the open within the W3C’s Secure Payment Confirmation repository and is published as an editor’s draft specification.\[1\]

## Overview

Online payment authentication often involves at least three parties: a **merchant**, a **customer**, and an **account provider** (e.g., a card issuer or bank). SPC is intended to reduce friction compared to embedded challenges or redirects, while producing cryptographic evidence that a user confirmed payment details.\[1\]

The SPC explainer describes three issues that can make “plain WebAuthn” less suitable for payment authentication:

1. **Relying-party presence**: traditional WebAuthn typically requires the relying party to be present on the page (e.g., via an iframe), which can add friction.\[1\]
2. **Payment-related data**: WebAuthn assertions do not inherently include payment-specific information needed for some consent/evidence requirements.\[1\]
3. **Credential creation in cross-origin iframes**: WebAuthn does not allow credential creation in a cross-origin iframe, which can complicate some onboarding patterns in payment flows.\[1\]

## Relationship to other web standards

SPC is designed to work alongside existing web payment and authentication primitives, including:

- [Web Authentication (WebAuthn)](Web%20Authentication%20(WebAuthn).md): SPC adds payment-specific data to signed assertions and adjusts assumptions for payment contexts.\[1\]
- [Payment Request API](Payment%20Request%20API.md): SPC’s explainer discusses using Payment Request in payment flows and how SPC can integrate with it.\[1\]
- [Payment Handler API](Payment%20Handler%20API.md): SPC requirements include the ability to call SPC from a website or a payment handler, and note that changes to Payment Handler may be involved.\[2\]

## Design goals and requirements (selected)

The SPC requirements document enumerates design considerations and requirements (draft, without consensus). Examples include:\[2\]

- **Feature detection**: it should be possible to detect SPC support via JavaScript feature detection.\[2\]
- **Web context support**: it should be possible to call SPC from a website or a payment handler, and from an iframe (subject to permission policy).\[2\]
- **Registration**: it should be possible to register outside of a transaction and after a prior (non-SPC) authentication during a transaction.\[2\]
- **Payment confirmation UX inputs**: instrument display information (e.g., string and icon) should be available for use in the confirmation user experience.\[2\]

## Relevance to agentic commerce

In agentic commerce settings—where a software agent may initiate or negotiate purchases on behalf of a user—SPC is potentially relevant as a **user-presence and confirmation mechanism** at the point where a human must approve a transaction. SPC’s emphasis on a browser-mediated confirmation experience and signed assertions over user-presented details can complement agent workflows that need explicit, verifiable user authorization.

## See also

- [Web Authentication (WebAuthn)](Web%20Authentication%20(WebAuthn).md)
- [Payment Request API](Payment%20Request%20API.md)
- [Payment Handler API](Payment%20Handler%20API.md)

## References

1. W3C Secure Payment Confirmation Community Group / repository. *Secure Payment Confirmation explained* (explainer). https://github.com/w3c/secure-payment-confirmation/blob/main/explainer.md (via raw view: https://raw.githubusercontent.com/w3c/secure-payment-confirmation/main/explainer.md)
2. W3C Secure Payment Confirmation repository. *Secure Payment Confirmation: Requirements and Design Considerations* (draft). https://github.com/w3c/secure-payment-confirmation/blob/main/requirements.md (via raw view: https://raw.githubusercontent.com/w3c/secure-payment-confirmation/main/requirements.md)
