# GNU Taler

**GNU Taler** ("Taxable Anonymous Libre Electronic Reserve") is a free-software electronic payment system designed to provide **payer anonymity** while enabling **merchant transparency** for taxation and auditing. In GNU Taler’s architecture, customers obtain digital cash from an **exchange** using traditional payment rails (such as bank transfers), spend it with merchants, and merchants redeem it back to traditional money via the exchange.[1][2]

GNU Taler aims to provide cash-like privacy for customers while supporting regulatory and accounting requirements by making merchant income visible and auditable.[1][3]

## Overview

GNU Taler separates the privacy properties of the payer from those of the payee:

- **Customers** use a wallet to withdraw digital cash from an exchange and can pay merchants without revealing their identity to the merchant.[1]
- **Merchants** are not anonymous and can be audited, which is intended to support taxation of merchant revenue and compliance obligations.[1][2]
- **Exchanges** issue and redeem digital cash and are expected to be operated and audited similarly to financial institutions.[2]

The system is implemented as free software and documented through published protocols and REST-style APIs for its components.[2][3]

## Components

GNU Taler documentation describes multiple major components and services, including:

- **Exchange**: the service that issues (withdraws) and redeems (deposits) digital cash, and interacts with traditional banking infrastructure.[3]
- **Merchant backend / back office**: services and tools used by merchants to accept payments and manage operations.[3]
- **Bank integration / wire gateway**: software for integrating with banking protocols and payment rails.[3]

Supplemental services in the GNU Taler ecosystem include tools for encrypted backup and recovery and other infrastructure supporting wallets and operations.[3]

## Privacy and auditability goals

GNU Taler is described as an "anonymous, taxable payment system" in which cryptography is used to prevent participants from defrauding each other without detection.[2] The design goal is to preserve customer privacy for payments while allowing merchant-side auditability so that merchant income can be taxed appropriately.[1][2]

## Documentation

GNU Taler maintains a public documentation portal describing its APIs, component manuals, and tutorials.[2][3]

## References

1. GNU Taler. "GNU Taler: Introduction" (slide deck). https://www.gnu.org/ghm/2020-january/taler.pdf (accessed 2026-02-27).
2. GNU Taler Documentation. "GNU Taler Documentation." https://docs.taler.net/ (accessed 2026-02-27).
3. GNU Taler. "GNU Taler: Documentation and Resources." https://www.taler.net/en/docs.html (accessed 2026-02-27).
