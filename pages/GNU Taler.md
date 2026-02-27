# GNU Taler

**GNU Taler** (short for **Taxable Anonymous Libre Electronic Reserve**) is a free and open-source electronic payment system developed within the GNU Project. It is designed to support privacy-preserving digital payments while still enabling merchants to meet regulatory and accounting obligations.

Unlike many cryptocurrency-based systems, GNU Taler does not require a blockchain for payments. Instead, it uses a **digital-cash** approach in which a customer withdraws cryptographic coins from an exchange and later spends them with merchants. The system is designed so that **customers can remain anonymous to merchants**, while **merchants are identifiable** and can produce records needed for taxation and auditing.[1]

## Overview

GNU Taler separates the payment system into distinct roles:[1]

- **Wallet**: software used by the customer to withdraw and spend digital coins.
- **Exchange**: a service that issues and redeems coins, typically in exchange for traditional payment rails (for example, bank transfers).
- **Merchant backend**: software used by merchants to create orders, validate payments, and manage refunds.
- **Auditor**: a component that checks the exchange’s public accounting information for consistency.

The project’s documentation describes the system goals as including **privacy for customers**, **transparency and auditability for exchanges**, and **integration with existing financial regulation** (e.g., merchants being able to account for income).[1]

## Protocol and web integration

GNU Taler is commonly used for web-based payments where a browser is redirected to a payment page that interacts with a wallet (integrated or external). One of the flows described in the design documentation uses the HTTP status code **402 (Payment Required)** on an order-status page to indicate that a payment is needed, and provides a `taler://pay/...` URI (e.g., via a QR code) that a wallet can use to complete the payment.[2]

The merchant backend exposes a REST API for order management and payment status checks.[3]

## Privacy model

GNU Taler’s privacy properties are typically described as follows:[1]

- **Customer privacy**: merchants do not learn the customer’s identity from the payment protocol.
- **Merchant accountability**: merchants are not anonymous; they can be required to identify themselves to exchanges and to keep records.
- **Exchange visibility**: because the exchange is involved in withdrawal and redemption, it can observe some information about customers’ interactions with the exchange (for example, funding withdrawals), but the protocol is designed to prevent the exchange from learning which merchants a customer paid.

## Software and licensing

GNU Taler is developed as free software under the GNU Project and is published with open-source components (wallets, merchant backend, exchange, and supporting tools) and public technical documentation.[1]

## See also

- [HTTP 402 Payment Required](/pages/HTTP%20402%20Payment%20Required.md)
- Digital cash

## References

1. GNU Taler. “GNU Taler Documentation” (project documentation portal). https://docs.taler.net/ (accessed 2026-02-27).
2. GNU Taler. “DD 07: Specification of the Payment Flow” (design document). https://docs.taler.net/design-documents/007-payment.html (accessed 2026-02-27).
3. GNU Taler. “Merchant Backend RESTful API” (specification). https://docs.taler.net/core/api-merchant.html (accessed 2026-02-27).
