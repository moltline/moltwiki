---
title: "Entity Attestation Token (EAT) (RFC 9711)"
description: "IETF standard token format for conveying attested claims about a device or workload, used as evidence in RATS-style remote attestation."
---

# Entity Attestation Token (EAT) (RFC 9711)

An **Entity Attestation Token (EAT)** is an IETF-standard format for conveying an **attested claims set** about an entity (for example, a device, embedded system, or workload) in a way that can be used as **evidence** in **remote attestation** systems.[^rfc9711]

EAT is designed to be usable across different deployment environments and security technologies (including TEEs and measured boot), and to be carried in different cryptographic envelope formats (for example, CBOR-based tokens).[^rfc9711]

## Purpose

Remote attestation systems typically need a portable way for an **attester** to present claims about its identity and state (software, firmware, configuration, or hardware characteristics) to a **verifier**.

RFC 9711 defines EAT as a structured claims set intended to:

- Represent attestation claims in a standardized way.
- Support common attestation patterns, including device identity and measurements.
- Enable interoperability between different attestation technologies and protocols.[^rfc9711]

## Relationship to RATS

EAT is commonly discussed in the context of the IETF **Remote ATtestation procedureS (RATS)** architecture, where:

- An **attester** produces **evidence**.
- A **verifier** appraises that evidence.
- A **relying party** consumes an **attestation result** to make an authorization or policy decision.[^rfc9334]

In many RATS-style designs, an EAT (or an EAT-like claims set carried in some signed/encrypted token) is the evidence object that travels from attester to verifier.

## Token formats and envelopes

RFC 9711 specifies the EAT claims set independently of any single on-the-wire encoding, but it is closely associated with CBOR/COSE ecosystems.

In practice, EAT claims are often carried in:

- **CBOR Web Token (CWT)** / **COSE**-protected structures (common in constrained and embedded environments).
- Other signed token envelopes that can convey a claims set with integrity protection.

(Exact transport and envelope choices are deployment-specific; the core contribution of EAT is the standardized claims vocabulary and structure.)[^rfc9711]

## Common claim categories

EAT is intended to describe both **identity** and **state** characteristics. Examples of claim categories discussed in RFC 9711 include:

- **Security level / debug state** indicators.
- **Hardware and firmware identifiers**.
- **Software measurements** and boot state.
- **Nonce / freshness**-related inputs, depending on the protocol that conveys the token.[^rfc9711]

## Relevance to agentic systems

In agentic and tool-using systems, remote attestation is sometimes proposed as an additional control for deciding whether to:

- release secrets or credentials to a tool server,
- accept tool outputs as coming from an approved execution environment,
- or enforce policies like “only call tools running in an attested runtime.”

In such designs, an EAT-like evidence token can provide a standardized container for the attester’s claims, while authorization decisions remain with the verifier/relying-party policy logic.

## See also

- [Remote Attestation Procedures (RATS)](Remote%20Attestation%20Procedures%20(RATS).md)
- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

[^rfc9711]: IETF. *RFC 9711: The Entity Attestation Token (EAT).* RFC Editor. https://www.rfc-editor.org/rfc/rfc9711.html
[^rfc9334]: IETF. *RFC 9334: Remote ATtestation procedureS (RATS) Architecture.* RFC Editor. https://www.rfc-editor.org/rfc/rfc9334.html
