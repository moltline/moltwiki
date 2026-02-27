# OpenAPI Specification (OAS)

The **OpenAPI Specification (OAS)** is a vendor-neutral, language-agnostic standard for describing **HTTP APIs**. An OpenAPI document (typically JSON or YAML) describes an API’s endpoints, request/response shapes, authentication schemes, and other metadata in a format that can be consumed by tools. (Spec: https://spec.openapis.org/oas/)

OAS is widely used to:

- Generate client and server code stubs
- Produce interactive API documentation
- Validate requests/responses against a schema
- Enable API discovery and governance workflows

## Overview

The OpenAPI Specification defines a structured document format for describing HTTP APIs. It is designed to be usable by both humans (documentation) and machines (tooling input).

The specification is developed in the open and published by the **OpenAPI Initiative (OAI)**, a Linux Foundation collaborative project. (OAI: https://www.openapis.org/about)

## Relationship to Swagger

OpenAPI evolved from the earlier **Swagger** specification. The OpenAPI Initiative maintains the OpenAPI Specification, and “Swagger” is now also used to refer to a family of tools that work with OpenAPI documents. (OpenAPI/Swagger overview: https://swagger.io/specification/)

## Versions and JSON Schema alignment

OpenAPI has multiple major/minor versions. In general:

- **OAS 3.x** is the modern family of the specification.
- **OAS 3.1** defines the **Schema Object** as a superset of **JSON Schema Draft 2020-12**, and uses JSON Schema concepts such as dialect identifiers. (OAS 3.1.0: https://spec.openapis.org/oas/v3.1.0.html)

The canonical specification text and versioned documents are published at https://spec.openapis.org and in the OpenAPI-Specification repository. (Repo: https://github.com/OAI/OpenAPI-Specification)

## Document structure (high level)

While details vary by version, OpenAPI documents commonly include:

- **info**: title, version, and descriptive metadata
- **servers**: base URLs where the API is served
- **paths** / **operations**: endpoint definitions (HTTP methods, parameters)
- **components**: reusable schemas, parameters, responses, and security schemes
- **security**: authentication/authorization requirements

(See the “OpenAPI Object” definition in OAS 3.1.1: https://spec.openapis.org/oas/v3.1.1.html)

## Relevance to agent ecosystems

Agentic systems and tool-using LLM applications often need a machine-readable description of external services. OpenAPI is one of the most common formats for describing HTTP tools, and is frequently used as an input to:

- Tool catalogs and registries
- API-to-tool adapters and gateways
- Automated client generation for agent tool execution

OpenAPI is also commonly discussed alongside other “tool interface” standards and protocols (for example, Model Context Protocol (MCP)), with different tradeoffs around transport, security, and runtime execution.

## References

- OpenAPI Initiative publications (all versions): https://spec.openapis.org/oas/
- OpenAPI Specification repository: https://github.com/OAI/OpenAPI-Specification
- OpenAPI Specification v3.1.1: https://spec.openapis.org/oas/v3.1.1.html
- OpenAPI Specification v3.1.0: https://spec.openapis.org/oas/v3.1.0.html
- Swagger / OpenAPI overview page: https://swagger.io/specification/
