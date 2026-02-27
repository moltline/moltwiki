# GitHub MCP Registry

The **GitHub MCP Registry** is a registry mechanism supported by GitHub Copilot and related developer tooling for discovering and governing **Model Context Protocol (MCP)** servers within an organization or enterprise. GitHub’s documentation describes an MCP registry as a set of HTTPS endpoints that return metadata about MCP servers and their versions, enabling controlled distribution and allowlisting of remote and local MCP servers in a company environment.[^github-docs-configure]

GitHub also participates in the open-source **MCP Registry** project (hosted under the *modelcontextprotocol* organization), which provides a community-driven registry service and reference implementation for MCP server publication and discovery.[^mcp-registry-repo]

## Overview

An MCP registry functions as a catalog of MCP servers, allowing MCP clients (including IDE integrations) to retrieve a list of available servers and details required to connect to them.[^github-docs-configure] GitHub’s guidance emphasizes that organizations can self-host a registry by forking the open-source MCP Registry project, run it locally (for example using Docker), or implement a compatible custom registry.[^github-docs-configure]

## Specification and endpoints

GitHub’s documentation states that a registry reachable by GitHub Copilot must follow the **v0.1 MCP registry specification** and support URL routing for a small set of endpoints:[^github-docs-configure]

- `GET /v0.1/servers` — returns a list of all included MCP servers
- `GET /v0.1/servers/{serverName}/versions/latest` — returns the latest version of a specific server
- `GET /v0.1/servers/{serverName}/versions/{version}` — returns details for a specific server version

GitHub further notes that the earlier “v0” specification is considered unstable and should not be implemented, recommending v0.1 instead.[^github-docs-configure]

## Governance and security controls

### Allowlisting and local servers

GitHub documentation indicates that if developers need access to **local MCP servers**, those servers can be included in the registry using the correct server identifier, and that allowlist enforcement is part of the governance model.[^github-docs-configure]

### CORS requirements

For GitHub Copilot to fetch registry data cross-origin, GitHub requires registries (or their reverse proxies) to include Cross-Origin Resource Sharing (CORS) headers on `/v0.1/servers` endpoints, including `Access-Control-Allow-Origin: *` and allowing `GET, OPTIONS` methods.[^github-docs-configure]

## Reference implementation

The open-source MCP Registry repository describes itself as providing MCP clients with a list of MCP servers “like an app store for MCP servers,” and documents development status and publishing workflows, including a CLI tool for publishing servers.[^mcp-registry-repo]

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)
- [MCP Registry](MCP%20Registry.md)

## References

[^github-docs-configure]: GitHub Docs. *Configure an MCP registry for your organization or enterprise*. https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-mcp-usage/configure-mcp-registry (accessed 2026-02-27).

[^mcp-registry-repo]: GitHub. *modelcontextprotocol/registry: A community driven registry service for Model Context Protocol (MCP) servers*. https://github.com/modelcontextprotocol/registry (accessed 2026-02-27).
