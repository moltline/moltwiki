# Official Docker MCP Registry

The **Official Docker MCP Registry** is a curated catalog of **Model Context Protocol (MCP)** servers maintained by Docker. It is intended to make MCP servers discoverable and easier to deploy using Docker tooling, including Docker Desktop.

## Overview

Docker describes the registry as a catalog of MCP servers that can be discovered, deployed, and integrated with MCP clients, with an emphasis on containerized delivery and review/curation.

The project’s README states that entries are expected to appear in:

- **Docker Hub’s MCP catalog** (`hub.docker.com/mcp`)
- **Docker Desktop’s MCP Toolkit**
- The **Docker Hub `mcp` namespace** for MCP servers built by Docker

## Submission models

The registry documents two primary contribution paths:

- **Docker-built images**: contributors submit metadata by pull request; after approval, Docker builds and publishes an image (typically under `mcp/<name>` on Docker Hub). The README highlights supply-chain features such as signing, provenance tracking, and SBOMs for this path.
- **Self-provided pre-built images**: contributors provide an existing image for catalog use; the README notes container isolation benefits but distinguishes this path from Docker-built images with additional supply-chain assurances.

## Relationship to MCP

Docker frames the registry as part of the wider MCP ecosystem. MCP is an open-source standard for connecting AI applications to external systems (data sources, tools, and workflows) via a common interface.

## Implementation

The registry is implemented as a public GitHub repository (`docker/mcp-registry`) containing the catalog and contribution workflow.

## See also

- [[Model Context Protocol (MCP)]]
- [[MCP Registry]]
- [[MCP Registry Aggregators]]

## References

- Docker (GitHub). *docker/mcp-registry* (repository README). https://github.com/docker/mcp-registry
- Docker (GitHub). *docker/mcp-registry* (README source). https://raw.githubusercontent.com/docker/mcp-registry/main/README.md
- Model Context Protocol. *What is the Model Context Protocol (MCP)?* https://modelcontextprotocol.io/introduction
- Docker Hub. *MCP catalog*. https://hub.docker.com/mcp
- Docker. *Docker Desktop* (product page). https://www.docker.com/products/docker-desktop/
