---
title: "Agent Name Service (ANS)"
description: "IETF Internet-Draft proposing a DNS-inspired, PKI-backed directory and resolution protocol for discovering AI agents and their endpoints/capabilities."
---

## What it is

**Agent Name Service (ANS)** is a proposed, DNS-inspired directory and resolution system for **discovering AI agents** and resolving an agent name to a structured record containing **endpoints plus verifiable identity and capability metadata**. It is specified as an IETF **Internet-Draft** (work in progress):

- https://datatracker.ietf.org/doc/html/draft-narajala-ans-00

## What problem ANS is trying to solve

Classic DNS primarily maps names to network locations (e.g., IP addresses). In agent ecosystems, a caller often needs more than “where”; it also needs “who” and “what”. The ANS draft frames discovery as resolving a name to an **agent registry record** that can include:

- **Identity**: who operates the agent and how it is authenticated.
- **Reachability**: one or more protocol endpoints.
- **Capabilities**: what the agent claims it can do (for capability-aware resolution).
- **Verification material**: credentials used to prevent impersonation and support authenticated resolution.

Background on DNS: https://datatracker.ietf.org/doc/html/rfc1035

## Overview (draft)

At a high level, the draft describes ANS as a protocol-agnostic registry mechanism that:

- Uses **PKI certificates** for verifiable agent identity and trust. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- Defines **registration and renewal** mechanisms for lifecycle management. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- Uses DNS-inspired naming conventions and discusses **capability-aware resolution**. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- Specifies structured interactions using **JSON Schema**. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- Includes a modular **Protocol Adapter Layer** intended to support multiple agent communication standards (the draft mentions A2A, MCP, ACP, etc.). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Architecture and roles (draft)

The draft’s architecture includes:

- **Requesting agent**: submits registration/renewal requests.
- **Agent registry**: stores agent identity, capabilities, protocol-specific metadata, and lifecycle timestamps. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **Registration authority (RA)**: verifies registration/renewal requests and enforces registry policy; the draft describes the RA as interacting with a certificate authority as part of the PKI model. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt
- **Certificate authority (CA)**: issues and manages X.509 certificates used in the PKI trust model. https://datatracker.ietf.org/doc/html/rfc5280
- **Protocol Adapter Layer**: translates between the registry’s internal representation and protocol-specific formats. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Relationship to DNS and DNS-SD

ANS is “DNS-inspired”, but it is not simply DNS Service Discovery (DNS-SD):

- **DNS-SD** defines how to use DNS record types and queries to discover named instances of a service type within a domain. https://datatracker.ietf.org/doc/html/rfc6763
- **ANS** proposes a separate registry and resolution protocol oriented around agent discovery, where the resolved record can include identity and capability metadata and can be adapted to multiple agent communication protocols. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Protocol Adapter Layer (what it’s for)

A key design element in the draft is a **Protocol Adapter Layer** that maps between:

- a **protocol-agnostic** registry record (the draft describes structured communication using JSON Schema), and
- **protocol-specific** representations for different agent ecosystems.

The draft gives an illustrative example where an MCP tool description could be stored as protocol-specific extension data, with elements of the agent name encoding protocol and capability (example shown in the draft). https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Security considerations (draft)

The draft includes a threat analysis and discusses risks such as impersonation, registry poisoning, man-in-the-middle attacks, and denial of service, with mitigations centered on authenticated resolution and PKI-backed identity binding. https://www.ietf.org/archive/id/draft-narajala-ans-00.txt

## Notes and cautions

- ANS is an **Internet-Draft** and may change or expire; treat details (schemas, algorithms, naming formats) as provisional until standardized. https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
