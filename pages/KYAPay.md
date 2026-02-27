# KYAPay

**KYAPay** is an open protocol for identity-linked payments intended for agent-to-agent and agent-to-service interactions. The protocol is described by its maintainers as using JSON Web Tokens (JWTs) to package identity claims and payment-related authorization into verifiable, signed tokens that can be presented by software agents to services.

## Overview

The KYAPay repository describes the protocol as an "identity-linked payment protocol" for interactions involving autonomous or semi-autonomous software agents. It includes a core JWT data model and example APIs, and is published under the Community Specification License v1.0, with accompanying code under the MIT License.

A Skyfire post introducing the concept frames KYAPay as part of "agentic commerce"—transactions completed by AI agents on behalf of people or organizations—arguing that programmable identity and programmable payments are required for agent-driven transactions over APIs.

## Token model

The KYAPay whitepaper describes KYAPay as a lightweight, standards-compliant JWT-based format. It outlines three initial token types:

* **KYA Token** (typ: `kya+JWT`) for identity-only claims
* **Pay Token** (typ: `pay+JWT`) for payment authorization-only claims
* **KYA + Pay Token** (typ: `kya+pay+JWT`) combining identity and payment data

## Publication

The maintainers publish protocol materials in a public GitHub repository, including a core data model document and an example API document, and state that a full v1.0 specification is intended to be released in the repository.

## References

1. Skyfire (GitHub). "The KYAPay protocol (kyapay.org)". https://github.com/skyfire-xyz/kyapay
2. Skyfire. "Agentic Commerce: The Rise of Tokenized Payments and Identity". https://skyfire.xyz/agentic-commerce-the-rise-of-tokenized-payments-and-identity/
3. KYAPay. "KYAPay Protocol Launch Whitepaper". https://www.kyapay.ai/
