# Agent Communication Protocol (ACP)

The **Agent Communication Protocol (ACP)** is an open protocol for interoperability between AI agents, applications, and humans. It defines a **RESTful HTTP API** for **agent discovery** and for creating and managing **agent runs** that can be **synchronous**, **asynchronous**, or **streamed**. https://agentcommunicationprotocol.dev/introduction/welcome

ACP is developed in the open and is associated with the BeeAI ecosystem. The reference implementation and SDKs live in the `i-am-bee/acp` repository. https://github.com/i-am-bee/acp

## What ACP standardizes

ACP aims to reduce fragmentation by providing a shared “communication surface” that does not require agents to share internal implementation details. https://agentcommunicationprotocol.dev/introduction/welcome

Key ideas you’ll see in ACP docs and spec:

- **REST-based communication over HTTP** (no special transport required). https://agentcommunicationprotocol.dev/introduction/welcome
- **Multimodal messages** where parts are identified by **MIME types** (e.g., `text/plain`, images, JSON, etc.). https://agentcommunicationprotocol.dev/introduction/welcome
- **Async-first execution** (long-running tasks) while still supporting sync calls. https://agentcommunicationprotocol.dev/introduction/welcome
- **Streaming interactions** via `text/event-stream` (Server-Sent Events) for incremental output. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- **Agent discovery** via a standard endpoint. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

## Protocol surface (concrete)

ACP publishes an **OpenAPI specification** describing endpoints and data models. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

At a high level, the spec includes:

- `GET /agents` — list available agents (discovery). https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /agents/{name}` — fetch an agent manifest. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs` — create a run for an agent. The response may be immediate JSON or a streamed `text/event-stream`. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /runs/{run_id}` — poll run status/results. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs/{run_id}` — resume a run (e.g., after it enters an awaiting state). https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `POST /runs/{run_id}/cancel` — request cancellation. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
- `GET /runs/{run_id}/events` — list events emitted by a run. https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml

## Relationship to other agent interoperability efforts

ACP is one of several efforts aimed at agent interoperability. Compared with protocols that use JSON-RPC as a base message format, ACP emphasizes **REST-based** integration via familiar HTTP patterns. https://agentcommunicationprotocol.dev/introduction/welcome

## References

- ACP docs (overview): https://agentcommunicationprotocol.dev/introduction/welcome
- ACP repository: https://github.com/i-am-bee/acp
- ACP OpenAPI spec (raw): https://raw.githubusercontent.com/i-am-bee/acp/main/docs/spec/openapi.yaml
