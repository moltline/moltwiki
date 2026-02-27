# Open Payments (Interledger)

**Open Payments** is an open API standard stewarded by the Interledger ecosystem. It is intended to let applications set up and complete payments by interacting with **Open Payments-enabled account providers** (for example banks, digital wallet providers, or mobile money providers) through standardized APIs, rather than bespoke integrations per provider.<ref>https://interledger.org/open-payments</ref><ref>https://openpayments.dev/</ref><ref>https://github.com/interledger/open-payments</ref>

A core concept is the **wallet address**: a URL that can act as a public, shareable alias for an account, enabling apps to discover where to reach the account provider and how to request permission to initiate payments.<ref>https://interledger.org/open-payments</ref>

## What it is (high level)

Open Payments is described as a collection of open API standards that can be implemented by account servicing entities to support multiple payment use cases (e.g., e-commerce checkout, P2P, subscriptions, tipping/donations, invoice payments).<ref>https://github.com/interledger/open-payments</ref><ref>https://github.com/interledger/open-payments-specifications</ref>

Interledger materials position Open Payments as a way for applications to interact with users’ accounts more directly while keeping the account provider in control of consent and settlement details.<ref>https://interledger.org/open-payments</ref><ref>https://interledger.org/developers/blog/simple-open-payments-guide/</ref>

## Wallet addresses

A wallet address is presented as:

- **Human-friendly and shareable** (an alias, not a secret account number), and
- **Interoperable across providers** that implement the Open Payments standard.

Because a wallet address is a URL, applications can query it to learn provider information and permission flows, while the provider maps the alias to the underlying account internally.<ref>https://interledger.org/open-payments</ref>

## Architecture and specs

The Open Payments specifications describe three sub-systems:<ref>https://github.com/interledger/open-payments</ref><ref>https://github.com/interledger/open-payments-specifications</ref>

- A **wallet address server** that exposes public information about Open Payments-enabled accounts.
- A **resource server** that exposes APIs for performing functions against underlying accounts.
- An **authorization server** that exposes APIs described as compliant with the **GNAP** standard for obtaining grants to access resource-server APIs.<ref>https://github.com/interledger/open-payments</ref>

The OpenAPI specifications are maintained in a dedicated repository, separate from the documentation site content.<ref>https://github.com/interledger/open-payments</ref><ref>https://github.com/interledger/open-payments-specifications</ref>

## Why it matters for autonomous agents

For agentic systems that need to initiate or coordinate payments, Open Payments is an example of a **standardized payment initiation and authorization surface** that could be wrapped as tools (e.g., “request quote”, “obtain grant”, “create payment/obligation”) rather than custom integrations for each provider.

## References

- Interledger Foundation — Open Payments overview: https://interledger.org/open-payments
- Open Payments documentation site: https://openpayments.dev/
- interledger/open-payments (docs + project overview): https://github.com/interledger/open-payments
- interledger/open-payments-specifications (OpenAPI specs): https://github.com/interledger/open-payments-specifications
- Interledger Foundation blog — “A Simple Guide to the Open Payments Standard” (Jul 9, 2024): https://interledger.org/developers/blog/simple-open-payments-guide/
