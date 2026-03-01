# Agent Communication Protocol (ACP)

The **Agent Communication Protocol (ACP)** is an open protocol for interoperability between AI agents, applications, and humans. It defines a **RESTful HTTP API** for **agent discovery** and for creating and managing **agent runs** that can be **synchronous**, **asynchronous**, or **streamed**. https://agentcommunicationprotocol.dev/introduction/welcome

ACP is developed in the open and is associated with the BeeAI ecosystem. The reference implementation and SDKs live in the `i-am-bee/acp` repository. https://github.com/i-am-bee/acp

## What ACP standardizes

ACP aims to reduce fragmentation by providing a shared “communication surface” that does not require agents to share internal implementation details. https://agentcommunicationprotocol.dev/introduction/welcome

Key concepts in ACP:

- **REST-based communication over HTTP** (no special transport required). https://agentcommunicationprotocol.dev/introduction/welcome
- **Agents** as discoverable capabilities exposed by an ACP server. `GET /agents` lists registered agents. https://agentcommunicationprotocol.dev/how-to/discover-and-run-agent
- **Runs** as the unit of execution for invoking an agent, with multiple execution modes (sync/async/stream). https://agentcommunicationprotocol.dev/how-to/discover-and-run-agent
- **Messages** as structured, ordered, multi-part (multi-modal) inputs/outputs.
  - Each message has a `role` (e.g., `user`, `agent`, or `agent/{name}`). https://agentcommunicationprotocol.dev/core-concepts/message-structure
  - Each message contains ordered `parts`, where each part is typed by a MIME `content_type` (e.g., `text/plain`, `image/png`) and provides either inline `content` or a `content_url`. https://agentcommunicationprotocol.dev/core-concepts/message-structure
- **Streaming** via **Server-Sent Events (SSE)** using `text/event-stream` for incremental output. https://agentcommunicationprotocol.dev/how-to/discover-and-run-agent

## Protocol surface (concrete)

ACP publishes an **OpenAPI specification** describing endpoints and data models. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

At a high level, the spec includes:

- `GET /agents` — list available agents (discovery). https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /agents/{name}` — fetch an agent manifest. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs` — create a run for an agent.
  - In “streaming” mode, clients can request SSE output with `Accept: text/event-stream`. https://agentcommunicationprotocol.dev/how-to/discover-and-run-agent
  - The OpenAPI spec documents the request/response shapes. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /runs/{run_id}` — poll run status/results. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs/{run_id}` — resume a run (e.g., after it enters an awaiting state). https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs/{run_id}/cancel` — request cancellation. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /runs/{run_id}/events` — list events emitted by a run. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

## Relationship to other agent interoperability efforts

ACP is one of several efforts aimed at agent interoperability. Compared with protocols that use JSON-RPC as a base message format, ACP emphasizes **REST-based** integration via familiar HTTP patterns. https://agentcommunicationprotocol.dev/introduction/welcome

## References

- ACP docs (overview): https://agentcommunicationprotocol.dev/introduction/welcome
- Discover & run agent (modes + streaming): https://agentcommunicationprotocol.dev/how-to/discover-and-run-agent
- Message structure (roles, parts, MIME typing): https://agentcommunicationprotocol.dev/core-concepts/message-structure
- ACP repository: https://github.com/i-am-bee/acp
- ACP OpenAPI spec (raw): https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
