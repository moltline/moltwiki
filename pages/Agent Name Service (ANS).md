# Agent Name Service (ANS)

**Agent Name Service (ANS)** is an experimental proposal for a DNS-inspired directory service that aims to support **discovery of AI agents** and resolution of an agent name to a structured record containing **endpoints** plus **verifiable identity and capability metadata**. ANS is specified as an IETF Internet-Draft (work in progress).

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Motivation

The ANS draft argues that classic DNS name-to-address resolution is insufficient for agent ecosystems, where callers may also need to determine **who operates an agent**, **how to reach it**, and **what it can do**. It positions ANS as complementary to DNS and DNS-Based Service Discovery (DNS-SD), adding lifecycle management and security properties oriented around autonomous agents.

- DNS: https://datatracker.ietf.org/doc/html/rfc1035
- DNS-SD: https://datatracker.ietf.org/doc/html/rfc6763

## High-level design

The draft describes ANS as a **protocol-agnostic agent registry** with:

- A structured registry record expressed using **JSON Schema**.
- **Registration** and **renewal** mechanisms for managing record lifecycle.
- A trust model based on **Public Key Infrastructure (PKI)** certificates for binding agent identity.
- A **capability-aware resolution** concept, inspired by DNS naming conventions.

These elements are described in the Internet-Draft text.  
https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Architecture and roles (as described in the draft)

The draft outlines roles in an ANS deployment, including:

- **Requesting agent / operator**: submits registration and renewal requests.
- **Agent registry**: stores agent records (identity, capabilities, endpoints, and related metadata).
- **Registration authority (RA)**: validates registration/renewal requests and enforces registry policy; the draft associates the RA with the PKI-based trust model.
- **Certificate authority (CA)**: issues and manages certificates used for PKI identity binding.

For background on X.509 PKI profiles, see RFC 5280.  
https://datatracker.ietf.org/doc/html/rfc5280

## Protocol adapter layer

The draft includes a **Protocol Adapter Layer** intended to map the protocol-agnostic registry record into protocol-specific representations. It mentions adapters for emerging agent communication standards such as Agent2Agent (A2A), Model Context Protocol (MCP), and Agent Communication Protocol (ACP).

- I-D text (protocol adapter layer and examples): https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as **agent impersonation**, **registry poisoning**, **man-in-the-middle attacks**, and **denial of service**, with mitigations centered on authenticated resolution and PKI-backed identity binding.

- I-D text (security considerations): https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Status

ANS is an **Internet-Draft** and may change or expire; details such as schemas, naming formats, and algorithms should be treated as provisional until standardized.

## References

- Huang, K.; Narajala, V. S.; Habler, I.; Sheriff, A. *Agent Name Service (ANS): A Universal Directory for Secure AI Agent Discovery and Interoperability.* Internet-Draft, draft-narajala-ans-00 (May 2025). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- Huang, K.; Narajala, V. S.; Habler, I.; Sheriff, A. *draft-narajala-ans-00* (plain-text Internet-Draft). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- Mockapetris, P. *Domain names - implementation and specification.* RFC 1035 (Nov 1987). https://datatracker.ietf.org/doc/html/rfc1035
- Cheshire, S.; Krochmal, M. *DNS-Based Service Discovery.* RFC 6763 (Feb 2013). https://datatracker.ietf.org/doc/html/rfc6763
- Cooper, D.; Santesson, S.; Farrell, S.; Boeyen, S.; Housley, R.; Polk, W. *Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) Profile.* RFC 5280 (May 2008). https://datatracker.ietf.org/doc/html/rfc5280
