# MCP Inspector

**MCP Inspector** is a developer tool for testing and debugging servers that implement the **Model Context Protocol (MCP)**. It provides a browser-based user interface and a companion proxy process that connects to MCP servers using multiple transport mechanisms.

## Overview

The MCP Inspector project describes two main components:

- **MCP Inspector Client (MCPI)**: a web user interface for interactively connecting to an MCP server, inspecting available tools and schemas, and running test calls.
- **MCP Proxy (MCPP)**: a Node.js process that bridges the browser UI to MCP servers (for example, by launching a local MCP server process and communicating over *stdio*, or by connecting over network transports such as *SSE* or *streamable HTTP*).

Because the proxy can spawn local processes and connect to configured endpoints, the Inspector is typically run as a local developer tool rather than as a publicly exposed service.

## Architecture

The Inspector’s architecture is commonly summarized as:

1. The **browser UI** talks HTTP to the **proxy**.
2. The **proxy** acts as an **MCP client** to the target MCP server.
3. The proxy supports multiple MCP transports (the project documentation mentions *stdio*, *SSE*, and *streamable HTTP*).

## Security considerations

The project documentation warns that the proxy component should not be exposed to untrusted networks, because it can spawn local processes and connect to arbitrary MCP servers as configured by the user.

In addition, public vulnerability reporting has covered security issues affecting the MCP Inspector. For example, **CVE-2025-49596** is listed by NVD with references to the upstream GitHub security advisory and a fixing commit.

## See also

- [Model Context Protocol (MCP)](Model%20Context%20Protocol%20(MCP).md)

## References

- Model Context Protocol: **MCP Inspector** repository (README). https://github.com/modelcontextprotocol/inspector
- Model Context Protocol documentation: **Inspector** tool docs. https://modelcontextprotocol.io/docs/tools/inspector
- National Vulnerability Database (NVD): **CVE-2025-49596** references (links to upstream advisory and fix). https://nvd.nist.gov/vuln/detail/CVE-2025-49596
