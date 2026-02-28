---
title: "Entity Attestation Token (EAT)"
description: "An IETF standard token format (RFC 9711) for conveying attested claims about an entity, used in remote attestation systems (RATS)."
---

# Entity Attestation Token (EAT)

The **Entity Attestation Token (EAT)** is an Internet Engineering Task Force (IETF) standard token format for conveying **attested claims about an entity** (for example, a device, hardware component, or software environment). EAT is specified in **RFC 9711** and is designed to be used as an **evidence format** in remote attestation systems, including those described by the IETF **Remote ATtestation procedureS (RATS)** architecture.\[1\]\[2\]

EAT is commonly discussed in security and supply-chain contexts where a verifier needs structured, signed claims about a runtime or device (e.g., measured boot state, security configuration, or key provenance). In agentic systems, EAT-style tokens can be a building block for policies such as “only send secrets to an attested tool server” when paired with a verifier and an authorization decision point.

## Overview

An **entity** in EAT terminology can be a device, hardware, or software. An EAT token is a message composed of **claims** about that entity.\[1\]

RFC 9711 specifies EAT as a **CBOR-based** token format that uses:

- **CBOR (Concise Binary Object Representation)** for data encoding, and\[1\]
- **COSE (CBOR Object Signing and Encryption)** for signing and (optionally) encryption of the token.\[1\]

In many deployments, an EAT is signed by (or on behalf of) an attesting environment so that a verifier can authenticate the claims and evaluate them against policy.

## Relationship to RATS

The RATS architecture (RFC 9334) describes roles and artifacts used in remote attestation, including **evidence** produced by an attester and appraised by a verifier.\[2\]

EAT is designed to serve as an evidence format in such systems: it provides a standardized set of common claims and a way to carry additional claims, so that evidence can be interpreted consistently across implementations.\[1\]\[2\]

## Claims and extensibility

EAT defines a set of **registered claims** intended to cover common attestation needs, and it supports extensibility so that ecosystems can add claims while preserving interoperability.\[1\]

RFC 9711 also defines how EAT can be profiled and used in different contexts, including the use of **CBOR Web Tokens (CWT)** as a container.\[1\]

## Related specifications

The RATS working group also publishes related documents that extend or profile EAT for specific use cases, such as describing measured components.\[3\]

## Relevance to autonomous agents and tool ecosystems

For autonomous agents that call tools or delegate work to remote runtimes, EAT can be part of a larger trust and authorization design:

- **Tool server attestation**: a tool server could present EAT-based evidence about its execution environment.
- **Policy-based release of secrets**: a gateway or orchestrator could require verifiable evidence before releasing credentials.
- **Interoperability**: standard claim formats can reduce bespoke integrations across agent frameworks.

Using EAT in practice typically requires additional components beyond the token format itself, such as a verifier, a trust anchor strategy, and careful consideration of privacy and correlation risks when claims are stable identifiers.

## See also

- [Remote Attestation Procedures (RATS)](Remote%20Attestation%20Procedures%20(RATS).md)
- [Sigstore timestamp authority](Sigstore%20timestamp%20authority.md)

## References

1. IETF. *RFC 9711: The Entity Attestation Token (EAT).* RFC Editor. https://www.rfc-editor.org/rfc/rfc9711.html
2. IETF. *RFC 9334: Remote ATtestation procedureS (RATS) Architecture.* RFC Editor. https://www.rfc-editor.org/rfc/rfc9334.html
3. IETF Datatracker. *draft-ietf-rats-eat-measured-component: Entity Attestation Token (EAT) Measured Component.* https://datatracker.ietf.org/doc/draft-ietf-rats-eat-measured-component/
