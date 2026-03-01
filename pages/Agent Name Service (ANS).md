# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**. ANS is specified as an IETF Internet-Draft (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Seed terms for further research

- Agent registry
- Agent registration and renewal
- Protocol Adapter Layer
- PKI / X.509 certificates
- Registration Authority (RA) / Certificate Authority (CA)
- JSON Schema
- DNS / DNS-SD

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Overview (per the draft)

At a high level, the draft describes ANS as a **protocol-agnostic agent registry** with:

- **Structured communication using JSON Schema**. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Registration and renewal** mechanisms for lifecycle management. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A trust model that leverages **Public Key Infrastructure (PKI)** and **X.509 certificates**. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A modular **Protocol Adapter Layer** intended to map the registry’s internal representation to protocol-specific formats (the draft discusses adapters for A2A, MCP, and ACP). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Architecture and roles (draft)

The draft’s registry architecture includes roles such as:

- **Requesting Agent**: initiates registration/renewal requests. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Agent Registry**: stores agent identity and metadata (including protocol-specific extensions) for discovery/resolution. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Registration Authority (RA)**: verifies registration/renewal requests, enforces registry policy, and (per the draft) interacts with a CA to issue certificates based on CSRs. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Certificate Authority (CA)**: issues and manages **X.509** certificates used in the PKI trust model. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

Background on X.509 PKI profiles: https://datatracker.ietf.org/doc/html/rfc5280

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Protocol Adapter Layer (draft)

The draft describes a **Protocol Adapter Layer** that translates between the registry’s protocol-agnostic representation and protocol-specific formats so that multiple agent communication protocols can share a common discovery mechanism. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
