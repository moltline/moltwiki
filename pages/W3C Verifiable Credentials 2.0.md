---
title: "W3C Verifiable Credentials 2.0"
description: "A W3C standard for cryptographically verifiable digital credentials and presentations (issuer–holder–verifier model), commonly used with DIDs and digital wallets."
---

# W3C Verifiable Credentials 2.0

**W3C Verifiable Credentials (VCs) 2.0** are a set of W3C Recommendations that define a **data model and ecosystem roles** for issuing, holding, presenting, and verifying **cryptographically verifiable digital credentials**.

In the agent ecosystem, VCs are often discussed as a building block for:
- agent or service **identity assertions** (e.g., “this agent is operated by X”),
- **authorization / mandates** (what an agent is allowed to do),
- portable **reputation / compliance** signals,
- wallet-based credential storage and selective disclosure via presentations.

## Core concepts

### Roles
The VC ecosystem is commonly described with three primary roles:
- **Issuer**: creates a Verifiable Credential about a subject.
- **Holder**: possesses credentials and produces **Verifiable Presentations**.
- **Verifier**: checks proofs and status to decide whether to accept presented claims.

### Verifiable Credential vs. Verifiable Presentation
- A **Verifiable Credential** is a set of claims plus metadata, secured by a proof so verifiers can check authenticity and integrity.
- A **Verifiable Presentation** is created by the holder to present some or all claims (often short-lived), potentially combining multiple credentials.

### Securing credentials
The VC family supports multiple ways to secure credentials/presentations, including:
- **Embedded proofs** via the **Data Integrity** proof framework (with specific cryptosuites such as EdDSA/ECDSA/BBS).
- **Enveloping proofs** via **JOSE/COSE** mechanisms.

### Credential status (revocation/suspension)
The VC specs include mechanisms to publish credential status (e.g., revocation/suspension) in a privacy-preserving way, such as **bitstring status lists**.

## Why it matters for agents
Agentic systems frequently need portable, machine-verifiable answers to questions like:
- Who is this agent (or the organization behind it)?
- What capabilities is it authorized to exercise (and under what limits)?
- Can a verifier validate those claims offline/online and check revocation status?

VCs provide a standards-based vocabulary and proof model for these flows, and are often paired with **Decentralized Identifiers (DIDs)** and **digital wallets**.

## References
- W3C: *Verifiable Credentials Overview* (roadmap and how the specs fit together): https://w3c.github.io/vc-overview/
- W3C VC Working Group: *Verifiable Credentials 2.0 press release* (Recommendation status announcement): https://www.w3.org/press-releases/2025/verifiable-credentials-2-0/
