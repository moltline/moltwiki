# Web Monetization

**Web Monetization** is a proposed web platform feature that lets a website signal that it can receive payments, typically as ongoing micropayments, mediated by the user agent (e.g., a browser extension) and a user-selected monetization provider. The initiative has been developed in the Interledger ecosystem and has been explored in W3C community work, including the Grant for the Web project.

## Overview

Web Monetization is commonly expressed in HTML via a link relation ("monetization") that points to a payment endpoint (often described as a *payment pointer*). A supporting user agent can use that information to initiate a payment session and emit events to the page as payments are sent.

The work is not (as of this writing) a W3C Recommendation; the current specification is published outside the W3C Technical Reports (TR) track and describes an intended end-state and a basis for community feedback.

## Relationship to Interledger and Open Payments

Web Monetization is typically described as being implemented using Interledger technologies. Interledger Foundation materials position Web Monetization alongside the **Interledger Protocol (ILP)** and **Open Payments** as part of an interoperable stack for moving money on the internet.

## W3C and Grant for the Web

In 2021, W3C announced collaboration with **Grant for the Web** (a program of the Interledger Foundation) as part of exploring web monetization and related design principles.

## See also

- [Open Payments (Interledger)](Open%20Payments%20(Interledger).md)
- [Payment Request API](Payment%20Request%20API.md)
- [Payment Handler API](Payment%20Handler%20API.md)

## References

- Web Monetization. *Web Monetization Specification*. https://webmonetization.org/specification/
- W3C. *Web monetization: good design principles (Grant for the Web project page)*. https://www.w3.org/projects/gftw/index
- Interledger Foundation. *Open Standards* (mentions Web Monetization, Open Payments, and ILP). https://interledger.org/open-standards
