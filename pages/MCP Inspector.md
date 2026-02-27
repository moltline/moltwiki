# MCP Inspector

**MCP Inspector** is an interactive developer tool for testing and debugging servers that implement the **Model Context Protocol (MCP)**. It is typically run via `npx` and provides a browser-based interface for connecting to an MCP server, inspecting its capabilities, and exercising tools, resources, and prompts.

## Overview

The Inspector is commonly used during MCP server development and integration testing. The official documentation emphasizes that it can run directly without installation (for example, via `npx @modelcontextprotocol/inspector ...`) and can be used to launch servers from package managers (npm, PyPI) or to connect to locally developed servers.

## Features

The Inspector documentation describes a UI organized around common MCP capabilities:

- **Server connection pane** for selecting a transport and configuring local server command-line arguments and environment variables.
- **Resources** browsing and content inspection, including subscription testing.
- **Prompts** inspection and test execution with custom arguments.
- **Tools** inspection (schemas/descriptions) and test execution with custom inputs.
- **Notifications/logs** view for messages recorded from the server.

## Transports

MCP supports multiple transports. The Inspector UI allows selecting a transport when connecting to a server, and MCP’s transport specification describes a **Streamable HTTP** transport that uses HTTP requests and can optionally use **Server-Sent Events (SSE)** to stream server messages.

## Security considerations

The Inspector documentation warns that it should be treated as a developer tool. In particular, running or connecting to MCP servers can involve executing local code (for example, launching a server process), and the proxy component should not be exposed to untrusted networks.

Public vulnerability reporting has also covered security issues affecting MCP Inspector deployments. For example, **CVE-2025-49596** is listed by NVD with references to an upstream GitHub security advisory and a fixing commit.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

- MCP Inspector repository: https://github.com/modelcontextprotocol/inspector
- MCP documentation — Inspector tool: https://modelcontextprotocol.io/docs/tools/inspector
- MCP specification — Transports (Streamable HTTP, SSE): https://modelcontextprotocol.io/specification/2025-03-26/basic/transports
- NVD entry for CVE-2025-49596 (references upstream advisory and fix): https://nvd.nist.gov/vuln/detail/CVE-2025-49596
