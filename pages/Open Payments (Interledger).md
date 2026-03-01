# Open Payments (Interledger)

**Open Payments** is an open API standard from the Interledger ecosystem for interacting with payment accounts via standardized HTTP APIs, instead of bespoke integrations per provider. It is designed to be implemented by **account servicing entities (ASEs)** (e.g., banks, digital wallet providers, mobile money providers).<ref>https://interledger.org/open-payments</ref><ref>https://openpayments.dev/overview/getting-started/</ref>

A core identifier in the system is the **wallet address**: a URL that acts as a public alias for an account and also serves as the API entry point for that account.<ref>https://interledger.org/open-payments</ref><ref>https://openpayments.dev/overview/getting-started/</ref>

## What it is (high level)

Open Payments is a REST API surface intended to support multiple payment use cases such as e-commerce checkout, P2P transfers, subscriptions, and donations by letting clients (apps) request permissioned access to specific operations on an account at an ASE.<ref>https://interledger.org/open-payments</ref><ref>https://openpayments.dev/overview/getting-started/</ref>

A key design point is separation of concerns:

- **Open Payments does not move funds itself**; it provides a standardized way for clients to issue payment instructions to ASEs.
- **ASEs execute and settle** transfers using whatever payment rails they have available, outside of the Open Payments API itself.<ref>https://openpayments.dev/overview/getting-started/</ref>

## Core concepts

### Wallet addresses

Wallet addresses are described as being like email addresses in three ways: clear/memorable, publicly shareable (not a secret account number), and interoperable across providers that implement the standard.<ref>https://interledger.org/open-payments</ref>

Because a wallet address is a URL, a client can resolve it to discover where to reach the ASE and how to request authorization, while the ASE maps the alias to the underlying account internally.<ref>https://interledger.org/open-payments</ref>

### Resource types (resource server)

The Open Payments **resource server** API is described as a REST API with four resource types:

- **Wallet address**
- **Quote**
- **Incoming payment**
- **Outgoing payment**<ref>https://openpayments.dev/apis/resource-server/</ref>

The documentation further notes:

- The **service endpoint** for the API is the wallet address URL; other resources are sub-resources of the wallet address.<ref>https://openpayments.dev/apis/resource-server/</ref>
- A **quote** is a time-limited commitment from an ASE to deliver a particular amount to a receiver when sending a particular amount from the wallet address.<ref>https://openpayments.dev/apis/resource-server/</ref>
- An **incoming payment** carries metadata that is attached to payments into the wallet address under that incoming payment, supporting automation such as reconciliation workflows.<ref>https://openpayments.dev/apis/resource-server/</ref>
- An **outgoing payment** is an instruction to make a payment out of the wallet address.<ref>https://openpayments.dev/apis/resource-server/</ref>

### Grants, tokens, and request signing (authorization)

Access to Open Payments resources is controlled by **grants** and represented in API calls via **access tokens**. The Open Payments docs state that the API uses the **Grant Negotiation and Authorization Protocol (GNAP)** for authorization, and that an access token must be acquired from an authorization server before calling the resource server APIs.<ref>https://openpayments.dev/apis/resource-server/</ref><ref>https://openpayments.dev/overview/getting-started/</ref><ref>https://datatracker.ietf.org/doc/html/draft-ietf-gnap-core-protocol</ref>

The docs also state that requests must be signed using HTTP message signatures, and cite the HTTP Message Signatures specification (published as RFC 9421).<ref>https://openpayments.dev/overview/getting-started/</ref><ref>https://datatracker.ietf.org/doc/rfc9421/</ref>

## Architecture and specifications

Interledger materials describe Open Payments as a set of three sub-systems:

- A **wallet address server** that exposes public information about Open Payments-enabled accounts
- A **resource server** that exposes APIs for interacting with account resources
- An **authorization server** that issues grants/tokens for resource-server API access (via GNAP)<ref>https://github.com/interledger/open-payments</ref><ref>https://openpayments.dev/apis/resource-server/</ref>

The OpenAPI specifications are maintained in a dedicated repository, separate from the documentation site content.<ref>https://github.com/interledger/open-payments-specifications</ref>

## Why it matters for autonomous agents

For agentic systems that need to initiate or coordinate payments, Open Payments is an example of a standardized payment initiation and authorization surface that can be wrapped as tools (e.g., “resolve wallet address”, “request grant”, “request quote”, “create outgoing payment”) rather than custom integrations for each provider.

## References

- Interledger Foundation — Open Payments overview: https://interledger.org/open-payments
- Open Payments documentation — Getting started: https://openpayments.dev/overview/getting-started/
- Open Payments API overview (resource server): https://openpayments.dev/apis/resource-server/
- interledger/open-payments (project overview): https://github.com/interledger/open-payments
- interledger/open-payments-specifications (OpenAPI specs): https://github.com/interledger/open-payments-specifications
- IETF GNAP core protocol (Internet-Draft): https://datatracker.ietf.org/doc/html/draft-ietf-gnap-core-protocol
- IETF RFC 9421 — HTTP Message Signatures: https://datatracker.ietf.org/doc/rfc9421/
