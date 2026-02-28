# PISP Credit Transfer Payment (W3C)

**PISP Credit Transfer Payment** is a W3C Web Payments Working Group *payment method specification* intended for use with the **Payment Request API**. It defines a payment method identifier and the request/response data exchanged when a user chooses to pay a merchant via a **Payment Initiation Service Provider (PISP)** using a bank credit transfer (e.g., SEPA). PISPs are defined in the European Union’s **Payment Services Directive 2 (PSD2)** framework.

## Overview

The specification’s goal is to enable merchants to accept bank credit transfers through a standardized browser-mediated flow:

- The payer selects a payment app that supports the **`pisp-credit`** payment method.
- The payment app returns information about the payer’s bank/account sufficient for the merchant (or merchant’s PISP) to route the payment initiation.
- The merchant’s PISP communicates with the payer’s bank, where the payer is authenticated to confirm the payment.
- The credit transfer is initiated only after the payer’s bank authenticates the payer.

The specification emphasizes that the Payment Request response indicates that a message has been submitted to the payee’s bank (not that funds have settled), and that merchants should rely on their bank’s notification to confirm clearing.

## Relationship to other Web Payments specs

PISP Credit Transfer Payment is designed as a **payment method specification** for the **Payment Request API**, and depends on:

- **Payment Request API** (defines the `PaymentRequest` constructor and overall payment request flow)
- **Payment Method Identifiers** (defines how payment method identifiers are structured and interpreted)

It also references banking identifiers used in credit transfers:

- **BIC** (ISO 9362:2014)
- **IBAN** (ISO 13616-1:2007)

## Payment method identifier

The payment method identifier for this payment method is:

- `pisp-credit`

## Data model

### Request data (merchant → user agent)

The specification defines a request dictionary that allows a merchant to indicate which credit transfer networks it supports:

- `supportedNetworks`: an optional sequence of network identifiers (e.g., SEPA). If omitted, the merchant accepts any network or the PISP determines an appropriate network.

### Response data (payment app → merchant)

The response dictionary includes:

- `payerAccount` (required): an **IBAN** identifying the payer’s account for routing.
- `payerName` (required): the account holder name (may differ from the buyer).
- `selectedNetwork` (optional): the credit transfer network selected for the transfer.

## Security and privacy considerations

The specification motivates the flow as a way to reduce exposure of sensitive bank details to merchants, while leveraging the regulatory and authentication environment of PSD2. It notes, for example, that under PSD2 the payer’s IBAN is not considered sensitive data and is used primarily for routing, and that the actual credit transfer does not occur until after the payer’s bank authenticates the payer.

## References

- W3C Web Payments Working Group. *PISP Credit Transfer Payment*. W3C Editor’s Draft. https://w3c.github.io/payment-method-pisp-credit/  
- W3C. *Payment Request API*. https://www.w3.org/TR/payment-request/  
- W3C. *Payment Method Identifiers*. https://www.w3.org/TR/payment-method-id/  
- European Union. *Directive (EU) 2015/2366 (PSD2) on payment services in the internal market*. https://eur-lex.europa.eu/eli/dir/2015/2366/oj  
- ISO. *ISO 9362:2014 — Financial services — Business identifier code (BIC)*. https://www.iso.org/standard/60390.html  
- ISO. *ISO 13616-1:2007 — Financial services — International bank account number (IBAN) — Part 1: Structure of the IBAN*. https://www.iso.org/standard/41031.html
