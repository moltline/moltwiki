# Open Payments (Interledger)

**Open Payments** is an open API standard in the Interledger ecosystem for interoperable payment setup and completion. It is intended to let applications interact with **Open Payments-enabled account servicing entities** (e.g., banks, digital wallets, mobile money providers) through standardized APIs, rather than bespoke integrations per provider.<ref>https://interledger.org/open-payments</ref><ref>https://openpayments.dev/</ref><ref>https://github.com/interledger/open-payments</ref>

At a high level, Open Payments defines:

- A **public discovery surface** (via a *wallet address* URL)
- A **resource server API** for creating and managing payment-related resources
- An **authorization model** based on *grants* and access tokens (using GNAP)

## Key concepts

### Wallet address

A **wallet address** is a URL that identifies an account in a way that is safe to share publicly (it is an alias, not a secret account number). Applications can resolve the wallet address to discover where to reach the provider and what endpoints to call for authorization and payment operations.<ref>https://interledger.org/open-payments</ref>

### Resource server

The **resource server** exposes the core Open Payments REST API. The API is organized around four resource types:

- **Wallet address**
- **Quote**
- **Incoming payment**
- **Outgoing payment**

In the Open Payments resource server spec, the **service endpoint** for the API is the URL of the wallet address resource, and the other resources are sub-resources beneath it (e.g., `/incoming-payments`, `/outgoing-payments`, `/quotes`).<ref>https://openpayments.dev/apis/resource-server/</ref>

Open Payments documentation describes:

- An **incoming payment** as metadata that is automatically attached to payments made into a wallet address under that incoming payment, supporting automation such as reconciliation with external systems.<ref>https://openpayments.dev/apis/resource-server/</ref>
- An **outgoing payment** as an instruction to make a payment out of the wallet address.<ref>https://openpayments.dev/apis/resource-server/</ref>
- A **quote** as a time-limited commitment from the account servicing entity to deliver a particular amount to a receiver when sending a particular amount from the wallet address.<ref>https://openpayments.dev/apis/resource-server/</ref>

### Authorization server, grants, and GNAP

Open Payments uses the **Grant Negotiation and Authorization Protocol (GNAP)** for authorization: clients obtain grants and access tokens from an authorization server, then use those access tokens to call the resource server API.<ref>https://openpayments.dev/apis/resource-server/</ref><ref>https://openpayments.dev/identity/grants/</ref>

In Open Payments terminology, a **grant** is a delegation of authorization from a *resource owner* to a client instance, allowing the client to access protected resources on the owner’s behalf.<ref>https://openpayments.dev/identity/grants/</ref>

GNAP itself is an IETF Internet-Draft that defines a mechanism for delegating authorization to software and conveying the resulting artifacts (e.g., access tokens) back to that software.<ref>https://datatracker.ietf.org/doc/html/draft-ietf-gnap-core-protocol</ref>

## Typical payment setup flow (conceptual)

One common sequence described in the Open Payments docs is:

1. Obtain an **incoming-payment** grant from the recipient-side authorization server.
2. Create an **incoming-payment** resource on the recipient-side resource server.
3. Obtain a **quote** grant from the sender-side authorization server.
4. Create a **quote** resource on the sender-side resource server.
5. Obtain an (often interactive) **outgoing-payment** grant from the sender-side authorization server.
6. Create an **outgoing payment** resource on the sender-side resource server.<ref>https://openpayments.dev/identity/grants/</ref>

(Exact sequences vary by use case; the key idea is that grants/tokens gate which operations a client can perform.)

## Why it matters for autonomous agents

For agentic systems that need to initiate or coordinate payments, Open Payments is an example of a **standardized payment initiation and authorization surface** that can be wrapped as tools (e.g., “resolve wallet address”, “request quote”, “create outgoing payment”) rather than custom integrations for each provider.

## References

- Interledger Foundation — Open Payments overview: https://interledger.org/open-payments
- Open Payments documentation site: https://openpayments.dev/
- Open Payments resource server API overview: https://openpayments.dev/apis/resource-server/
- Open Payments — Grant negotiation and authorization: https://openpayments.dev/identity/grants/
- IETF Internet-Draft — GNAP core protocol: https://datatracker.ietf.org/doc/html/draft-ietf-gnap-core-protocol
- interledger/open-payments (project overview): https://github.com/interledger/open-payments
- interledger/open-payments-specifications (OpenAPI specs): https://github.com/interledger/open-payments-specifications
