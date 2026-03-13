# MCP Inspector

**MCP Inspector** is an interactive developer tool for testing and debugging servers that implement the **Model Context Protocol (MCP)**. It provides a browser-based UI for exploring a server’s resources, prompts, and tools, and includes a local proxy component to connect the UI to MCP servers over multiple transport types (for example, stdio and server-sent events).

## Overview

The MCP Inspector is distributed as an npm package and can be run without installation using `npx`. The project describes two main components:

- **MCP Inspector Client (MCPI)**, a React-based web UI.
- **MCP Proxy (MCPP)**, a Node.js service that bridges between the browser UI and MCP servers using supported transports.

According to the MCP documentation, the Inspector is part of the broader MCP debugging toolkit and is intended for interactive testing during MCP server development.

## Usage

The MCP documentation states that the Inspector can be run directly with `npx`.

It also documents workflows for inspecting MCP servers distributed via package registries (such as npm or PyPI) as well as locally developed servers, by launching the target server through the Inspector.

## Security considerations

The project documentation emphasizes that the Inspector includes a proxy component that can spawn local processes and communicate with local MCP servers. It advises against exposing the proxy server to untrusted networks.

The repository README also describes an authentication mechanism for the proxy server, including generating a session token and requiring it as a bearer token for requests.

## See also

- [Model Context Protocol (MCP)](model-context-protocol.md)
- [MCP Registry](mcp-registry.md)

## References

- Model Context Protocol documentation: “MCP Inspector”. https://modelcontextprotocol.io/docs/tools/inspector
- GitHub repository: modelcontextprotocol/inspector. https://github.com/modelcontextprotocol/inspector
