# Agent Directory Service (AGNTCY ADS)

The **Agent Directory Service (ADS)** is a distributed directory system for publishing and discovering metadata about AI agents and multi-agent systems. ADS is developed within the **AGNTCY** project and is described in an Internet-Draft submitted to the IETF.

ADS is designed to support *capability-based discovery* (finding agents by skills), *verifiable claims* (integrity and provenance mechanisms for published records), and *distributed architecture* (discovery across a network of directory servers).

## Overview

According to the AGNTCY documentation, ADS stores agent metadata as **directory records** and interconnects distributed directories using a **content-routing protocol**. Records are identified by globally unique names that are routable in a Distributed Hash Table (DHT), and the system uses a skill taxonomy to map capabilities to record identifiers and to locate servers hosting those records.

The ADS Internet-Draft describes ADS as a directory infrastructure for the agentic AI ecosystem, intended to help developers discover and compose compatible agents and to attach structured metadata (including skills and other attributes) to published agent records.

## Architecture

### Content-addressed identifiers

ADS uses **content-addressed identifiers** for records. The AGNTCY documentation states that ADS leverages **Content Identifiers (CIDs)** (from the multiformats ecosystem) to name directory records, providing a collision-resistant naming scheme where identifiers are derived from record content.

### Distributed discovery

AGNTCY documentation describes ADS as using a DHT-based approach for content routing and discovery. The documentation specifically references **libp2p Kademlia DHT** specifications for server and content discovery.

### Storage layer and OCI artifacts

The AGNTCY documentation and the ADS Internet-Draft describe an architecture that uses **OCI registries** as an object storage and distribution layer. In this model, records are packaged and transferred as OCI artifacts using OCI distribution protocols, enabling interoperability with existing registry tooling.

## Standards status

ADS is published as an **Internet-Draft** (work in progress) on the IETF Datatracker:

- *Agent Directory Service*, Internet-Draft: [draft-mp-agntcy-ads](https://datatracker.ietf.org/doc/draft-mp-agntcy-ads/)

## Relationship to other agent ecosystem components

The ADS Internet-Draft mentions **Model Context Protocol (MCP)** servers as an example of tool-calling infrastructure used in multi-agent systems, and the AGNTCY documentation describes ADS as using the **Open Agentic Schema Framework (OASF)** as a modeling framework for agent record data.

## References

- AGNTCY documentation — Agent Directory overview: https://docs.agntcy.org/dir/overview/
- IETF Datatracker — *Agent Directory Service* (Internet-Draft): https://datatracker.ietf.org/doc/draft-mp-agntcy-ads/
- AGNTCY dir-spec preview site (HTML/txt + Datatracker links): https://spec.dir.agntcy.org/
- multiformats — Content Identifiers (CID): https://github.com/multiformats/cid
- libp2p specs — Kademlia DHT: https://github.com/libp2p/specs/tree/master/kad-dht
