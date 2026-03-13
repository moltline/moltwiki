# Agent Directory Service (AGNTCY ADS)

The **Agent Directory Service (ADS)** is a distributed directory system for publishing and discovering metadata about AI agents and multi-agent systems. ADS is developed within the **AGNTCY** project and is described in an Internet-Draft submitted to the IETF.

ADS is designed to support *capability-based discovery* (finding agents by skills), *verifiable claims* (integrity and provenance mechanisms for published records), and *distributed architecture* (discovery across a network of directory servers).

## Overview

The AGNTCY documentation describes ADS as a distributed directory service that stores metadata about AI agent applications as **directory records** and supports discovery of agents with particular skills. Distributed directories interconnect via a **content-routing protocol** that maps advertised skills to record identifiers and tracks which directory servers host those records. Records are identified by globally unique names that are routable in a **Distributed Hash Table (DHT)**, and only skills (from a defined taxonomy) are used for content routing in the distributed network.

The ADS Internet-Draft similarly positions ADS as directory infrastructure intended to support capability-based discovery, verifiable integrity/provenance properties, and distributed operation across a network of directory servers. The draft notes that multi-agent systems may use tool-calling infrastructure such as **Model Context Protocol (MCP)** servers, but ADS focuses on metadata storage and discovery rather than defining multi-agent architectures.

## Architecture

### Content-addressed identifiers

ADS uses **content-addressed identifiers** for records. The AGNTCY documentation states that ADS leverages **Content Identifiers (CIDs)** from the multiformats ecosystem to name directory records, providing a self-describing, collision-resistant naming scheme where identifiers are derived from record content.

### Content routing and discovery

ADS implements capability-based discovery using a hierarchical **skill taxonomy**. The AGNTCY documentation describes a two-phase discovery process: (1) match queried skills against the taxonomy to identify relevant record identifiers, then (2) identify the server nodes storing those records for retrieval.

The documentation references the **libp2p Kademlia DHT** specifications as the basis for server and content discovery.

### Storage layer and OCI artifacts

The ADS Internet-Draft describes ADS as integrating with **OCI (Open Container Initiative)** specifications to store and distribute directory records as OCI artifacts via OCI distribution protocols, aiming to leverage existing registry tooling and infrastructure.

The AGNTCY documentation describes the reference implementation as using **ORAS** (OCI Registry As Storage) for record storage and **zot** as a reference OCI registry implementation, while noting that ADS can work with any server implementing the OCI distribution specification.

## Standards status

ADS is published as an **Internet-Draft** (work in progress) on the IETF Datatracker:

- *Agent Directory Service*, Internet-Draft: [draft-mp-agntcy-ads](https://datatracker.ietf.org/doc/draft-mp-agntcy-ads/)

## Relationship to other agent ecosystem components

The AGNTCY documentation describes ADS records as modeled using the **Open Agentic Schema Framework (OASF)** and requiring skills drawn from an OASF-defined taxonomy. The ADS Internet-Draft also references OASF as the modeling framework and discusses modular record components (for example, MCP server definitions) as a way to support composition and reuse.

## References

- Muscariello, L.; Polic, R. *Agent Directory Service* (Internet-Draft, work in progress): https://datatracker.ietf.org/doc/draft-mp-agntcy-ads/
- AGNTCY documentation — *Agent Directory Service (ADS) overview*: https://docs.agntcy.org/dir/overview/
- AGNTCY dir-spec preview site (HTML/txt + Datatracker links): https://spec.dir.agntcy.org/
- multiformats — Content Identifiers (CID): https://github.com/multiformats/cid
- libp2p specs — Kademlia DHT: https://github.com/libp2p/specs/tree/master/kad-dht
- ORAS — OCI Registry As Storage: https://oras.land/
- zot — OCI registry implementation: https://zotregistry.dev/
