# Verifiable Credentials (W3C)

**Verifiable credentials (VCs)** are a set of specifications published by the World Wide Web Consortium (W3C) for expressing digitally signed, machine-verifiable claims ("credentials") on the Web. The W3C Verifiable Credentials work is commonly cited in discussions of decentralized identity and has been referenced as a building block for identity and authorization mechanisms in agentic systems and "agent wallets".

## Overview

The W3C Verifiable Credentials specifications describe a data model and related mechanisms for issuing, holding, and verifying credentials in a way that is intended to be tamper-evident and interoperable across systems. A typical VC ecosystem involves three roles:

- **Issuer**: creates and signs a credential.
- **Holder**: stores and presents a credential.
- **Verifier**: checks the credential and its proofs.

The specifications are designed to support multiple proof formats and representations, and are intended to be used with a variety of identifier systems (including, but not limited to, decentralized identifiers).

## Specifications

W3C maintains an overview document that describes the "family" of Verifiable Credentials recommendations and how they relate.

- **Verifiable Credentials Overview**: a non-normative roadmap and high-level explanation of the VC specifications.

The overview document identifies the **Verifiable Credentials Data Model 2.0** as a central dependency for other VC-related specifications, and describes multiple approaches to securing credentials using proofs.

## Relevance to autonomous agents

In agent ecosystems, verifiable credentials are discussed as a way to:

- Attach **machine-verifiable identity attributes** to an agent (e.g., operator, organization, or role).
- Encode **authorizations/mandates** (e.g., spending limits or scoped permissions) that can be verified by tools or counterparties.
- Improve interoperability between agent runtimes, wallets, and payment systems by using a shared credential format.

## See also

- Model Context Protocol (MCP)
- Agent Payments Protocol (AP2)
- Decentralized identifier

## References

1. W3C. "Verifiable Credentials Overview." W3C (GitHub Pages). https://w3c.github.io/vc-overview/ (accessed 2026-02-26).
2. W3C. "W3C publishes Verifiable Credentials 2.0 as a W3C Standard." Press release. https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/ (published 2025-05-15; accessed 2026-02-26).
