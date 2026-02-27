# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**.

ANS is specified as an IETF Internet-Draft (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://www.rfc-editor.org/rfc/rfc1035.html

## Overview

At a high level, ANS proposes:

- A **protocol-agnostic registry record** (described using JSON Schema) that can carry agent metadata and be extended for different agent protocols. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Registration and renewal** mechanisms for lifecycle management of entries. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A trust model that uses **Public Key Infrastructure (PKI)** and certificates for verifiable agent identity. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A modular **Protocol Adapter Layer** that maps the protocol-agnostic registry record into protocol-specific representations (the draft mentions A2A, MCP, ACP as examples). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Key concepts (draft)

### Registry record

ANS centers on a registry entry that is intended to be:

- **Protocol-agnostic**: a single, canonical record format that can describe an agent independent of how it is contacted.
- **Extensible**: protocol-specific data is attached via extensions rather than redefining the whole record per protocol.

In practice, the draft describes structured request/response messages and record schemas using JSON Schema. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

### Naming and resolution

Like DNS, ANS uses a name-resolution flow: a requester submits a name, and receives a record.

Unlike DNS, the resolved record is meant to include **identity and capability** information in addition to endpoints. The draft also describes **capability-aware resolution** as a goal (i.e., selecting a record or endpoint based on requested capabilities). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

### Lifecycle management

The draft explicitly includes **registration** and **renewal** so entries can be created, updated, and periodically revalidated over time. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Architecture and roles (draft)

The draft describes a registry architecture with roles such as:

- **Requesting agent / operator**: submits registration and renewal requests.
- **Agent registry**: stores records (identity, capabilities, endpoints, and related metadata).
- **Registration authority (RA)**: validates registration/renewal requests and enforces registry policy; the draft positions the RA as interacting with a certificate authority as part of the PKI-based trust model. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Certificate authority (CA)**: issues and manages certificates used in the PKI trust model.

Background on X.509 PKI profiles: https://datatracker.ietf.org/doc/html/rfc5280

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain. https://www.rfc-editor.org/rfc/rfc6763.html
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
