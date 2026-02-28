# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**.

ANS is currently specified as an **IETF Internet-Draft** (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Core concepts (as described in the draft)

### Agent registry record

ANS centers on a **protocol-agnostic record** describing an agent, intended to be machine-validated using **JSON Schema**. The draft positions this record as the registry’s canonical representation, with protocol-specific views derived via adapters.

Draft: https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

### Registration and renewal (lifecycle)

The draft includes a **registration and renewal mechanism** so entries can be created, updated, and kept fresh over time (rather than being “set and forget”).

Draft: https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

### PKI-backed identity

The draft’s trust model uses **Public Key Infrastructure (PKI)** with **X.509 certificates** to bind an agent’s registry entry to a verifiable identity.

- Draft: https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- X.509/PKI profile background: https://datatracker.ietf.org/doc/html/rfc5280

### Protocol Adapter Layer

ANS explicitly separates:

- a **protocol-agnostic** registry record, and
- **protocol-specific** representations for concrete agent protocols.

A **Protocol Adapter Layer** is described as the translation boundary between these worlds (the draft mentions A2A, MCP, ACP as examples).

Draft (Protocol Adapter Layer): https://datatracker.ietf.org/doc/html/draft-narajala-ans-00#section-5

## Architecture and roles (draft)

The draft describes a registry architecture with roles such as:

- **Requesting agent / operator**: submits registration and renewal requests.
- **Agent registry**: stores agent records (including identity material and metadata).
- **Registration authority (RA)**: verifies registration/renewal requests and enforces registry policy; the draft describes the RA as interacting with a certificate authority as part of the PKI-based trust model. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00#section-3
- **Certificate authority (CA)**: issues and manages certificates used in the PKI trust model. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00#section-3

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata beyond classic DNS name→address mapping. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding.

Draft (Security Considerations): https://datatracker.ietf.org/doc/html/draft-narajala-ans-00#section-6

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
