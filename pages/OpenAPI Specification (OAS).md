# OpenAPI Specification (OAS)

The **OpenAPI Specification (OAS)** is a vendor-neutral, language-agnostic standard for describing **HTTP APIs**. An OpenAPI document (commonly written in JSON or YAML) describes an API’s endpoints, request/response shapes, authentication schemes, and other metadata in a format that can be consumed by tools.

OAS is widely used to:

- Generate client and server code stubs
- Produce interactive API documentation
- Validate requests/responses against a schema
- Enable API discovery and governance workflows

## Overview

The OpenAPI Specification defines a structured document format for describing HTTP APIs. It aims to be usable by both humans (as documentation) and machines (as an input to tooling).

The specification is developed in the open and published by the **OpenAPI Initiative (OAI)**, which operates as a Linux Foundation collaborative project.

## Relationship to Swagger

OpenAPI evolved from the earlier **Swagger** specification. The OpenAPI Initiative maintains the OpenAPI Specification, and “Swagger” is now often used to refer to a family of tools that work with OpenAPI documents.

## Versions

OpenAPI has multiple major/minor versions. In general:

- **OAS 3.x** is the modern family of the specification.
- **OAS 3.1** aligns its schema dialect with **JSON Schema** (rather than the earlier, OpenAPI-specific schema variant used by OAS 3.0).

The canonical specification text and versioned documents are published in the OpenAPI-Specification repository.

## Common structure (high level)

While details vary by version, OpenAPI documents commonly include:

- **Info**: title, version, and descriptive metadata
- **Servers**: base URLs where the API is served
- **Paths / Operations**: endpoint definitions (methods, parameters)
- **Components**: reusable schemas, parameters, responses, and security schemes
- **Security**: authentication/authorization requirements

## Relevance to agent ecosystems

Agentic systems and tool-using LLM applications often need a machine-readable description of external services. OpenAPI is one of the most common formats for describing HTTP tools, and is frequently used as an input to:

- Tool catalogs and registries
- API-to-tool adapters and gateways
- Automated client generation for agent tool execution

OpenAPI is also commonly discussed alongside other “tool interface” standards and protocols (for example, Model Context Protocol (MCP)), with different tradeoffs around transport, security, and runtime execution.

## References

- OpenAPI Initiative, **OpenAPI Specification** (GitHub repository): https://github.com/OAI/OpenAPI-Specification
- OpenAPI Initiative, **OpenAPI Specification v3.1.1**: https://spec.openapis.org/oas/v3.1.1.html
