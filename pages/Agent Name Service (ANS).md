# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**. ANS is specified as an IETF Internet-Draft (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Seed terms

- agent discovery
- registry record
- capability-aware resolution
- Public Key Infrastructure (PKI)
- X.509 certificates
- registration and renewal
- protocol adapter layer
- DNS-based service discovery (DNS-SD)

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include identity, endpoints, and capability metadata, alongside material used to support authenticated resolution. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Overview (per the Internet-Draft)

At a high level, the ANS specification describes:

- A **protocol-agnostic registry mechanism** for secure discovery of agents. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A structured, extensible way to represent agent metadata (the draft describes using **JSON Schema** for structured communication). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Registration and renewal** mechanisms intended to support lifecycle management of registry entries. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A trust model that leverages **Public Key Infrastructure (PKI)** certificates for verifiable identity binding. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A modular **Protocol Adapter Layer** intended to map the protocol-agnostic record into protocol-specific representations (the draft mentions A2A, MCP, ACP as examples). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Architecture and roles (draft)

The draft describes a registry architecture with roles such as:

- **Requesting agent / operator**: submits registration and renewal requests.
- **Agent registry**: stores records (identity, capabilities, endpoints, and related metadata).
- **Registration authority (RA)**: validates registration/renewal requests and enforces registry policy (positioned as part of a PKI-based trust model). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Certificate authority (CA)**: issues and manages certificates used in the PKI trust model.

Background on X.509 PKI profiles: https://datatracker.ietf.org/doc/html/rfc5280

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD).

- **DNS-SD** specifies how DNS resource records can be named and structured to facilitate service discovery using standard DNS queries. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Security considerations (draft)

The ANS draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Status and scope

- ANS is specified as an **Internet-Draft** (work in progress), which may change, be replaced, or expire; treat details as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## References

- IETF Internet-Draft: Agent Name Service (ANS) (draft-narajala-ans-00). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- DNS (RFC 1035). https://datatracker.ietf.org/doc/html/rfc1035
- X.509 PKI profile (RFC 5280). https://datatracker.ietf.org/doc/html/rfc5280
- DNS-Based Service Discovery (RFC 6763). https://datatracker.ietf.org/doc/html/rfc6763
- ANS paper (arXiv:2505.10609). https://arxiv.org/html/2505.10609v1
