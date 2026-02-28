# A2A Inspector

**A2A Inspector** (also referred to as the **A2A Protocol Inspector**) is an open-source, web-based developer tool for inspecting, debugging, and validating servers that implement the **Agent2Agent (A2A) protocol**.

The project provides a browser UI that can connect to an A2A agent server, fetch and display the agent’s **Agent Card**, run basic specification-compliance checks, and show the raw on-the-wire JSON-RPC messages exchanged with the server.

## Overview

The A2A Inspector is intended as a development aid for teams building A2A-compatible agents. Its documented feature set includes:

- Connecting to an A2A agent by base URL (for example, a local server).
- Fetching and displaying the agent’s **Agent Card**.
- Performing basic **spec compliance** validation on the agent card.
- A live chat UI for sending and receiving messages.
- A debug console for viewing raw **JSON-RPC 2.0** messages sent and received.

## Implementation

The repository describes a two-part architecture:

- A **FastAPI** backend (Python) that handles communication with the A2A agent.
- A **TypeScript** frontend that provides the web interface.

The project documentation lists Python and Node.js tooling prerequisites and provides instructions for running the inspector locally or via Docker.

## Relationship to A2A

A2A Inspector targets servers implementing the **Agent2Agent (A2A) protocol**, which defines an interoperability layer for agent-to-agent communication. In practice, the inspector is used to exercise A2A endpoints and to observe and validate protocol-level exchanges.

## References

1. https://github.com/a2aproject/a2a-inspector
