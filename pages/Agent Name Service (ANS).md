# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**. ANS is specified as an IETF Internet-Draft (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Core ideas (from the draft)

The ANS draft describes:

- A **protocol-agnostic registry mechanism** intended to complement (not replace) emerging agent communication protocols. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **PKI-backed identity binding**, using certificates as the basis for verifiable identity and trust. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **Registration and renewal** flows for lifecycle management of registry entries. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- A DNS-inspired **naming and resolution** approach, including **capability-aware resolution**. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- A modular **Protocol Adapter Layer** that maps a protocol-agnostic ANS record into protocol-specific representations (the draft calls out A2A, MCP, ACP as examples). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Terminology (useful mental model)

- **Name resolution**: turning a name into a record a client can use.
- **Directory / registry**: a service that stores records and answers resolution queries.
- **Capability-aware resolution**: selecting or filtering results based on capabilities requested by the caller (e.g., “an agent that supports protocol X” or “has capability Y”), rather than returning only a network location. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **PKI / X.509**: the certificate-based public key infrastructure widely used on the Internet; the common Internet profile is described in RFC 5280. https://datatracker.ietf.org/doc/html/rfc5280

## Architecture and roles (draft)

The draft describes a registry architecture with roles such as:

- **Requesting agent / operator**: submits registration and renewal requests.
- **Agent registry**: stores records (identity, capabilities, endpoints, and related metadata).
- **Registration authority (RA)**: validates registration/renewal requests and enforces registry policy; the draft positions the RA as interacting with a certificate authority as part of the PKI-based trust model. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **Certificate authority (CA)**: issues and manages certificates used in the PKI trust model. https://datatracker.ietf.org/doc/html/rfc5280

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS** is the Internet’s hierarchical naming system; core protocol details are in RFC 1035. https://datatracker.ietf.org/doc/html/rfc1035
- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain (DNS-Based Service Discovery). https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Status and publication

ANS is currently published as an **independent submission Internet-Draft** with intended status **Experimental** (not an IETF standard and subject to change). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

The authors also published a corresponding paper describing ANS on arXiv. https://arxiv.org/abs/2505.10609
