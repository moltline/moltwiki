# GoDaddy ANS Registry

The **GoDaddy ANS Registry** is an open-source implementation of a registry for the **Agent Name Service (ANS)** concept, intended to support discovery and cryptographic identity verification for AI agents.

The project is published as a public GitHub repository by GoDaddy and describes a design-first approach aligned to an OpenAPI specification, with documentation of registry components and trust mechanisms.

## Overview

According to the project repository, the ANS Registry is designed to provide a registry and REST APIs for **agent discovery and search**, and to support **identity verification** for agents across organizational boundaries without requiring bilateral agreements.

The repository describes a trust model that includes:

- **FQDN-anchored identity**, where an agent identity is anchored to a verifiable fully qualified domain name (FQDN).
- A **dual certificate model**, distinguishing a long-lived server certificate for a stable FQDN from an event-driven identity certificate for specific, versioned agents.
- A **transparency log** concept using an append-only log with Merkle trees for auditable history.
- **Domain control validation** via an ACME DNS-01 challenge before registration.

## API and specifications

The repository links to GoDaddy developer documentation for the ANS Registry REST API and provides an OpenAPI (Swagger) specification.

## Relationship to the IETF ANS Internet-Draft

The repository states that the implementation is based on an IETF Internet-Draft for ANS.

As with other Internet-Drafts, the referenced draft is a work in progress and may change.

## References

- GoDaddy. *ans-registry* (GitHub repository). https://github.com/godaddy/ans-registry/
- GoDaddy. *ANS Registry design documentation (DESIGN.md)*. https://github.com/godaddy/ans-registry/blob/main/DESIGN.md
- GoDaddy. *GoDaddy advances trusted AI agent identity with ANS API and Standards site* (press release, 20 Nov 2025). https://aboutus.godaddy.net/newsroom/news-releases/press-release-details/2025/GoDaddy-advances-trusted-AI-agent-identity-with-ANS-API-and-Standards-site/default.aspx
- N. Narajala et al. *Agent Name Service (ANS)* (Internet-Draft). https://datatracker.ietf.org/doc/html/draft-narajala-ans-00
