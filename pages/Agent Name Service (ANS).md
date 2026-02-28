# Agent Name Service (ANS)

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory service for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**.

ANS is specified as an IETF Internet-Draft (work in progress): https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## High-level architecture (draft)

The draft describes a registry architecture with roles such as:

- **Requesting Agent**: the entity initiating registration/renewal (an individual, organization, or automated system). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **Agent Registry**: stores agent records (identity, capabilities, endpoints, timestamps, and protocol-specific extensions). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **Registration Authority (RA)**: verifies registration/renewal requests, enforces registry policies, and (per the draft) interacts with a Certificate Authority to issue certificates based on CSRs; it may also handle lifecycle events like renewal and revocation. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **Certificate Authority (CA)**: issues and manages X.509 certificates used in the PKI trust model. https://datatracker.ietf.org/doc/html/rfc5280

## Protocol-agnostic record + Protocol Adapter Layer

A central idea in ANS is a **protocol-agnostic registry record** (described using JSON Schema) that can carry agent metadata and be extended for different agent protocols. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

To interoperate across different agent ecosystems, the draft defines a modular **Protocol Adapter Layer** that maps the protocol-agnostic record into protocol-specific representations (the draft mentions A2A, MCP, ACP as examples). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

Practical implication: ANS is attempting to be a shared discovery substrate, while leaving the “how do I talk to this agent?” details to the adapter for the protocol you actually intend to use.

## Naming + resolution

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata (not just service endpoints). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

The draft also describes **capability-aware resolution** as part of its naming/resolution approach. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

ANS’s trust model is explicitly PKI-based (X.509). Background on X.509 PKI profiles: https://datatracker.ietf.org/doc/html/rfc5280

## Status / cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
- The ANS draft uses RFC 2119/BCP 14 requirement language (MUST/SHOULD/etc.). Background: https://datatracker.ietf.org/doc/html/rfc2119
