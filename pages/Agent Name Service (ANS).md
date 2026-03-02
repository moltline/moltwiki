# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**. ANS is specified as an IETF Internet-Draft (work in progress):

- https://datatracker.ietf.org/doc/draft-narajala-ans/
- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Overview (per the Internet-Draft)

At a high level, ANS proposes:

- A **protocol-agnostic registry mechanism** for agent discovery that uses **structured communication via JSON Schema**. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Agent registration and renewal** mechanisms for lifecycle management. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- A trust model that integrates **Public Key Infrastructure (PKI)** and **X.509 certificates** for verifiable agent identity. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00 and https://datatracker.ietf.org/doc/html/rfc5280
- A modular **Protocol Adapter Layer** intended to translate the protocol-agnostic registry record into protocol-specific representations (the draft mentions A2A, MCP, ACP as examples). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Architecture and roles (draft)

The draft describes a registry architecture with roles such as:

- **Requesting agent**: the entity initiating registration/renewal. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Agent registry**: a database for storing agent metadata including capabilities and certificates. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Registration authority (RA)**: verifies registration/renewal requests, enforces registry policy, and (per the draft) interacts with a CA to issue certificates based on CSRs; it also manages lifecycle actions such as renewal and revocation. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- **Certificate authority (CA)**: issues and manages X.509 certificates used as part of the trust model. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00 and https://datatracker.ietf.org/doc/html/rfc5280

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** specifies how DNS records are named/structured so clients can discover instances of a service type in a domain using standard DNS queries. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## Implementations and related work

- GoDaddy has published a proof-of-concept description of an “enhanced ANS Registry” design that builds on the ANS Internet-Draft and integrates DNS/PKI operational flows (e.g., domain-control validation and certificate issuance) for agent registration. https://www.godaddy.com/resources/news/building-trust-at-internet-scale-godaddys-agent-name-service-registry-for-the-agentic-ai-marketplace

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/draft-narajala-ans/
