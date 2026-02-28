# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**. ANS is specified as an IETF Internet-Draft (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity and trust**: operator identity bound to cryptographic credentials.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: capability metadata used for *capability-aware* resolution.
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Overview

At a high level, the draft proposes:

- A **protocol-agnostic registry record** described using **JSON Schema**, with extension points for protocol-specific metadata. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Registration and renewal** mechanisms for lifecycle management of entries. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A trust model that uses **Public Key Infrastructure (PKI)** and **X.509 certificates** for verifiable agent identity. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A modular **Protocol Adapter Layer** that maps the protocol-agnostic registry record into protocol-specific representations (the draft mentions A2A, MCP, ACP as examples). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Architecture and roles (draft)

The draft describes a registry architecture with roles such as:

- **Requesting agent**: the entity initiating registration or renewal.
- **Agent registry**: the database storing agent records (including identity-related material and protocol-specific metadata via extensions). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Registration authority (RA)**: verifies registration/renewal requests, enforces policy, and may interact with a certificate authority as part of the PKI-based trust model. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Certificate authority (CA)**: issues and manages X.509 certificates used in the PKI trust model. https://datatracker.ietf.org/doc/html/rfc5280

## Naming and resolution (draft)

ANS adopts DNS-like naming ideas but targets *agent discovery* rather than name-to-address mapping alone. The draft describes:

- **DNS-inspired naming conventions** intended to support scalable, human-readable identifiers.
- A **resolution process** that can incorporate capability constraints (“capability-aware resolution”). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A **formal resolution algorithm** and a discussion of secure resolution implementation considerations. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

Background on X.509 PKI profiles: https://datatracker.ietf.org/doc/html/rfc5280

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
