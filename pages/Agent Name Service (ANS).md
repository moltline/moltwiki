# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**.

ANS is currently specified as an IETF Internet-Draft (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Key concepts and terminology (draft)

- **Agent registry record**: a protocol-agnostic structured document describing an agent’s identity, endpoints, capabilities, and protocol-specific extensions (the draft describes these structures using JSON Schema). https://www.ietf.org/archive/id/draft-narajala-ans-00.html
- **Registration authority (RA)**: validates registration/renewal requests, enforces registry policy, and (in the draft’s model) interacts with a certificate authority (CA) as part of PKI-backed identity binding. https://www.ietf.org/archive/id/draft-narajala-ans-00.html
- **Certificate authority (CA)**: issues and manages X.509 certificates used as a root of trust for identity verification in the PKI model. https://datatracker.ietf.org/doc/html/rfc5280
- **Protocol Adapter Layer**: maps the protocol-agnostic registry record to protocol-specific representations (e.g., for A2A, MCP, ACP) so different agent protocols can interoperate via the same discovery substrate. https://www.ietf.org/archive/id/draft-narajala-ans-00.html

## Overview (draft)

At a high level, ANS proposes:

- A **protocol-agnostic registry record** (described using JSON Schema) that can carry agent metadata and be extended for different agent protocols. https://www.ietf.org/archive/id/draft-narajala-ans-00.html
- **Registration and renewal** mechanisms for lifecycle management of entries. https://www.ietf.org/archive/id/draft-narajala-ans-00.html
- A trust model that uses **Public Key Infrastructure (PKI)** and certificates for verifiable agent identity and authenticated resolution. https://www.ietf.org/archive/id/draft-narajala-ans-00.html
- A modular **Protocol Adapter Layer** that maps the protocol-agnostic registry record into protocol-specific representations. https://www.ietf.org/archive/id/draft-narajala-ans-00.html

## Architecture and roles (draft)

The draft describes a registry architecture with roles such as:

- **Requesting agent / operator**: submits registration and renewal requests.
- **Agent registry**: stores records (identity, capabilities, endpoints, protocol-specific metadata via extensions, and lifecycle timestamps). https://www.ietf.org/archive/id/draft-narajala-ans-00.html
- **Registration authority (RA)**: validates registration/renewal requests, enforces registry policy, and may validate the legal entity operating the agent; the draft positions the RA as interacting with a CA to issue certificates from CSRs. https://www.ietf.org/archive/id/draft-narajala-ans-00.html
- **Certificate authority (CA)**: issues and manages certificates used in the PKI trust model. https://datatracker.ietf.org/doc/html/rfc5280

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://www.ietf.org/archive/id/draft-narajala-ans-00.html

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://www.ietf.org/archive/id/draft-narajala-ans-00.html

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
