# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed architecture for discovering AI agents via DNS-inspired names and resolving them to verifiable identity and capability metadata.

ANS is published as an Internet-Draft in the IETF Datatracker (work in progress, subject to change): https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

The ANS draft argues that classic DNS name resolution (mapping names to network locations) is not sufficient for agent ecosystems where a caller often needs, in addition to an address, information about:

- **Identity** (who is this agent / operator?)
- **How to reach it** (endpoints for one or more agent protocols)
- **What it can do** (capabilities / entitlements)
- **How to verify it** (cryptographic credentials)

The design borrows the *naming* intuition from DNS (RFC 1035) while extending the *resolved record* to include richer agent metadata. https://datatracker.ietf.org/doc/html/rfc1035

## Overview (high-level)

The ANS draft proposes an agent directory service intended to support:

- **Discovery**: resolving a human-readable, DNS-like agent name to a structured record describing the agent and its endpoints. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Verifiable identity and trust**: associating registry entries with PKI credentials (e.g., X.509 certificates) to help prevent impersonation and enable authenticated resolution. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Lifecycle management**: registration and renewal mechanisms for maintaining current records over time. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Protocol interoperability**: a *protocol adapter layer* intended to map a common registry record format into protocol-specific metadata for multiple agent protocols (e.g., A2A, MCP, ACP). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Architecture and roles

The draft describes a registry architecture with roles including:

- **Requesting agent** (or operator): submits registration / renewal requests.
- **Agent registry**: stores identity, capability, and protocol endpoint metadata.
- **Registration authority (RA)**: validates registration and renewal requests, enforces registry policy, and interacts with a certificate authority to obtain credentials. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Certificate authority (CA)**: issues and manages X.509 certificates used as part of the trust model. (For background on X.509 PKI profiles, see RFC 5280.) https://datatracker.ietf.org/doc/html/rfc5280
- **Protocol adapter layer**: translates between the registry’s protocol-agnostic record and protocol-specific representations. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Relationship to DNS and DNS-SD

ANS is explicitly “DNS-inspired”, but it is not the same thing as DNS Service Discovery (DNS-SD).

- **DNS-SD** (RFC 6763) describes how to use standard DNS record types and queries to discover named instances of a service type within a domain. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol aimed at agent discovery, where the resolved record includes identity and capability metadata and can be adapted into multiple agent communication protocols. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Security considerations (draft)

The draft’s security considerations discuss threats such as:

- agent impersonation
- registry poisoning
- man-in-the-middle attacks
- denial of service

…and frames mitigations around authenticated resolution and PKI-backed identity binding. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Notes and cautions

- ANS is an **Internet-Draft**: it is not an IETF standard and may change or expire. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- Treat details (schemas, algorithms, naming formats) as provisional until standardized.
