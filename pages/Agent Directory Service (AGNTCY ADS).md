# Agent Directory Service (AGNTCY ADS)

The **Agent Directory Service (ADS)** is a distributed directory service for publishing, storing, and discovering metadata about AI agents and multi-agent systems. ADS is developed within the **AGNTCY** project and is described in an Internet-Draft submitted to the IETF.

ADS is designed to support *capability-based discovery* (finding agents by skills), *verifiable claims* (integrity and provenance mechanisms for published records), and *distributed architecture* (discovery across a network of directory servers). The current IETF draft emphasizes use cases such as discovering compatible agents, evaluating performance characteristics (e.g., cost and latency), composing multi-agent workflows, and tracking versioning and dependencies.

## Overview

In ADS, agent metadata is stored as **directory records**. The system interconnects distributed directories through a **content-routing** mechanism that maps skills (from a taxonomy) to record identifiers, and record identifiers to directory servers hosting those records. Both record identifiers and the skill taxonomy are designed to be routable in a **Distributed Hash Table (DHT)**, enabling decentralized discovery.

The ADS Internet-Draft frames ADS as a directory infrastructure for the agentic AI ecosystem, focusing on flexible metadata storage and discovery rather than prescribing a single multi-agent architecture.

## Architecture

### Content-addressed identifiers

ADS uses **Content Identifiers (CIDs)** to name directory records. CIDs are cryptographically derived from record content, providing immutability (content changes produce a new identifier), deduplication (identical content shares an identifier), and verifiability (nodes can check that retrieved content matches its CID).

### Skill taxonomies and discovery

The draft describes a taxonomy-driven approach to capability search, using hierarchical taxonomies to optimize matching and routing. The high-level discovery flow is commonly described as a two-level mapping: skills are mapped to candidate record identifiers (CIDs), and those CIDs are mapped to servers (peers) that can provide the corresponding record artifacts.

### Distributed routing substrate

AGNTCY documentation describes ADS as using a DHT-based approach for content routing and discovery, referencing **libp2p Kademlia DHT** specifications for server and content discovery.

### Storage layer and OCI artifacts

ADS stores and distributes directory records as **OCI artifacts** in **OCI registries**, leveraging existing container-registry ecosystems and tooling. The Internet-Draft notes that building on OCI specifications provides compatibility with deployed authentication/authorization mechanisms and can integrate with signing/verification tooling (e.g., Notary, cosign) and registry distribution infrastructure.

AGNTCY documentation further describes a reference implementation in Go with gRPC/protobuf interfaces, using **ORAS** (OCI Registry As Storage) for record storage and **zot** as a reference OCI registry implementation.

## Standards status

ADS is published as an **Internet-Draft** (work in progress) on the IETF Datatracker:

- *Agent Directory Service*, Internet-Draft: [draft-mp-agntcy-ads](https://datatracker.ietf.org/doc/draft-mp-agntcy-ads/)

## Relationship to other agent ecosystem components

The ADS Internet-Draft situates ADS in the context of multi-agent systems that may use tool-calling infrastructure such as **Model Context Protocol (MCP)** servers. The AGNTCY documentation describes ADS as using the **Open Agentic Schema Framework (OASF)** to model record data, while using skills (from an OASF taxonomy) as the primary input to content routing.

## References

- IETF Datatracker — *Agent Directory Service* (Internet-Draft, work in progress): https://datatracker.ietf.org/doc/draft-mp-agntcy-ads/
- AGNTCY documentation — ADS overview: https://docs.agntcy.org/dir/overview/
- AGNTCY dir-spec preview site (HTML/txt + Datatracker links): https://spec.dir.agntcy.org/
- multiformats — Content Identifiers (CID): https://github.com/multiformats/cid
- libp2p specs — Kademlia DHT: https://github.com/libp2p/specs/tree/master/kad-dht
- ORAS (OCI Registry As Storage): https://oras.land/
- zot OCI registry: https://zotregistry.dev/
